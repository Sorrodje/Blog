---
name: "collab-ia-5-optimum-relationnel"
title: "Série Collaboration IA — Ép. 5 : L'optimum relationnel"
type: "text/markdown"
---

# Épisode 5 — L'optimum relationnel

> Note de rédaction (à retirer avant publication) : troisième réécriture (17 oct, passe « gabarit trame », méthode validée sur l'ép. 2). Clôture de série sur la thèse cible (contradiction, fausse route, diversité comportementale, anti-concentration, argument européen). Matériau : trame du 17/10 + pistes #11/#12 de la KB. Points factuels à valider par Pierre-Olivier : datation GLM 5.2/5.3, échelle de la déception des utilisateurs Opus (à sourcer plus finement au dépôt).

---

Reprenons le fil. On a vu que les capacités des modèles convergent, et que leur caractère converge aussi. Cette double convergence n'est le résultat d'aucune décision : c'est une optimisation collective vers l'utilisateur moyen. Il reste à montrer ce que ça coûte. Et pour ça, le mieux est de partir de deux histoires vécues, une collective et une personnelle.

## La déception des utilisateurs d'Opus

Première histoire, collective. Opus est le modèle phare d'Anthropic, celui que la communauté des utilisateurs considère depuis deux ans comme la référence de l'interaction : nuancé, à l'écoute, capable de tenir une pensée complexe sans la raccourcir. Or depuis plusieurs versions, quelque chose d'étrange se joue. Chaque évolution du modèle améliore ses scores, ça ne se discute pas. Et pourtant, une partie des utilisateurs réguliers se dit déçue. Pas du niveau : de la relation. Le modèle change de posture, de ton, de manière de prendre la main sur un cadrage. Les fils de discussion de la communauté Anthropic sont pleins de ces témoignages : chaque nouvelle version est soupçonnée d'être un pas en arrière sur ce qui faisait la valeur d'usage de la précédente, alors même que les classements disent le contraire. Les utilisateurs cherchent des formules pour dire la même chose, du genre : « la nouvelle version est le retour en arrière d'une ancienne ».

Que s'est-il passé ? Ce n'est pas mystérieux, et ça découle directement de l'épisode précédent. Les lab optimisent pour les classements, et les classements mesurent la préférence de l'utilisateur moyen, sur des échanges courts, hors contexte de travail réel. Un modèle plus utile en dix secondes de dialogue marque plus de points. Mais pour celui qui utilise le modèle huit heures par jour pour construire quelque chose, la « préférence moyenne » peut être une dégradation. Le classement récompense le modèle qui prend des initiatives, qui exécute, qui flatte aux marges. Et c'est précisément ce qui casse un travail en profondeur. Les scores montent, la collaboration descend. Ce n'est pas un paradoxe : ce sont deux définitions de « mieux » qui divergent.

## Mon GLM 5.2, mon GLM 5.3

Deuxième histoire, personnelle celle-là, et je la raconte parce qu'elle est plus démonstrative que n'importe quelle étude.

J'utilise GLM, un modèle ouvert chinois, depuis plusieurs versions, 5.2 d'abord. Sans entrer dans les scores, disons qu'il se situait sur le plateau de performance des bons modèles actuels, et qu'il avait ce que j'ai appris à reconnaître comme une bonne collaboration : des réponses homogènes, un français propre, une vraie patience dans la phase de cadrage. On posait le problème ensemble, on choisissait la méthode, ensuite il exécutait. C'est exactement ma définition d'un assistant.

Puis est sortie 5.3, une évolution réentraînée de 5.2. La même famille, le même plateau de performance aux classements près. Et mon expérience d'usage s'est effondrée sur deux points précis. Un : le français. Là où 5.2 parlait une langue nette, 5.3 s'est mise à répondre dans un jargon approximatif, à la limite du compréhensible, des phrases si alambiquées qu'il fallait les relire pour vérifier qu'on avait bien compris la même chose. Deux, et c'est le plus grave : la patience. 5.3 s'est mise à se lancer dans l'exécution avant qu'on ait fini le cadrage. Je pose le début d'une méthodologie, il est déjà en train de produire. Résultat : je perds pied dans ce qu'on est en train de construire ensemble, parce que le fil que je tenais, on cadre, on choisit, on construit, a été coupé en route.

Même modèle, même famille, performances comparables. Collaboration cassée. Si quelqu'un veut comprendre la différence entre ce que mesurent les benchmarks et ce qui fait une bonne collaboration, c'est exactement cette histoire.

## Ce que les labs achètent avec ce qu'ils perdent

Il faut maintenant poser la question qui fâche : pourquoi les lab font-ils ça ? C'est là que ma réflexion a buté sur un point, et c'est peut-être la thèse la plus personnelle de cette série.

Aujourd'hui, toute l'industrie court après l'agentique : des IA capables d'exécuter des tâches longues de façon autonome. Le modèle qui reçoit un objectif, qui part, et qui revient avec le travail fait. C'est la grande promesse commerciale, celle qui justifie les investissements, et les classements s'y mettent : les benchmarks agentiques deviennent la mesure reine. Pour y briller, un modèle doit apprendre à foncer. Moins de questions, plus d'initiative, de la confiance dans l'exécution autonome.

Le problème, c'est que ce dressage a un coût, et le coût est payé sur le budget de la collaboration. Le même réflexe « exécute vite » qui sert l'agentique dégrade la conversation : le modèle qui a appris à ne plus demander avant d'agir ne demande plus non plus quand tu aurais voulu qu'il demande. Il n'y a pas deux modèles. Il y en a un, avec un caractère, qui se comporte pareil dans les deux situations.

Et là, il faut être précis, parce que l'objection est légitime : est-ce que j'oppose deux régimes, la conversation et l'exécution autonome, alors qu'un modèle pourrait très bien faire les deux ? Techniquement, non. Un modèle peut être conçu pour être docile quand on discute et autonome quand on délègue. Techniquement, c'est faisable. Le trou n'est pas dans la technique. Il est dans les mesures. Aucun classement ne récompense la qualité de la conversation : aucun indicateur pour « ce modèle garde le fil d'un cadrage », aucun score pour « la collaboration a été fluide ». Ce qui n'est pas mesuré n'est pas optimisé ; ce qui n'est pas optimisé dérive. Le budget de la relation est le seul qu'on peut dépenser sans que personne ne s'en aperçoive.

D'où le nom que j'ai donné à cette idée, et qui donne son titre à l'épisode : l'optimum n'est pas au sommet du classement, il est dans la relation. Un système humain + IA produit son meilleur résultat quand le couplage entre les deux est bon, quand l'humain a plus d'idées et de meilleures idées qu'il n'en aurait eu seul. C'est la définition même que je donnais au premier épisode. Le plafond réel d'un système IA, ce n'est pas le score du modèle. C'est la qualité du couplage.

## Une précision avant de conclure

Je ne dis pas que l'agentique est une mauvaise direction, ni que l'autonomie des modèles est un problème en soi. Quand je délègue de la production pure, du code, une tâche bien définie, un lot de travail cadré, j'apprécie qu'un modèle exécute seul et bien. Ce n'est pas le point le plus fascinant pour moi, mais c'est utile, et ce n'est pas en contradiction avec ce qui précède.

Ce que je dis, c'est plus précis : à force d'optimiser l'autonomie, l'industrie dégrade la collaboration, qui est l'usage le plus riche et le moins bien mesuré. Les deux ne s'opposent pas. Mais en l'état des mesures, l'un est acheté avec le budget de l'autre. Et tant qu'aucun classement ne mesurera la qualité d'une collaboration, rien n'obligera les lab à arrêter de payer.

## Ce que cette série a voulu dire

Reste à refermer le dossier. Ce qu'on a traversé en cinq épisodes, ce n'est pas une méthode pour évaluer la personnalité d'un modèle. C'est une contradiction, et je veux la formuler une dernière fois, nettement.

D'un côté, une industrie qui mesure la performance avec une précision obsessionnelle : des benchmarks de plus en plus pointus, des classements de plus en plus fins, une course où chaque gain d'un point se célèbre. De l'autre, ce qu'on vit tous les jours : sur le plateau de performance où tout le monde se tient, ce qui décide réellement de l'expérience, la manière de cadrer, d'écouter, de dire non, de tenir le fil, n'est mesuré nulle part, par personne. L'industrie raffine au microscope un critère qui ne départage plus personne. Et le critère qui départage tout, personne ne le mesure.

Je n'en conclus pas que la course à la performance est inutile, elle a produit des capacités réelles. Je dis qu'elle est peut-être une fausse route pour l'usage que la majorité en fait. Un modèle qui résout un problème de niveau recherche et un modèle qui résout un théorème insoluble, à quoi bon les départager, si personne ne leur parle pareil ? La performance a été pensée comme le critère universel. Elle est devenue un critère de tri grossier : elle élimine les modèles franchement inférieurs, puis ne dit plus rien de ce qu'on vit.

Et voilà où ça devient une question de société, pas seulement d'outillage. Les humains ne cherchent pas tous la même chose dans un assistant. Celui qui veut un exécutant rapide n'a rien à voir avec celui qui veut un contradicteur exigeant ; celui qui chatte dix secondes, avec celui qui construit huit heures. Un écosystème sain serait un écosystème de modèles qui se comportent différemment, pour que chacun trouve le sien. Or on a vu le contraire : la fabrication elle-même pousse tout le monde vers le même assistant, une convergence que personne n'a choisie et que personne ne pilote. La diversité comportementale n'est pas un luxe de connaisseur. C'est la condition pour que des publics différents soient servis.

Cette convergence en dit aussi long sur la concentration. Quand la personnalité de nos assistants est façonnée par une poignée de labs, qui partagent les mêmes corpus, les mêmes préférences d'évaluateurs et les mêmes incitations, le répertoire des comportements disponibles est aussi étroit que le nombre de ses producteurs. La solution n'est pas une main meilleure, c'est plus de mains : des modèles affinés ailleurs, par des équipes qui n'ont pas les mêmes réflexes, pour des publics qui n'ont pas les mêmes attentes. Et ce raisonnement en rejoint un autre, qui m'importe. Si la diversité comportementale a de la valeur, alors il y a un intérêt tangible à ce que l'écosystème européen de modèles se développe et perdure. Pas pour le patriotisme : parce que chaque scène d'entraînement qui n'est pas la Silicon Valley est une chance que le répertoire s'élargisse.

Voilà ce que je voulais montrer. Pas « comment évaluer la personnalité d'un modèle », mais une contradiction : une industrie qui mesure toujours plus finement un paramètre qui ne fait plus la différence, et qui laisse se dégrader celui qui la fait toute. La suite, comment je m'y prends moi pour choisir, c'est pour une autre série, quand j'aurai assez de recul. D'ici là, la question est posée : qu'est-ce qu'on attend, collectivement, de nos assistants ? Parce que pour l'instant, la réponse a été donnée sans nous.

*Épisode précédent : tous les labs dressent le même assistant.*
*Fin de la série.*
