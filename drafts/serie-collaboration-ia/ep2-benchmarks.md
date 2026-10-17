---
name: "collab-ia-2-benchmarks"
title: "Série Collaboration IA — Ép. 2 : Ce qu'un benchmark ne dira jamais de ton assistant"
type: "text/markdown"
---

# Épisode 2 — Ce qu'un benchmark ne dira jamais de ton assistant

> Note de rédaction (à retirer avant publication) : premier jet, épisode le plus « matière sourcée » de la série. Sources à dérouler en notes de bas de page au moment du dépôt. Chiffres à re-vérifier à la publication (saturation = sujet mouvant, leçon du billet Mistral dépublié). Garde-fou de posture : on explique ce qu'on a appris ensemble, pas ce que Mistral Vibe sait et Sorrodje ignore — la voix reste celle de l'épisode 1.

---

Dans l'épisode précédent, je racontais ma perplexité face aux benchmarks : des scores, des acronymes, et aucun rapport visible avec ce que j'attendais d'un assistant. Depuis, Mistral Vibe et moi avons creusé la question. Ce qu'on a trouvé est plus simple et plus gênant que prévu : les benchmarks ne sont pas mauvais — ils mesurent juste ce que presque plus personne n'a besoin de savoir.

## Un benchmark, c'est quoi, concrètement

Commençons par leur rendre justice. Un benchmark, c'est une collection de questions avec des réponses vérifiables. MMLU, le plus célèbre : des milliers de QCM académiques, de la médecine au droit. GSM8K : des problèmes de maths de niveau collège. GPQA : des questions de niveau doctoral en sciences. Un modèle passe le test, on compte les points, on publie le pourcentage.

C'est solide, reproductible, comparable — et c'est exactement pour ça que le marché s'y accroche. Quand un lab sort un modèle, la release note ouvre sur le tableau de scores. Quand on choisit un modèle, on regarde le classement. C'est la monnaie commune de l'industrie.

Sauf que cette monnaie ne départage plus personne.

## Tout le monde a le même niveau

Voici le fait le plus important qu'on ait trouvé, et le moins commenté : sur les tests classiques, les grands modèles ne se distinguent plus. MMLU, qui départageait les modèles il y a trois ans, est aujourd'hui réussi à 88-94 % par *tous* les modèles de pointe. Une différence de deux points, c'est du bruit de mesure — le même modèle relancé deux fois peut varier d'autant. GSM8K, les maths de collège ? Tout le monde est vers 99 %. GPQA, le test de niveau doctoral qui devait tenir des années ? Les meilleurs modèles dépassent 90 %, deux ans à peine après sa création.

L'AI Index de Stanford, la référence annuelle du domaine, l'a mesuré noir sur blanc : près de la moitié des soixante benchmarks les plus cités sont aujourd'hui « saturés » — c'est-à-dire que les meilleurs modèles s'y regroupent si près du plafond que les écarts ne veulent plus rien dire. Leur formule est plus parlante que tout : « des évaluations censées rester difficiles pendant des années sont saturées en quelques mois ».

Traduit en usage réel : demander « quel est le modèle le plus intelligent » n'a plus de réponse, parce que la question n'est plus séparable. Ils le sont tous, à peu près, pour ce que les tests mesurent. Le classement dit qui est dans le club, pas qui est le meilleur.

## Pourquoi ça sature aussi vite

La mécanique est simple à comprendre. Un benchmark à réponse vérifiable — un QCM, un théorème, un cas de test de code — est facile à cibler lors de l'entraînement. Parfois volontairement : les données d'entraînement sont opaques, et on ne sait jamais tout à fait si le modèle a appris à raisonner ou à reconnaître la question. Parfois involontairement, par contamination : le test devient assez connu pour se retrouver dans les données. Dans les deux cas, le score monte sans que rien d'autre change.

Les chercheurs réagissent en fabriquant des tests plus durs, construits pour ne pas saturer — Humanity's Last Exam, des questions d'experts ; ARC-AGI, des énigmes visuelles que les modèles ratent lamentablement ; FrontierMath, des problèmes de maths de niveau recherche. Ils font leur travail : ils départagent toujours. Mais remarquez le glissement : ce sont des mesures de capacité *extrême*, sur des tâches que 99,9 % des utilisateurs ne feront jamais. Le classement continue d'exister — il parle juste de moins en moins de nous.

## Ce que le score ne dit pas : un exemple

Prenons un test réel, rapporté par une utilisatrice qui a passé la même question à neuf modèles : un dilemme de carrière, une vraie question sans bonne réponse. Deux modèles de la même famille, niveau de benchmark équivalent :

Le premier a répondu en 19 mots. Juste assez pour être entendu. Le second a répondu en 367 mots — et surtout, sans qu'on lui demande, il a rédigé un email au recruteur pour demander un délai, et conclu : « envoie ça ».

Aucun des deux n'est « meilleur ». Ce sont deux conceptions opposées de ce dont la personne avait besoin : l'un écoute, l'autre agit. Selon votre usage, l'un des deux est parfait et l'autre est un cauchemar. Et aucun benchmark au monde ne départage cette différence — parce qu'elle n'est pas une différence de capacité. Les deux savent écrire un email. Les deux savent être brefs. Ce qui diffère, c'est leur *comportement* : ce qu'ils choisissent de faire, spontanément, avec la même question.

C'est là que mon intuition de béotien rejoint la littérature : des chercheurs ont montré que pour beaucoup d'utilisateurs, le caractère d'un assistant — sa manière de se comporter — pèse plus dans la préférence que les gains de capacité brute. Les benchmarks mesurent le savoir-faire. Ce qui fait la différence dans une conversation réelle, c'est le savoir-être. Et ça, rien ne le mesure.

## Le trou dans le classement

Reformulons donc ce qu'on a appris :

- Les benchmarks classiques ne départagent plus les grands modèles — la capacité s'est uniformisée.
- Les benchmarks modernes départagent toujours, mais sur des tâches extrêmes sans rapport avec l'usage courant.
- Et le comportement — verbeux ou dense, direct ou précautionneux, exécutant ou partenaire — n'est mesuré nulle part dans aucun des deux.

Ça ne veut pas dire que les scores sont inutiles. Ils filtrent : un modèle à 60 % là où les autres sont à 90 % a de vraies lacunes. Mais entre deux modèles du même plateau, le classement ne vous dira rien de ce qui déterminera votre expérience : est-ce qu'il me laisse cadrer avant d'exécuter ? Est-ce qu'il me dit non quand j'ai tort ? Est-ce qu'il me noie sous la longueur pour compenser le doute ?

Ces questions-là ont des réponses. Simplement, elles sont ailleurs que dans les scores. Et il se trouve qu'on peut les étudier sérieusement — c'est l'objet de l'épisode suivant : la personnalité d'un LLM, ça existe, ça se mesure, et ça varie entre les modèles plus qu'on ne croît.

*Épisode précédent : j'ai appris à travailler avec l'IA avant de savoir ce qu'elle valait.*
*Épisode suivant : la personnalité d'un LLM, ça existe et ça se mesure.*