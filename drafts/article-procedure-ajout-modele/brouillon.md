# Ajouter un fournisseur et un modèle à son portail IA — notre to-do list

> Statut : brouillon de travail — en cours de rédaction, déroulé en conditions réelles avec OpenRouter le 18/10/2026. Chaque phase est documentée juste après avoir été exécutée. Ne pas merger vers main tant que l'article n'est pas finalisé.


# Ajouter un fournisseur et un modèle à son portail IA — notre to-do list

> Statut : en cours de rédaction, déroulé en conditions réelles avec OpenRouter le 18/10/2026. Chaque phase est documentée juste après avoir été exécutée.

---

## Intro (à figer en dernier)

Ce texte est notre to-do list, pas un tutoriel. On gère un portail IA auto-hébergé — Open WebUI pour l'interface, LiteLLM comme goulet unique vers les fournisseurs — et chaque fois qu'on ajoute un fournisseur ou un modèle, on déroule la même procédure. Elle est née des pièges qu'on a dépatouillés nous-mêmes : des paramètres avalés silencieusement, des modèles fantômes après suppression, des listes qui ne se rafraîchissent pas. On la publie telle quelle, telle qu'on l'exécute, avec le pourquoi de chaque geste. Elle est écrite pour notre stack, mais l'essentiel vaut pour toute installation Open WebUI + LiteLLM.

Prérequis : un portail Open WebUI + LiteLLM opérationnel, et une API key de fournisseur **avec un plafond de dépense**. Comment on obtient la clé et comment on pose le plafond côté fournisseur, ça dépend de chaque fournisseur — c'est hors périmètre ici. Le plafond, lui, n'est pas négociable : il est posé **avant** tout branchement.

Exemple déroulé ici : OpenRouter, fournisseur passerelle multi-modèles.

---

## La procédure

L'article se coupe en deux parties, comme la stack : tout ce qui est en amont (fournisseur, modèle, params, vérification) vit côté LiteLLM ; tout ce qui est en aval (visibilité, custom, usage) vit côté Open WebUI.

**Règle transversale pour les lecteurs en mode YAML** : cette procédure est écrite pour LiteLLM en mode base de données (gestion via le dashboard). Chaque phase portera un encart d'une à deux phrases « Et en YAML ? » sans détailler : phase 1 → la clé se pose en `api_key: os.environ/...` dans `litellm_params` ; phase 2 → le modèle est une entrée `model_list` (mêmes champs) ; phase 3 → les params se posent dans `litellm_params` de l'entrée ; à chaque modif YAML → `docker compose restart litellm`. Objectif : détromper le lecteur qui n'a pas compris qu'on est en mode DB, pas écrire un second tuto. L'intro mentionnera d'emblée les deux modes d'existence de LiteLLM pour poser le cadre.

### Partie I — Côté LiteLLM

#### Phase 1 — Déclarer le fournisseur

Menu **Models & Endpoints → onglet LLM Credentials → + Add Credential** :

1. **Credential Name** : identifiant technique (ex. `openrouter`) — c'est lui qu'on référencera dans les modèles.
2. **Display Name** : étiquette affichée (ex. `Openrouter`).
3. **Provider** : sélectionner le fournisseur (ex. Openrouter).
4. **API Key** : la clé du fournisseur, masquée à la saisie, stockée **chiffrée en base** (salt LiteLLM) — jamais en clair dans un YAML.
5. **Add Credential** pour valider. Le credential apparaît dans la liste de l'onglet.

Pourquoi ça se passe ici : LiteLLM est le goulet unique entre Open WebUI et le fournisseur. La clé vit dans sa base, Open WebUI ne la voit jamais. À ce stade, LiteLLM sait parler au fournisseur, mais **aucun modèle n'est encore exposé**.

#### Phase 2 — Ajouter le modèle

Menu **Models & Endpoints → + Add Model** :

1. **Provider** : Openrouter.
2. **Model** : `openrouter/nvidia/nemotron-3-ultra-550b-a55b:free` — double préfixe : `openrouter/` (routage LiteLLM) + ID OpenRouter complet, `:free` compris. Où trouver l'ID : catalogue openrouter.ai/models ou `curl https://openrouter.ai/api/v1/models | jq '.data[].id'`.
3. **Existing Credentials** : sélectionner le credential créé en phase 1 (pas de clé à retaper).
4. **Model Name** : laisser l'auto-remplissage par défaut (l'alias qu'Open WebUI verra).
5. **Test Connect** : vérifier que le modèle répond AVANT de l'enregistrer — si le test échoue, rien n'est cassé, on corrige et on reteste.
6. **Add Model** seulement si le test est OK.
7. **Vérifier la présence** — le geste de référence pour confirmer que le modèle est bien enregistré et vivant :

```bash
set -a; source /opt/docker/openwebui/.env; set +a
curl -s http://localhost:4000/v1/models -H "Authorization: Bearer $LITELLM_MASTER_KEY" | jq -r '.data[].id'
```

Le modèle doit apparaître dans la liste — l'alias est l'ID complet (ex. `nvidia/nemotron-3-ultra-550b-a55b:free`). Ce listage est aussi le **premier réflexe de diagnostic** : si un modèle n'apparaît pas quelque part, on vérifie d'abord ici s'il est vivant côté LiteLLM avant de chercher plus loin.

Bonus : les modèles attachés à un credential nommé sont tracés dans la page Usage avec un tag `Credential: <nom>` — la conso se filtre par fournisseur sans config supplémentaire.

#### Phase 3 — Les paramètres : doctrine GARANTIR / PILOTER

*(à documenter — le cœur durable de l'article)*

Règle : un paramètre à **GARANTIR à 100 %** va en dur dans les `litellm_params` (LiteLLM) ; un paramètre à **PILOTER à la main** reste côté Open WebUI, c'est l'utilisateur qui porte la valeur.

**Important — mode base de données** : cette procédure est écrite pour LiteLLM en mode DB (dashboard). Credentials, modèles et params vivent dans la base, le `litellm-config.yaml` ne contient plus aucun `model_list`. Conséquences : les params se posent via le dashboard (édition du modèle), pas dans un fichier ; et les modifs via dashboard sont appliquées à chaud — pas de restart du conteneur à chaque changement de modèle. Encart prévu pour les lecteurs en mode YAML : les mêmes params se posent dans `litellm_params` du `model_list` du fichier de config.

⚠️ Point de clarté à assumer : les paramètres et leurs valeurs **varient selon le fournisseur et le modèle**. L'article donne la méthode pour vérifier (page du modèle côté fournisseur + protocole de test), pas un tableau intemporel — un tableau serait périmé avant publication (leçon du billet Mistral dépublié).

Cas particulier de l'exemple : Nemotron 3 Ultra n'est pas natif du registre LiteLLM → config volontairement minimale au départ, les params utiles seront motivés par le test (montrer la méthode plutôt qu'une config à recopier).

**Le rôle de `drop_params: true` (global, posé dans le `litellm_settings` du YAML)** : LiteLLM retire **silencieusement** tout paramètre non reconnu pour le modèle/fournisseur — c'est lui qui avale `reasoning_effort` sur Mistral Large 3 sans erreur.

Pourquoi on le garde (à expliciter dans le tuto) :
1. **C'est lui qui rend le portail tolérant** : Open WebUI envoie systématiquement des paquets de params OpenAI (`frequency_penalty`, `logit_bias`, `user`...) selon les réglages de l'utilisateur. Sans lui, chaque modèle qui n'en connaît pas un renverrait une 400 — l'utilisateur verrait des chats planter pour des réglages qu'il ne sait même pas envoyer.
2. **C'est cohérent avec la doctrine** : quand un paramètre utile est filtré à tort, le réflexe est de l'ajouter à `allowed_openai_params` — ciblé, motivé par un test. Le désactiver globalement inverserait le fardeau : transmettre n'importe quoi à n'importe qui, y compris des paramètres que le fournisseur interpréterait de façon inattendue ou facturée.

Le coût du choix est faible : un paramètre droppé se détecte par le test à valeur invalide (pas d'erreur = avalé), et on décide alors en connaissance de cause. D'où ce test : il rend visible ce que `drop_params` rend invisible en usage normal.

Précision mode DB : même en mode DB, le YAML garde les `litellm_settings` globaux (seul le `model_list` vit en base) — le mentionner dans l'encart.

**Tous les modèles ne méritent pas la même approche — la fourche registre / hors registre** (doctrine issue du terrain, à intégrer en tête de phase 3) : le `/model/info` renseigne d'abord **l'état civil du modèle chez LiteLLM**.
- **Modèle connu du registre LiteLLM** (ex. `zai-glm-5-3`) : `supported_openai_params` auto-peuplé (dont `reasoning_effort`), pricing auto, routing natif → **pas de whitelist**, config minimale.
- **Modèle hors registre** (ex. GLM 5.3 Flash, Nemotron) : fiche muette (`supported_openai_params` vide ou minimal, `pricing_overrides` à remplir) → workarounds : `allowed_openai_params` **ciblé sur les seuls params prouvés utiles par le test**, `extra_body` côté Open WebUI pour ce qu'il ne sait pas envoyer nativement (`prompt_cache_key` passe par là — **jamais en whitelist**), coûts déclarés à la main.
- Illustration extrême : même famille, même hébergeur — la GLM 5.3 est native, la Flash dehors. La fourche se tranche par modèle, pas par fournisseur ni par famille.

**Piège schéma ≠ modèle** (découvert le 23/10 sur la Flash) : le vocabulaire énuméré dans l'erreur du curl `bidon` (ex. 422 Mistral : `none|minimal|low|medium|high|xhigh|max`) est celui du **schéma API**, pas les niveaux réels du modèle — la Flash ne distingue en vrai que `low`/`high`/`max`, défaut `max`, sans interrupteur off. L'énumération prouve la **transmission**, pas les **niveaux effectifs** : croiser avec la doc du modèle avant d'écrire quoi que ce soit en dur. Conséquence connexe : un modèle qui pense par défaut consomme son plafond `max_tokens` en réflexion (le test de troncation se lit dans `completion_tokens_details.reasoning_tokens`, pas dans le texte). LiteLLM tague ces comportements dans `provider_specific_fields` (`text_but_should_think`, `only_thinking`) — un diagnostic au-delà du `/model/info`.

##### Test de transmission d'un param (curl, depuis le serveur)

```bash
set -a; source /opt/docker/openwebui/.env; set +a
curl -s http://localhost:4000/v1/chat/completions \
  -H "Authorization: Bearer $LITELLM_MASTER_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"<alias>","messages":[{"role":"user","content":"Réponds en un mot : ok"}],"reasoning_effort":"bidon"}'
```

Lecture : erreur du fournisseur = le paramètre passe jusqu'au bout (on peut le GARANTIR) ; réponse normale = paramètre droppé (LiteLLM `drop_params`) ou avalé (OpenRouter) — creuser avant de conclure ; si le param doit passer mais est filtré → `allowed_openai_params`.

**Résultat de l'exemple (Nemotron 3 Ultra via OpenRouter)** : le fournisseur refuse `bidon` en énumérant les valeurs valides — `max | xhigh | high | medium | low | minimal | none`. Verdict : le paramètre traverse toute la chaîne, aucune config `litellm_params` nécessaire, `reasoning_effort` est PILOTABLE depuis Open WebUI. Leçon pour le lecteur : la liste des valeurs valides vient du fournisseur lui-même, pas d'un tableau d'article — c'est la méthode qui compte, chaque modèle/fournisseur a sa liste. ⚠️ Nuance (leçon Flash du 23/10) : cette énumération = vocabulaire du schéma API, les niveaux réels du modèle peuvent être plus restreints — à croiser avec la page du modèle avant d'exploiter.

##### Contre-exemple : quand ça ne marche pas (Mistral Large 3, provider direct Mistral)

Même curl de transmission, même valeur `bidon` → **réponse normale, aucune erreur**. Symptôme : le paramètre a été avalé quelque part. La doctrine impose de creuser avant de conclure.

**Diagnostic** : `curl /model/info` filtré sur le modèle, et regarder deux choses dans `model_info` :
- `supported_openai_params` : la liste des params OpenAI que LiteLLM accepte de transmettre à ce modèle. Pour Mistral Large : `stream, temperature, top_p, max_tokens...` — **pas de `reasoning_effort`** → c'est LiteLLM qui l'a droppé silencieusement.
- `supports_reasoning` / `reasoning_effort_levels` : `null` partout → le modèle n'expose aucun reasoning pilotable dans le registre LiteLLM.

**Décision doctrine** : on *pourrait* forcer le passage via `allowed_openai_params`, mais ça ne servirait à rien — le modèle ne supporte pas le paramètre. Verdict : rien à GARANTIR, rien à PILOTER, on n'insiste pas. Forcer un param vers un modèle qui ne le supporte pas = de la config inutile qui masque la réalité.

**Leçon de structure** : un paramètre a trois états possibles — transmis (Nemotron : le fournisseur rejette `bidon` en énumérant ses valeurs), droppé parce que non supporté (Mistral Large 3 : fiche `model/info`), ou transmis mais ignoré (cas intermédiaire à creuser). Le `/model/info` est l'outil de diagnostic central.

##### Troisième exemple : Mistral Small latest (provider direct) — même fournisseur, état différent

Même curl, `bidon` → **rejet 422, Mistral énumère son vocabulaire** : `none | minimal | low | medium | high | xhigh | max`. Le paramètre traverse, il est PILOTABLE depuis Open WebUI.

Deux leçons :
1. Deux modèles du **même fournisseur** peuvent être dans des états différents (Large 3 : droppé ; Small : transmis). On ne vérifie jamais « par fournisseur », on vérifie **par modèle**.
2. Le vocabulaire évolue : la doctrine d'origine (constatée à l'époque sur Mistral Small 4) disait `none`/`high` seulement ; l'API d'aujourd'hui expose sept niveaux. Dernière preuve que la vérification à l'ajout est la seule méthode pérenne — et que la page officielle du modèle + ce test valent mieux qu'un tableau d'article.
3. **La passerelle elle-même évolue** : il y a quelques semaines, LiteLLM rejetait `reasoning_effort` sur les modèles Mistral non-Magistral (`UnsupportedParamsError`), et le contournement était `allowed_openai_params: ['reasoning_effort']` sur chaque requête. Corrigé depuis (forwarding sur modèles hybrides, puis acceptation générale). Le même curl a donc changé de verdict sans qu'on touche à rien — le test à l'ajout prime toujours sur la doc ou sur la mémoire. Et `allowed_openai_params` reste dans la boîte à outils : contournement quand un param est bloqué à tort par la passerelle, ça redeviendra vrai pour un autre fournisseur demain.

##### Protocole de test complet (depuis Open WebUI — après la phase de visibilité)

*(à documenter : ① canal à 128 tokens max ; ② reasoning_effort invalide depuis OWUI ; ③ effet high vs max, plusieurs runs ; ④ garantie finale en dur)*

#### Phase 4 — Vérifier le fonctionnement (protocole de test)

*(à documenter — test côté LiteLLM en direct, puis les 4 étapes du protocole)*

### Partie II — Côté Open WebUI

#### Phase 5 — Rendre le modèle visible

*(à documenter : le refresh de connexion, sans lequel le modèle n'apparaît pas dans le sélecteur du Workspace)*

#### Phase 6 — Créer le modèle custom

*(à documenter : Workspace → Models, base model, prompt, params, KB)*

#### Bonus — Retirer un modèle proprement

*(à documenter : le problème des fantômes et la purge SQL)*

---

## Notes de rédaction (ne pas publier)

- Structure = le pense-bête consolidé (canvas `pense-bete-ajout-modele`), enrichi de ce qu'on vit avec OpenRouter.
- Règle anti-périssable : les valeurs par modèle (reasoning_effort etc.) = exemples d'illustration avec avertissement, pas vérités intemporelles. Doctrine GARANTIR/PILOTER = le socle durable.
- Cadrage acté : l'article commence après l'obtention de la clé fournisseur. Pas de couverture des procédures d'inscription/crédit par fournisseur.
- OpenRouter, point spécifique documenté : compte prépayé = le solde est déjà un plafond dur naturel ; limite par clé = sous-plafond (plancher UI à 50 $ constaté, mais 10 $ accepté). La nuance solde/limite-clé vaut 2 phrases dans l'intro des prérequis.
---

## Notes de rédaction (ne pas publier)

- Structure = le pense-bête consolidé, enrichi de ce qu'on vit avec OpenRouter.
- Règle anti-périssable : les valeurs par modèle (reasoning_effort etc.) = exemples d'illustration avec avertissement, pas vérités intemporelles. Doctrine GARANTIR/PILOTER = le socle durable.
- Cadrage acté : l'article commence après l'obtention de la clé fournisseur. Pas de couverture des procédures d'inscription/crédit par fournisseur.
- OpenRouter, point spécifique documenté : compte prépayé = le solde est déjà un plafond dur naturel ; limite par clé = sous-plafond (plancher UI à 50 $ constaté, mais 10 $ accepté). La nuance solde/limite-clé vaut 2 phrases dans l'intro des prérequis.
- Cadrage des exemples (18 oct) : deux exemples déroulés dans le corps (Nemotron = fil conducteur complet ; Mistral Large 3 = contre-exemple du paramètre droppé), Mistral Small en une parenthèse de la phase 3 (même fournisseur, état différent + évolution de la passerelle).
- Update 24/10 (doctrine Flash) : fourche registre/hors-registre en tête de phase 3, piège schéma ≠ modèle (l'énumération du curl = schéma API, pas niveaux réels), prompt_cache_key jamais en whitelist (extra_body), thinking par défaut qui consomme max_tokens.
