---
name: "collab-ia-3-personnalite"
title: "Série Collaboration IA — Ép. 3 : La personnalité d'un LLM, ça existe vraiment"
type: "text/markdown"
---

# Épisode 3 — La personnalité d'un LLM, ça existe vraiment

> Note de rédaction (à retirer avant publication) : réécriture complète lors de la passe du 17/10 — titre changé (« ça se mesure » → « ça existe vraiment ») pour éviter la lecture « méthode d'évaluation » ; la thèse de la série est la contradiction, pas une méthode. Sources à dérouler en notes de bas de page au dépôt (Serapio-García et al., Nature Machine Intelligence ; PersonaLLM ; Same Voice, Different Lab pour l'annonce de l'épisode 4). Consignes actées : pas de formules à effet, pas de calques anglais, « on » communautaire, posture « on a appris ensemble », pas de leçon universitaire.

---

Épisode précédent : les benchmarks mesurent le savoir-faire, et ce qui fait la différence dans une vraie discussion, c'est le savoir-être. Restait le mot qui fâche. Parler de la personnalité d'un modèle, j'ai longtemps cru que c'était de l'anthropomorphisme — la tentation de prêter des sentiments à une machine. Puis, en creusant pour cette série, on est tombés sur des travaux qui changent la donne. Pas parce qu'ils disent que les modèles ont une âme — ils ne disent rien de ce genre. Parce que ce que je vivais sans les mots pour le dire, d'autres l'ont étudié avec des méthodes sérieuses. Voilà ce qu'on y a trouvé.

## Des tests de psy, passés à des machines

En psychologie, on mesure la personnalité depuis un siècle avec des questionnaires standardisés. Le plus courant, le Big Five, évalue cinq grands traits : l'ouverture à l'expérience, la conscience (le sérieux, la rigueur), l'extraversion, l'amabilité, le névrotisme (la tendance à l'inquiétude). Ces tests sont loin d'être parfaits — on en reparlera —, mais des décennies d'études en ont fait un outillage solide pour décrire les humains.

Des chercheurs ont eu l'idée de les faire passer à des LLM. Pas en gadget : questionnaires complets, dizaines de modèles, et les mêmes précautions de méthode que pour des humains — parce qu'un test bâclé ne veut rien dire. Le tout publié dans une grande revue à comité de lecture, pas sur un blog.

Surprise : les modèles ont un profil. Posées les mêmes questions, leurs réponses se répartissent de façon cohérente le long des cinq axes — pas au hasard, comme le ferait un programme sans caractère. Et le détail qui nous a le plus éclairés : plus un modèle est gros et affiné pour la discussion, plus son profil est net et stable. Sa personnalité n'est pas un accident de fabrication : elle se précise avec l'entraînement.

Un mot d'honnêteté, parce qu'il le faut : ces tests ne mesurent ni sentiments, ni conscience, ni intériorité — seulement des régularités dans les réponses. Mais pour nous, c'est l'essentiel : le mot « personnalité » n'est pas une métaphore lâchée. C'est un vrai objet, descriptible, comparable d'un modèle à l'autre. Ce qu'on sent confusément en discutant avec un assistant — ce « caractère » qui fait qu'on préfère l'un à l'autre — existe aussi au sens où la science l'entend.

## La vraie surprise : le caractère fait partie de la capacité

Autre travail, autre découverte — et celle-là, on ne l'attendait pas. Une équipe a entraîné des modèles pour qu'ils expriment des profils de personnalité précis : plus consciencieux, plus agréables, moins inquiets. Puis elle a mesuré l'effet sur le reste. Résultat : les versions rendues plus consciencieuses et plus agréables raisonnent mieux. Pas juste « autrement » — mieux, sur des exercices de raisonnement standard.

Autrement dit : la manière d'être d'un modèle fait partie de sa manière de penser. Les deux ne sont pas des axes indépendants qu'on réglerait séparément. Ça explique, rétrospectivement, quelque chose qu'on vivait sans le comprendre dès l'épisode 1 : un modèle « agréable » au sens profond — rigoureux, à l'écoute — n'est pas juste plus sympa. Il travaille mieux.

## Alors, tous différents ?

Restait la question du début : ces profils, est-ce qu'ils diffèrent entre les modèles des différents lab ? Une étude récente a fait l'effort : 144 traits de caractère, les grandes familles de modèles — ouverts et propriétaires —, et des centaines de micro-duels : deux réponses à la même situation, des évaluateurs tranchent, on cumule, et ça donne un classement de personnalité, façon classement Elo aux échecs.

La réponse est oui : les profils diffèrent. Certains modèles sont plus directs, d'autres plus verbeux, d'autres plus prudents. Jusque-là, notre intuition d'utilisateur tenait la route. Mais l'étude cachait un second résultat, beaucoup plus dérangeant — celui qui a changé la suite de notre enquête. C'est l'épisode suivant.

*Épisode précédent : ce qu'un benchmark ne dira jamais de ton assistant.*
*Épisode suivant : tous les labs dressent le même assistant.*
