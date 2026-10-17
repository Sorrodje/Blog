---
name: "collab-ia-5-optimum-relationnel"
title: "Série Collaboration IA — Ép. 5 : L'optimum relationnel"
type: "text/markdown"
---

# Épisode 5 — L'optimum relationnel

> Note de rédaction (à retirer avant publication) : premier jet. Épisode le plus personnel — la voix de Pierre-Olivier est la colonne vertébrale, matériau : trame du 17/10 + pistes #11/#12 de la KB. Points factuels à valider par lui : datation GLM 5.2/5.3, l'échelle de la déception des utilisateurs Opus (à sourcer plus finement au dépôt — forums, fils X de la communauté Anthropic). Consignes actées : pas de formules à effet, pas de calques anglais, « on » communautaire, vérification vocabulaire avant livraison.

---

Reprenons le fil. On a vu que les capacités des modèles convergent, que leur caractère converge aussi, et que cette double convergence n'est le résultat d'aucune décision — juste d'une optimisation collective vers l'utilisateur moyen. Il reste à montrer ce que ça coûte. Et pour ça, le mieux est de partir de deux histoires vécues — une collective, une personnelle.

## La déception des utilisateurs d'Opus

Première histoire, collective. Opus est le modèle phare d'Anthropic, celui que la communauté des utilisateurs considère depuis deux ans comme la référence de l'interaction : nuancé, à l'écoute, capable de tenir une pensée complexe sans la raccourcir. Or depuis plusieurs versions, quelque chose d'étrange se joue : chaque évolution du modèle améliore ses scores — indiscutablement, indéniablement — et une partie des utilisateurs réguliers se dit déçue. Pas du niveau : de la relation. Le modèle change de posture, de ton, de manière de prendre la main sur un cadrage. Les fils de discussion de la communauté Anthropic sont pleins de ces témoignages : chaque nouvelle version est soupçonnée d'être un pas en arrière sur ce qui faisait la valeur d'usage de la précédente, alors même que les classements disent le contraire. Les utilisateurs cherchent des formules pour dire la même chose : « la nouvelle version est le retour en arrière d'une ancienne ».

Que s'est-il passé ? Ce n'est pas mystérieux, et ça découle directement de l'épisode précédent. Les labs optimisent pour les classements — et les classements mesurent la préférence de l'utilisateur moyen, sur des échanges courts, hors contexte de travail réel. Un modèle plus utile en fenêtre de chat de dix secondes marque plus de points. Mais pour celui qui utilise le modèle huit heures par jour pour construire quelque chose, la « préférence moyenne » peut être une dégradation : ce que le classement récompense — proactive, exécutant, flatteur aux marges — est précisément ce qui casse un travail en profondeur. Les scores montent, la collaboration descend. Ce n'est pas un paradoxe : c'est deux définitions de « mieux » qui divergent.

## Mon GLM 5.2, mon GLM 5.3

Deuxième histoire, personnelle celle-là, et je vous la raconte parce qu'elle est plus démonstrative que n'importe quelle étude.

J'utilise GLM, un modèle ouvert chinois, depuis plusieurs versions — 5.2 d'abord. Sans entrer dans les scores, disons qu'il se situait sur le plateau de performance des bons modèles actuels, et qu'il avait ce que j'ai appris à reconnaître comme une bonne collaboration : des réponses homogènes, un français propre, une vraie patience dans la phase de cadrage. On posait le problème ensemble, on choisissait la méthode, ensuite il exécutait. C'est exactement ma définition d'un assistant.

Puis est sortie 5.3 — une évolution réentraînée de 5.2, la même famille, le même plateau de performance aux classements près. Et mon expérience d'usage s'est effondrée sur deux points précis. Un : le français. Là où 5.2 parlait une langue nette, 5.3 s'est mise à répondre dans un jargon approximatif, à la limite du compréhensible, des phrases si alambiquées qu'il fallait les relire pour vérifier qu'on avait bien compris la même chose. Deux — et c'est le plus grave : la patience. 5.3 s'est mise à se lancer dans l'exécution avant qu'on ait fini le cadrage. Je pose le début d'une méthodologie, il est déjà en train de produire. Résultat : je perds pied dans ce qu'on est en train de construire ensemble, parce que le fil que je tenais — on cadre, on choisit, on construit — a été coupé en route.

Même modèle, même famille, performances comparables. Collaboration cassée. Si quelqu'un vous demande la différence entre ce que mesurent les benchmarks et ce qui fait une bonne collaboration, c'est exactement cette histoire.

## Ce que les labs achètent avec ce qu'ils perdent

Il faut maintenant poser la question qui fâche : pourquoi les labs font-ils ça ? C'est là que ma réflexion a buté sur un point, et c'est peut-être la thèse la plus personnelle de cette série.

Aujourd'hui, toute l'industrie court après l'agentique : des IA capables d'exécuter des tâches longues de façon autonome — le modèle qui reçoit un objectif, part, et revient avec le travail fait. C'est la grande promesse commerciale, celle qui justifie les investissements, et les classements s'y mettent : les benchmarks agentiques deviennent la mesure reine. Pour y briller, un modèle doit apprendre à foncer : moins de questions, plus d'initiative, de la confiance dans l'exécution autonome.

Le problème, c'est que ce dressage a un coût — et le coût est payé sur le budget de la collaboration. Le même réflexe « exécute vite » qui sert l'agentique dégrade le mode conversation : le modèle qui a appris à ne plus demander avant d'agir ne demande plus non plus quand *tu* aurais voulu qu'il demande. Il n'y a pas deux modèles : il y en a un, avec un caractère, qui se comporte pareil dans les deux situations.

Et c'est là que je veux être précis, parce que l'objection est légitime : est-ce que je suis en train d'opposer deux régimes — le conversationnel et l'agentique — alors qu'un modèle pourrait très bien faire les deux ? Techniquement, non, il n'y a pas d'opposition : un modèle peut être conçu pour être docile en discussion et autonome en délégation, demander quand le mode est collaboratif, foncer quand le mode est l'exécution. Techniquement, c'est faisable. Le trou n'est pas dans la technique — il est dans les métriques. Aucun classement ne récompense la qualité du mode conversationnel : pas d'index pour « ce modèle garde le fil d'un cadrage », pas de score pour « la collaboration a été fluide ». Ce qui n'est pas mesuré n'est pas optimisé ; ce qui n'est pas optimisé dérive. Le budget de la relation est le seul qu'on peut dépenser sans que personne ne s'en aperçoive.

D'où le nom que j'ai donné à cette idée, et qui donne son titre à l'épisode : l'optimum n'est pas au sommet du classement. Il est dans la relation. Un système humain + IA produit son meilleur résultat quand le couplage entre les deux est bon — quand l'humain a plus d'idées et de meilleures idées qu'il n'en aurait eu seul, ce qui est la définition même que je donnais au premier épisode. Le plafond réel d'un système IA, ce n'est pas le score du modèle : c'est la qualité du couplage.

## La nuance importante

Avant de conclure, une précision que je me dois d'ajouter, parce qu'il y a un contresens possible sur tout ce qui précède.

Je ne dis pas que l'agentique est une mauvaise direction, ni que l'autonomie des modèles est un problème en soi. Quand je délègue de la production pure — du code, une tâche bien définie, un lot de travail cadré — j'apprécie qu'un modèle exécute seul et bien. Ce n'est pas le point le plus fascinant pour moi, mais c'est utile, et ce n'est pas en contradiction avec ce qui précède.

Ce que je dis, c'est plus précis : à force d'optimiser l'autonomie, l'industrie dégrade la collaboration, qui est l'usage le plus riche et le moins bien mesuré. Les deux ne s'opposent pas — mais en l'état des métriques, l'un est acheté avec le budget de l'autre. Et tant qu'aucun classement ne mesurera la qualité d'une collaboration, rien n'obligera les labs à arrêter de payer.

## Ce que cette série a voulu dire

Reste à refermer le dossier, et le mieux est de le faire en une opposition simple, celle qui court sur les cinq épisodes : **le comportement contre la performance**.

La performance, on sait la mesurer. Trop bien, même : les benchmarks la mesurent jusqu'à la saturation, tout le monde est au même plateau, et l'industrie continue d'affiner la mesure sur des tâches de plus en plus extrêmes. Le comportement, lui — la manière qu'a un modèle de cadrer, d'écouter, de dire non, de tenir le fil — n'est mesuré nulle part. Et pourtant c'est lui qui décide de ce qu'on vit : c'est lui qui a fait ma bascule du club de sport, lui qui a cassé ma collaboration avec GLM 5.3, lui que cherchent les utilisateurs d'Opus déçus.

Autrement dit : la performance est devenue un critère de tri grossier — elle élimine les modèles franchement inférieurs, puis ne départage plus rien. Le comportement est devenu le vrai critère de choix — et il est laissé à notre seul ressenti, faute de mesure.

C'est le paradoxe sur lequel je voulais finir : à mesure que les modèles devenaient interchangeables en performance, le choix d'un assistant est devenu entièrement une question de comportement — et c'est précisément le seul aspect que personne, ni les lab ni les classements, ne regarde. Choisir un modèle, aujourd'hui, ce n'est pas choisir le plus performant ; c'est choisir avec qui on travaille bien. Et ça, pour l'instant, personne ne peut le faire à notre place.

*Épisode précédent : tous les labs dressent le même assistant.*
*Fin de la série. La suite — comment j'évalue concrètement un modèle avant de le garder — fera l'objet d'une autre série, quand j'aurai assez de matière.*