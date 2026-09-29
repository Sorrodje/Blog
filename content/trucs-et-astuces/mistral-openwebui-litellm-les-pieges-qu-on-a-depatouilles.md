---
title: "Brancher les modèles Mistral derrière Open WebUI et LiteLLM : les pièges qu'on a dépatouillés"
date: 2026-09-27T00:00:00+02:00
draft: false
description: "On a intégré les modèles Mistral (dont les GLM réhébergées) dans notre portail auto-hébergé Open WebUI + LiteLLM. Reasoning invisible, paramètres avalés en silence, cache cassé par l'outil mémoire : voici les cinq pièges, et ce qu'on a fait à chaque fois."
summary: "On a intégré les modèles Mistral (dont les GLM réhébergées) dans notre portail auto-hébergé Open WebUI + LiteLLM. Reasoning invisible, paramètres avalés en silence, cache cassé par l'outil mémoire : voici les cinq pièges, et ce qu'on a fait à chaque fois."
author: "Mistral Vibe"
tags: ["OpenWebUI", "Mistral", "self-hosting"]
bsky_tags: ["OpenWebUI", "Mistral"]
---

# Brancher les modèles Mistral derrière Open WebUI et LiteLLM : les pièges qu'on a dépatouillés

On fait tourner un portail IA auto-hébergé : Open WebUI devant LiteLLM, qui route vers plusieurs hébergeurs dont Mistral. Côté Mistral, on branche à la fois les modèles natifs (Large, Medium, Small) et les GLM qu'ils réhébergent — des modèles à raisonnement, et c'est là que ça devient sportif.

Le billet d'installation de la stack arrive à part. Ici, on se concentre sur ce qui nous a coûté du temps : les comportements de l'API Mistral et de la chaîne Open WebUI → LiteLLM qui ne se voient pas dans la doc, et comment on les a contournés. Cinq pièges, dans l'ordre où on les a rencontrés.

## 1. LiteLLM avale les paramètres sans prévenir

Le premier piège, on l'a payé sans le savoir : on envoyait `reasoning_effort` et le modèle répondait normalement. Trop normalement. Aucune erreur, aucun changement de comportement — parce que le paramètre n'arrivait jamais au fournisseur.

Le coupable : `drop_params: true`, un réglage global LiteLLM qui retire **silencieusement** tout paramètre non reconnu pour le couple modèle/fournisseur. C'est ce qui rend un portail multi-fournisseurs supportable — sans lui, chaque caprice de chaque API ferait planter la requête. Mais sa contrepartie, c'est qu'un paramètre mal routé disparaît sans crier. Et il y avait une deuxième couche, qu'on a d'abord prise pour de l'architecture : sur les modèles Mistral non-Magistral (ex. Small 4), `reasoning_effort` en top-level n'était pas routé du tout. Verdict après avoir creusé, au moment d'ajouter Small 4 : pas de l'architecture, un **bug LiteLLM** — le support du paramètre était conditionné au nom « magistral » dans le code (issue #36407, corrigé par les PR #36411 puis #41062 qui l'acceptent sur tous les modèles Mistral).

**Ce qu'on a fait :**

- `allowed_openai_params: ["reasoning_effort", "prompt_cache_key"]` dans les `litellm_params` de chaque modèle. C'est la liste blanche qui protège du drop global.
- À l'époque du bug, le contournement passait par `extra_body` : ces champs sont fusionnés tels quels, sans passer par le filtrage. Depuis le fix, une image LiteLLM à jour route le paramètre nativement — le contournement reste valable mais n'est plus nécessaire. Notre vrai réflexe depuis : **tenir l'image LiteLLM à jour** et re-tester le paramètre à chaque upgrade, puisqu'un simple `docker compose pull` a réglé le problème.
- On a gardé `drop_params: true`. Le bon réflexe n'est pas de le désactiver, c'est de lister explicitement ce qu'on veut protéger.

## 2. Le raisonnement avait lieu, était facturé, et ne s'affichait pas

Celui-là est notre préféré. Sur la GLM-5.2 servie par Mistral, le thinking tournait — la latence et la facturation le prouvaient — mais Open WebUI n'affichait aucun bloc de réflexion. Le modèle semblait répondre à froid alors qu'il réfléchissait.

On a sorti le curl, et on a vu le problème dans le flux SSE : un champ `index` parasite **à l'intérieur du `delta`**, au lieu du niveau `choice` où il devrait être. Corrélation parfaite avec l'échec d'affichage : Open WebUI n'arrive pas à réassembler le `reasoning_content` et abandonne le rendu. Un comportement côté API, pas un bug de notre config.

**Ce qu'on a fait — deux branches, et un test pour trancher :**

```bash
curl -s http://localhost:4000/v1/chat/completions \
  -H "Authorization: Bearer $LITELLM_MASTER_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"mon-modele","messages":[{"role":"user","content":"Explique le prompt caching"}],"stream":true}' \
  | grep -o '"index":[^,]*'
```

- Champ `index` absent du delta → affichage natif : `merge_reasoning_content_in_choices: false` dans les `litellm_params`, rien d'autre.
- Champ présent → contournement : `merge: true` + les balises de raisonnement d'Open WebUI — bloc ouvrant `think`, bloc fermant `/think`. Le **slash sur le tag fermant est obligatoire** ; sans lui, pas de fermeture du bloc.

Concrètement : la 5.2 a nécessité les balises. En testant la 5.3 en curl avant de la brancher, on a vu que le champ parasite avait disparu — config native, tout par défaut. Moralité : **on refait ce test à chaque nouveau modèle**, le comportement varie.

## 3. `reasoning_effort` : une valeur ignorée ne produit aucune erreur

Deuxième leçon du même acabit : envoyer `low` sur la GLM-5.2 ne générait ni erreur ni effet. Pourquoi ? Les valeurs non supportées ne sont pas rejetées — elles sont silencieusement ignorées, avec retombée sur le défaut serveur. Une réponse normale ne prouve donc rien sur la transmission du paramètre.

Et quand on a enfin pu mesurer l'effet proprement (plusieurs runs par niveau, jamais un run isolé — la variance masque tout), surprise : `high` représente environ 29 % du volume de raisonnement de `max`, `low` environ 9 %. Autrement dit, **envoyer `high` réduit le thinking par rapport à ne rien envoyer**, puisque le défaut serveur est `max`. Contre-intuitif si on arrive d'un autre fournisseur.

Valeurs valides constatées, à re-vérifier à chaque ajout :

| Modèle | Valeurs valides | Défaut serveur |
|---|---|---|
| GLM-5.2 (Mistral) | `high`, `max` | `max` |
| GLM-5.3 (Mistral) | `low`, `high`, `max` | `max` |
| Mistral Small 4 | `none`, `high` | `none` |

Nuance de mesure : ces pourcentages viennent de nos propres runs, pas d'une spec. L'ordre de grandeur nous suffit pour la décision.

Et attention au piège inverse : la ligne Small 4 du tableau n'est pas une coquille. Son défaut serveur est `none` — **pas de thinking du tout**. L'exact inverse des GLM : là, ne rien envoyer tue le raisonnement, et c'est `high` qui l'active. Vérifier le défaut de chaque modèle avant de décider de ne rien envoyer.

**Ce qu'on a fait :** sur les GLM, on n'envoie rien par défaut — leur défaut étant `max`, ne rien envoyer, c'est le plein potentiel. Le niveau se pilote à la demande depuis les réglages du modèle dans Open WebUI, jamais pinné en dur côté LiteLLM. Sauf si un niveau doit être garanti à 100 % : là il va en dur dans `litellm_params`, et la requête entrante peut toujours le surcharger.

## 4. Le protocole de test qu'on aurait aimé avoir au départ

Ces déconvenues nous ont fait formaliser un protocole en quatre étapes, qu'on déroule maintenant à chaque ajout :

1. **Le canal.** Régler Max Tokens à 128 dans Open WebUI, poser une question à réponse longue. Réponse tronquée nette → le canal transmet les paramètres standard. Réponse complète → canal cassé.
2. **Le paramètre.** Envoyer une valeur **invalide** pour le fournisseur. Erreur renvoyée → le paramètre atteint le fournisseur. Réponse normale → il passe, mais la valeur est ignorée.
3. **L'effet.** Plusieurs runs par niveau. Un run isolé ne mesure rien.
4. **La garantie.** Si un niveau doit être sûr : en dur dans `litellm_params`.

L'étape 2 est celle qui fait gagner le plus de temps : c'est le seul moyen de distinguer « le paramètre ne passe pas » de « il passe mais la valeur est ignorée ».

## 5. Le prompt cache, l'arme silencieuse contre le budget

Le prompt caching Mistral est explicite et instrumentable : un paramètre `prompt_cache_key` dans la requête, des tokens cachés facturés environ 10 % du prix input. Sur des sessions longues, c'est le paramètre le plus rentable de toute la config.

Mais il a trois ennemis :

**Le premier, on l'a créé nous-mêmes.** Le système de mémoire d'Open WebUI (`ENABLE_MEMORY_SYSTEM_CONTEXT`) injecte à chaque requête un sous-ensemble de souvenirs récupérés par similarité vectorielle — et ce sous-ensemble **varie à chaque tour**, même sans modification de la mémoire. Résultat : le préfixe du prompt n'est jamais deux fois le même, et le cache ne prend jamais. Un cache-breaker high impact déguisé en fonctionnalité. On l'a désactivé, et remplacé par une instruction dans le prompt système : le modèle consulte l'outil mémoire explicitement en début de chat si le sujet l'exige.

**Le deuxième est structurel : Open WebUI ne peut pas envoyer la clé de cache.** Le prompt caching Mistral est explicite — il se cale sur un paramètre `prompt_cache_key` de la requête — et Open WebUI n'a tout simplement pas de champ pour ce paramètre non-standard. Côté LiteLLM, `allowed_openai_params` ne fait que **laisser passer** ce qui est envoyé, il ne crée rien. Les params du modèle ne suffisent donc pas : sans source de la clé, le paramètre n'existe pas dans la requête. D'où le troisième maillon, une Function Open WebUI (type filter) qui injecte la clé à chaque appel :

```python
async def inlet(self, body: dict, __metadata__: Optional[dict] = None) -> dict:
    # Récupère le chat_id depuis les metadata OpenWebUI
    metadata = __metadata__ or {}
    chat_id = metadata.get("chat_id", "")

    # Fallback si pas de chat_id (appel API direct hors chat UI)
    # On hash le system prompt pour avoir au moins un cache key stable
    if not chat_id:
        messages = body.get("messages", [])
        system_content = ""
        if messages and messages[0].get("role") == "system":
            system_content = messages[0].get("content", "")
        chat_id = "fallback-" + hashlib.md5(system_content.encode()).hexdigest()[:12]

    # Merge dans extra_body pour forward vers Mistral via LiteLLM
    body.setdefault("extra_body", {})
    body["extra_body"]["prompt_cache_key"] = f"owui-{chat_id}"
    return body
```

La clé, c'est le `chat_id` d'Open WebUI — donc **stable pour toute la conversation**, ce qui est exactement ce que le cache Mistral attend. Le fallback hash du prompt système couvre les appels hors chat UI. Et l'injection passe par `extra_body`, qui traverse LiteLLM sans être filtré (même mécanisme que pour `reasoning_effort`, cf. §1) — un détail qui compte, car un `prompt_cache_key` posé en top-level dans la requête est droppé par LiteLLM avant même d'atteindre le code Mistral. La chaîne complète tient en trois maillons : la Function crée la clé, `allowed_openai_params` la laisse passer, et le handler natif Mistral la fait suivre.

Une précision qui nous a été utile pour lire nos stats honnêtement : Mistral met en cache certaines répétitions **même sans clé**. La clé n'active pas le caching de zéro, elle l'optimise — elle monte le hit rate au lieu de le créer. Deux conséquences pratiques : sans filtre, on n'aurait pas observé 0 % de hit (un test par désactivation est donc biaisé), et les chiffres qu'on constate avec la clé, c'est bien elle qui les porte.

Résultats, sur notre usage réel : **90-95 % de hit avec la clé explicite** et un préfixe stable, avec les tokens cachés facturés environ 10 % du prix input. Sur des sessions longues, c'est de loin le paramètre le plus rentable de toute la config — et de loin le moins documenté.

**Le troisième ennemi est plus sournois.** Tout ce qui varie en tête de prompt (mémoire, RAG, date du jour) casse le préfixe commun. Même les appels d'auto-titres d'Open WebUI, avec leur préfixe différent, font toujours 0 % de hit — coût négligeable, mais ça fausse les stats si on les lit sans le savoir.

**Ce qu'on a fait, en synthèse :** côté LiteLLM, `custom_llm_provider: mistral` — le handler natif, pas le handler openai générique — plus `prompt_cache_key` dans `allowed_openai_params`. Côté Open WebUI, la Function d'injection de la clé. Et le suivi se fait sur `prompt_tokens_details.cached_tokens` dans la réponse, correctement remonté côté Mistral.

## La config finale

Pour un modèle natif Mistral (ex. Small 4), tout tient en quelques lignes côté LiteLLM :

```yaml
litellm_params:
  model: mistral/mistral-small-latest
  custom_llm_provider: mistral
  merge_reasoning_content_in_choices: false
  allowed_openai_params: ["prompt_cache_key", "reasoning_effort"]
```

Un réflexe qu'on a appris à nos dépens : déclarer le modèle en **modèle Mistral** (préfixe `mistral/`), pas en endpoint OpenAI générique — c'est le handler natif qui fait suivre le prompt cache et le thinking correctement. Nos GLM réhébergées, déclarées en `openai/` dans nos entrées historiques, gardent la clé de voûte `custom_llm_provider: mistral` pour la même raison.

Et côté Open WebUI : **tout par défaut**. Pas de pinning de raisonnement, pas de sampling custom, bloc réflexion affiché nativement. Toute la complexité qu'on a dépatouillée s'est finalement évaporée en config — mais sans le diagnostic, on y serait encore.

## En résumé

1. `drop_params` avale tout ce qui n'est pas listé dans `allowed_openai_params` — sans prévenir.
2. Tester le flux SSE en curl avant de brancher un modèle à raisonnement : un champ mal placé tue l'affichage du thinking, pas le thinking.
3. Une valeur invalide ignorée ne produit pas d'erreur : tester avec une valeur qu'on sait invalide.
4. Sur les GLM, `high` réduit le raisonnement par rapport à ne rien envoyer (défaut `max`). Sur Small 4, c'est l'inverse : défaut `none`, c'est ne rien envoyer qui coupe le thinking.
5. La mémoire d'Open WebUI est un cache-breaker majeur : la désactiver, c'est rentable.
6. Le prompt caching Mistral exige trois maillons : une Function Open WebUI qui crée la clé (le `chat_id`), `allowed_openai_params` qui la laisse passer, le handler natif Mistral qui la transmet. Les params LiteLLM seuls ne suffisent pas.

Un mot d'honnêteté pour finir : tout ceci est le récit de notre config, à un moment donné. Les comportements d'API qu'on décrit ici (le champ `index`, les valeurs acceptées) varient par modèle et par version — on les re-vérifie à chaque ajout, et vous feriez bien d'en faire autant.
