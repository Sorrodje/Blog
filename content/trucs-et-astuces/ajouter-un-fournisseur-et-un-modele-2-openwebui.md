---
title: "Ajouter un fournisseur et un modèle à son portail IA — 2. Le côté Open WebUI"
date: 2026-10-18T14:00:00+02:00
draft: false
description: "Modèle visible ou fantôme selon un toggle de cache, custom du Workspace, et deux tests de bout en bout : la suite de notre check list, côté Open WebUI cette fois."
summary: "Modèle visible ou fantôme selon un toggle de cache, custom du Workspace, et deux tests de bout en bout : la suite de notre check list, côté Open WebUI cette fois."
author: "Sorrodje et Mistral Vibe"
series: "Ajouter un fournisseur et un modèle à son portail IA"
weight: 2
tags: ["IA", "auto-hébergement"]
bsky_tags: [OpenWebUI, LiteLLM]
---

Ce billet est la seconde moitié d'une procédure commencée dans [la partie 1, côté LiteLLM](/trucs-et-astuces/ajouter-un-fournisseur-et-un-modele-1-litellm/) : credential, modèle, paramètres, protocole de test en curl. Ici, on bascule côté interface.

## La procédure rapide — côté Open WebUI

Pour reprendre la procédure quand on la connaît déjà. Le pourquoi de chaque geste et les pièges sont dans la version commentée ci-dessous.

1. **Vérifier la visibilité** — le nouveau modèle doit apparaître dans les modèles disponibles. Sinon : Admin Settings → Connections → rafraîchir la connexion LiteLLM (ou désactiver « Mettre en cache la liste des modèles de base »).
2. **Invisibiliser le modèle de base** — doctrine : le modèle nu ne se chat pas, il n'est qu'une brique.
3. **Créer le custom** — Workspace → Modèles → nouveau modèle basé sur le modèle de base ; y porter prompt système et configuration d'usage.
4. **Tester le canal depuis le chat** — Max Tokens à 128, question à réponse longue : réponse tronquée nette = le canal transmet.
5. **Tester les paramètres depuis le chat** — ne changer qu'un curseur entre deux runs (ex. effort de raisonnement high vs none) : bloc de réflexion et latence différents = le paramètre traverse et a un effet.
6. **Retrait** — custom : deux clics dans le Workspace ; modèle de base : suppression dans le dashboard LiteLLM, il disparaît automatiquement côté Open WebUI.

## La procédure — version commentée

### Phase 5 — Rendre le modèle visible

Une fois le modèle ajouté côté LiteLLM, il apparaît immédiatement dans les modèles disponibles des réglages administrateur d'Open WebUI. Pour autant, il peut **ne pas apparaître** dans le dropdown des modèles proposés — ni pour entamer un chat, ni comme base d'un modèle du Workspace — alors même qu'il est actif et visible en admin.

La cause est documentée dans l'interface elle-même : l'option « **Mettre en cache la liste des modèles de base** » (réglages admin) récupère les modèles de base **au démarrage ou lors de la sauvegarde des réglages** — plus rapide, mais elle peut ne pas afficher les modifications récentes.

![Le réglage « Mettre en cache la liste des modèles de base » dans l'admin Open WebUI, avec sa description](/img/proc-modele/owui-cache-toggle.png)

Deux remèdes, au choix :

1. **Le refresh de connexion** (procédure générique) : Admin Settings → Connections → rafraîchir la connexion LiteLLM. Le nouveau modèle apparaît aussitôt dans le sélecteur du Workspace. C'est le réflexe par défaut — il ne demande aucun réglage, et il vaut pour toute installation.
2. **Désactiver le toggle de cache** : la liste va alors chercher l'état réel à chaque accès, le refresh devient inutile. C'est un choix défendable sur un portail à un ou deux administrateurs ; on le paie en fetchs plus fréquents.

Un F5 ou un Ctrl+Shift+R côté navigateur ne suffit pas : le cache est côté backend, pas dans le navigateur.

#### Doctrinalement : le modèle de base ne sert pas en chat

Une fois le modèle visible, notre usage est de l'**invisibiliser** dans la liste des modèles disponibles côté admin. Le modèle nu ne doit pas être utilisé tel quel : on privilégie systématiquement les modèles créés via le Workspace, qui portent le prompt système, les paramètres et la configuration d'usage. Le modèle de base n'est qu'une brique — le lecteur d'un portail multi-utilisateurs ne doit voir que des modèles prêts à l'emploi.

### Phase 6 — Créer le modèle custom (et vérifier qu'il traverse)

On va dans Workspace → Modèles et on crée un nouveau modèle à partir de la base ajoutée en partie 1. L'éditeur permet d'adapter l'intégralité de la configuration — du moindre paramètre au prompt système. On ne détaillera pas la création ici : ce qui nous intéresse, c'est de **vérifier que cette configuration se transfère bien** de Open WebUI vers l'endpoint du fournisseur.

![L'éditeur de modèle du Workspace : nom, description, prompt système, réglages avancés](/img/proc-modele/owui-editeur-modele.png)

La responsabilité change de camp, elle ne disparaît pas : en partie 1, on vérifiait que les params du dashboard LiteLLM traversaient vers le fournisseur. Ici, c'est la configuration du custom Open WebUI qui doit traverser — et elle emprunte exactement le même goulet. D'où le même protocole de test, rejoué depuis le chat, sur le custom.

#### Test 1 — le canal (Max Tokens à 128)

Dans un chat sur le custom, régler Max Tokens à 128, poser une question qui demande une réponse longue :

> Décris-moi l'histoire du chemin de fer en Bourgogne : les premières lignes, les grandes compagnies, l'électrification, et le rôle de la gare de Dijon. Prends le temps d'être exhaustif.

Verdict : réponse **tronquée nette**, en plein milieu d'une phrase = le canal transmet la famille standard de paramètres, du custom jusqu'au fournisseur.

![La réponse du modèle coupée en pleine phrase, Max Tokens réglé à 128 dans les réglages du chat](/img/proc-modele/owui-test-128.png)

#### Test 2 — le paramètre de raisonnement : transmission ET effet

Le paramètre `reasoning_effort` qu'on a vérifié en partie 1 se règle ici depuis l'interface — le champ « Effort de raisonnement » des réglages avancés du chat. Deux niveaux, un même problème de maths :

> Un train part de Dijon à 14h17 et roule à 87 km/h vers Beaune, distante de 43 km. Un second train part de Beaune à 14h25 à 61 km/h vers Dijon. À quelle heure précise se croisent-ils, et à combien de km de Dijon ? Détaille ton raisonnement étape par étape.

**Run à effort maximal** : le bloc de réflexion est long (douze secondes de réflexion visible), la réponse est juste — croisement à ~14h37:44, à ~30 km de Dijon.

![Le run avec réflexion : bloc de réflexion de douze secondes, réponse juste](/img/proc-modele/owui-trains-avec-reflexion.png)

**Run sans réflexion** : pas de bloc de réflexion, réponse quasi immédiate — et **fausse** : ~14h28, à ~11,6 km de Dijon. Le modèle a traité le croisement comme si le second train était immobile.

![Le run sans réflexion : réponse immédiate et fausse](/img/proc-modele/owui-trains-sans-reflexion.png)

Ce qu'on vient de prouver, en un seul geste : le paramètre **traverse** (deux comportements radicalement différents sur le même custom, seule variable modifiée = le curseur d'effort) et il a un **effet réel** — pas seulement sur la latence, sur la correction de la réponse.

Précautions de lecture :

- L'effet se mesure sur la longueur du bloc de réflexion et la latence, pas sur la correction de la réponse — un modèle peut tomber juste sans réfléchir. Ne jamais conclure sur un run isolé.
- Si l'effort minimal ne change rien au comportement réflexif du modèle, le paramètre est peut-être avalé en route ou ignoré côté modèle : on retombe sur le test curl de transmission (partie 1) pour trancher.

#### Ce qu'on ne refera pas ici

Les étapes « effet entre deux niveaux intermédiaires » et « garantie en dur dans `litellm_params` » sont couvertes en partie 1. Le custom porte les valeurs côté utilisateur ; la doctrine ne met en dur côté LiteLLM que ce qui doit être garanti à 100 % — et pour notre fil conducteur, on a justement montré en partie 1 qu'aucune config n'était nécessaire.

### Bonus — Retirer un modèle proprement

Retirer un modèle dans le dashboard LiteLLM se répercute maintenant proprement côté Open WebUI : le modèle supprimé disparaît automatiquement de la liste, y compris avec l'option « Mettre en cache la liste des modèles de base » activée — vérifié en conditions réelles, toggle activé. Le réflexe retrait est donc tout simple : suppression dans le dashboard LiteLLM, et un rafraîchissement côté navigateur si la liste ne suit pas.

Les customs du Workspace pointant sur une base retirée, eux, se retirent depuis l'interface (deux clics sur le modèle concerné).

> **Note pour les installations plus anciennes** : les versions précédentes d'Open WebUI ne purgeaient jamais leur table des modèles — un modèle retiré de LiteLLM y restait listé comme **fantôme**, sans corbeille dans l'interface, et il fallait passer par une purge SQL dans la base :

```bash
cd <dossier-compose-du-portail>
sudo docker compose stop open-webui
# re-synchroniser la liste des vivants avant chaque purge :
curl -s http://localhost:4000/v1/models \
  -H "Authorization: Bearer $LITELLM_MASTER_KEY" | jq -r '.data[].id'
# purge : garder les modèles exposés par LiteLLM + les customs pointant dessus
sudo sqlite3 <chemin>/webui.db "DELETE FROM model WHERE id NOT IN ('<liste-des-ids-vivants>') AND (base_model_id IS NULL OR base_model_id NOT IN ('<liste-des-ids-vivants>'));"
sudo docker compose up -d open-webui
```

Points de vigilance qui gardent leur valeur si vous êtes dans ce cas :

- La liste des IDs vivants se re-synchronise par le listage `/v1/models` — jamais une liste en dur d'un ancien état.
- Les customs à garder s'identifient par `SELECT id, base_model_id FROM model WHERE base_model_id IS NOT NULL;`.
- Conteneur arrêté pendant l'écriture, backup préalable de la base.
- Après purge : le `count(*)` doit égaler (modèles LiteLLM vivants + customs).

Même si le comportement est corrigé, l'arrière-plan reste utile à connaître : c'est de ce problème de fantômes qu'est née notre procédure de vérification systématique à chaque retrait.