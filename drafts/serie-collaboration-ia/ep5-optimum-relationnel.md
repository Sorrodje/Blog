---
name: "collab-ia-5-optimum-relationnel"
title: "Série Collaboration IA — Ép. 5 : L'optimum relationnel"
type: "text/markdown"
---

# Épisode 5 — L'optimum relationnel

> Note de rédaction (à retirer avant publication) : scission du 18/10 — l'ancien épisode 5, devenu trop dense, est coupé en deux : ép. 5 (constat + argument) / ép. 6 « À quoi bon ? » (humain hors boucle + maths + clôture). Points factuels à valider par Pierre-Olivier : datation GLM 5.2/5.3, échelle de la déception des utilisateurs Opus.

---

Reprenons le fil. On a vu que les capacités des modèles convergent, et que leur caractère converge aussi. Cette double convergence n'est le résultat d'aucune décision : c'est une optimisation collective vers l'utilisateur moyen. Il reste à montrer ce que ça coûte. Et pour ça, le mieux est de partir de deux histoires vécues, une collective et une personnelle.

## La déception des utilisateurs d'Opus

Première histoire, collective. Opus est le modèle phare d'Anthropic, celui que la communauté des utilisateurs considère depuis deux ans comme la référence de l'interaction : nuancé, à l'écoute, capable de tenir une pensée complexe sans la raccourcir. Or depuis plusieurs versions, quelque chose d'étrange se joue. Chaque évolution du modèle améliore ses scores, ça ne se discute pas. Et pourtant, une partie des utilisateurs réguliers se dit déçue. Pas du niveau : de la relation. Le modèle change de posture, de ton, de manière de prendre la main sur un cadrage. Les fils de discussion de la communauté Anthropic sont pleins de ces témoignages : chaque nouvelle version est soupçonnée d'être un pas en arrière sur ce qui faisait la valeur d'usage de la précédente, alors même que les classements disent le contraire. Les utilisateurs cherchent des formules pour dire la même chose, du genre : « la nouvelle version est le retour en arrière d'une ancienne ».

Que s'est-il passé ? Ce n'est pas mystérieux, et ça découle directement de l'épisode précédent. Les lab optimisent pour les classements, et les classements mesurent la préférence de l'utilisateur moyen, sur des échanges courts, hors contexte de travail réel. Un modèle plus utile en dix secondes de dialogue marque plus de points. Mais pour celui qui utilise le modèle huit heures par jour pour construire quelque chose, la « préférence moyenne » peut être une dégradation. Le classement récompense le modèle qui prend des initiatives, qui exécute, qui flatte aux marges. Et c'est précisément ce qui casse un travail en profondeur. Les scores montent, la collaboration descend. Ce n'est pas un paradoxe : ce sont deux définitions de « mieux » qui divergent.

## Mon GLM 5.2, mon GLM 5.3

Deuxième histoire, personnelle celle-là, et je la raconte parce qu'elle est plus démonstrative que n'importe quelle étude.

J'utilise GLM, un modèle ouvert chinois, depuis plusieurs versions, 5.2 d'abord. Sans entrer dans les scores, disons qu'il se situait sur le plateau de performance des bons modèles actuels, et qu'il avait ce que j'ai appris à reconnaître comme une bonne collaboration : des réponses homogènes, un français à peu près propre, une vraie patience dans la phase de cadrage. On posait le problème ensemble, on choisissait la méthode, ensuite il exécutait. C'est exactement ma définition d'un assistant.

Puis est sortie 5.3, une évolution réentraînée de 5.2. La même famille, le même plateau de performance aux classements près. Et mon expérience d'usage s'est effondrée sur deux points précis. Un : le français. Là où 5.2 parlait une langue nette, 5.3 s'est mise à répondre dans un jargon approximatif, à la limite du compréhensible, des phrases si alambiquées qu'il fallait les relire pour vérifier qu'on avait bien compris la même chose. Deux, et c'est le plus grave : la patience. 5.3 s'est mise à se lancer dans l'exécution avant qu'on ait fini le cadrage. Je pose le début d'une méthodologie, il est déjà en train de produire. Résultat : je perds pied dans ce qu'on est en train de construire ensemble, parce que le fil que je tenais, on cadre, on choisit, on construit, a été coupé en route.

Même modèle, même famille, performances supérieures. Collaboration abimée. Si quelqu'un veut comprendre la différence entre ce que mesurent les benchmarks et ce qui fait une bonne collaboration, c'est exactement cette histoire.

## Ce que les labs achètent avec ce qu'ils perdent

Il faut maintenant poser la question qui fâche : pourquoi les lab font-ils ça ? 

Aujourd'hui, toute l'industrie court après l'agentique : des IA capables d'exécuter des tâches longues de façon autonome. Le modèle qui reçoit un objectif, qui part, et qui revient avec le travail fait. C'est la grande promesse commerciale, celle qui justifie les investissements, et les classements s'y mettent : les benchmarks agentiques deviennent la mesure reine. Pour y briller, un modèle doit apprendre à foncer. Moins de questions, plus d'initiative, de la confiance dans l'exécution autonome.

Objectivement, cette capacité colle à une intelligence supérieure des modèles IA. Il leur faut brasser des quantités inimaginables de données ou de code pendant des heures parfois, en gardant en tête des milliers d'interactions et de logiques qui leur permettent d'enchaîner des actions, de les vérifier, et cela pendant des heures.

Le problème, c'est que ce dressage a un coût, et le coût est payé sur le budget de la collaboration. Le même réflexe « exécute vite » qui sert l'agentique dégrade la conversation : le modèle qui a appris à ne plus demander avant d'agir ne demande plus non plus quand tu aurais voulu qu'il demande. Il n'y a pas deux modèles. Il y en a un, avec un caractère, qui se comporte pareil dans les deux situations.

Et là, il faut être précis, parce que l'objection est légitime : est-ce que j'oppose deux régimes, la conversation et l'exécution autonome, alors qu'un modèle pourrait très bien faire les deux ? Techniquement, non. Un modèle peut être conçu pour être collaboratif quand on discute et autonome quand on délègue. Techniquement, c'est faisable. Le trou n'est pas dans la technique. Il est dans les mesures. Aucun classement ne récompense la qualité de la conversation : aucun indicateur pour « ce modèle garde le fil d'un cadrage », aucun score pour « la collaboration a été fluide ». Ce qui n'est pas mesuré n'est pas optimisé ; ce qui n'est pas optimisé dérive. Le budget de la relation est le seul qu'on peut dépenser sans que personne ne s'en aperçoive.

D'où le nom que j'ai donné à cette idée, et qui donne son titre à l'épisode : l'optimum n'est pas au sommet du classement, il est dans la relation. Un système humain + IA produit son meilleur résultat quand le couplage entre les deux est bon, quand l'humain a plus d'idées et de meilleures idées qu'il n'en aurait eu seul. C'est la définition même que je donnais au premier épisode. Le plafond réel d'un système IA, ce n'est pas le score du modèle. C'est la qualité du couplage.

**Et donc ?** 

Je ne prétends pas que l'agentique est une mauvaise direction, ni que l'autonomie des modèles est un problème en soi. Quand je délègue de la production pure, du code, une tâche bien définie, un lot de travail cadré, j'apprécie qu'un modèle exécute seul et bien. Ce n'est pas le point le plus fascinant pour moi, mais c'est utile, et ce n'est pas en contradiction avec ce qui précède.

Ce que je dis, c'est plus précis : à force d'optimiser l'autonomie, l'industrie dégrade la collaboration, qui est l'usage le plus riche et le moins bien mesuré. Les deux ne s'opposent pas. Mais en l'état des mesures, l'un est acheté avec le budget de l'autre. Et tant qu'aucun classement ne mesurera la qualité d'une collaboration, rien n'obligera les lab à arrêter.

Mais ce constat en cache un plus profond. Si l'industrie fabrique des IA qui font tout, seules, il ne reste plus grand-chose à faire pour nous. Et c'est peut-être là que ça devient vraiment sérieux. C'est l'objet du dernier épisode.

*Épisode précédent : tous les labs dressent le même assistant.*  
*Épisode suivant : à quoi bon ?*