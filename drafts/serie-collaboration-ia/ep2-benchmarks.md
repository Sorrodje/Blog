---
name: "collab-ia-2-benchmarks"
title: "Série Collaboration IA — Ép. 2 : Ce qu'un benchmark ne dira jamais de ton assistant"
type: "text/markdown"
---

# Épisode 2 — Ce qu'un benchmark ne dira jamais de ton assistant

> Note de rédaction (à retirer avant publication) : deuxième réécriture (17 oct, passe « gabarit trame ») — phrases construites sur le gabarit de la trame de Pierre-Olivier, règles dures appliquées : pas de triade d'adjectifs, pas de chaîne de tirets (une apposition max, sinon deux points ou deux phrases), pas de marqueur d'annonce (« Traduit en usage réel », « Résumons ce qu'on a appris » remplacés par du récit), verbes et agents d'abord. Sources à dérouler en notes de bas de page au moment du dépôt. Chiffres à re-vérifier à la publication (saturation = sujet mouvant). Anecdote des 9 modèles anonymisée, à trancher.

---

Dans l'épisode précédent, je racontais ma perplexité face aux benchmarks : des scores, des acronymes, et aucun rapport visible avec ce que j'attendais d'un assistant. Depuis, on a creusé la question avec Mistral Vibe. Ce qu'on a trouvé est plus simple et plus gênant que prévu : les benchmarks ne sont pas mauvais. Ils mesurent juste ce que presque plus personne n'a besoin de savoir.

## Un benchmark, c'est quoi, concrètement

Commençons par leur rendre justice. Un benchmark, c'est une collection de questions avec des réponses vérifiables. MMLU, le plus célèbre : des milliers de QCM académiques, de la médecine au droit. GSM8K : des problèmes de maths de niveau collège. GPQA : des questions de niveau doctoral en sciences. Un modèle passe le test, on compte les points, on publie le pourcentage.

C'est solide et comparable, et c'est exactement pour ça que le marché s'y accroche. Quand un lab sort un modèle, la note de version commence par le tableau de scores. Quand on choisit un modèle, on regarde le classement. C'est le mètre-étalon commun de l'industrie.

Sauf que cette mesure ne départage plus personne.

## Tout le monde a le même niveau

Voici le fait le plus important qu'on ait trouvé, et le moins commenté : sur les tests classiques, les grands modèles ne se distinguent plus. MMLU, qui départageait les modèles il y a trois ans, est aujourd'hui réussi à 88-94 % par tous les modèles de pointe. Une différence de deux points, c'est du bruit : le même modèle relancé deux fois peut varier d'autant. GSM8K, les maths de collège ? Tout le monde est vers 99 %. GPQA, le test de niveau doctoral qui devait tenir des années ? Les meilleurs modèles dépassent 90 %, deux ans à peine après sa création.

L'AI Index de Stanford fait référence chaque année sur ces questions. Elle l'a mesuré noir sur blanc : près de la moitié des soixante benchmarks les plus cités sont aujourd'hui « saturés ». Autrement dit, les meilleurs modèles s'y regroupent si près du plafond que les écarts ne veulent plus rien dire. Leur formule est plus parlante que tout : « des évaluations censées rester difficiles pendant des années sont saturées en quelques mois ».

En vrai, demander quel est le modèle le plus intelligent n'a plus de réponse. Ils le sont tous, à peu près, pour ce que les tests mesurent. Le classement dit qui est dans le club, pas qui est le meilleur.

Et le mouvement s'est accéléré, je l'ai vécu de l'intérieur. En mai, pour travailler sérieusement, il fallait un Claude Sonnet ou Opus. En juin, Gemini m'est devenu utilisable. En juillet, Minimax M3 ou Qwen 97B-A17B l'étaient aussi. Aujourd'hui, j'ai entre quinze et vingt options avec lesquelles je ne perçois quasiment plus de différence de performance pure. En six mois, le club est passé de trois membres à une vingtaine.

Or, pendant ce temps, mon besoin, lui, n'a pas bougé. J'ai grosso modo les mêmes usages, la même approche, et surtout le même besoin d'une interaction productive entre l'IA et moi. Les modèles sont devenus plus intelligents ; ce que j'attends d'eux, lui, n'a pas changé d'un iota. Et voilà le point de tout ce papier : parmi ces quinze ou vingt modèles utilisables, tous ne me sont pas aussi agréables ni aussi productifs. Pourquoi j'adore travailler avec Mistral Large 4 et GLM 5.2, et pourquoi GLM 5.3 est devenu désagréable ? Aucun benchmark ne répond à cette question. C'est elle qui va nous occuper.

## Pourquoi ça sature aussi vite

La mécanique est simple à comprendre. Un benchmark à réponse vérifiable, qu'il s'agisse d'un QCM, d'un théorème ou d'un cas de test de code, est facile à cibler lors de l'entraînement. Parfois volontairement : les données d'entraînement sont opaques, et on ne sait jamais tout à fait si le modèle a appris à raisonner ou à reconnaître la question. Parfois involontairement, par contamination : le test devient assez connu pour se retrouver dans les données. Dans les deux cas, le score monte sans que rien d'autre change.

Les chercheurs réagissent en fabriquant des tests plus durs, construits pour ne pas saturer. Humanity's Last Exam, des questions d'experts. ARC-AGI, des énigmes visuelles que les modèles ratent lamentablement. FrontierMath, des problèmes de maths de niveau recherche. Ils font leur travail : ils départagent toujours. Mais il y a un glissement. Ces tests mesurent des capacités extrêmes, sur des tâches que 99,9 % d'entre nous ne feront jamais. Le classement continue d'exister, il parle juste de moins en moins de nous.

## Ce que le score ne dit pas : un exemple

Prenons un test réel. Une utilisatrice a passé la même question à neuf modèles : un dilemme de carrière, une vraie question sans bonne réponse. Deux modèles de la même famille, niveau de benchmark équivalent.

Le premier a répondu en 19 mots. Juste assez pour être entendu. Le second a répondu en 367 mots, et surtout, sans qu'on lui demande, il a rédigé un email au recruteur pour demander un délai, avant de conclure : « envoie ça ».

Aucun des deux n'est « meilleur ». L'un écoute, l'autre agit. Selon l'usage qu'on en fait, l'un des deux est parfait et l'autre est un cauchemar. Et aucun benchmark au monde ne départage cette différence, parce qu'elle n'est pas une différence de capacité. Les deux savent écrire un email. Les deux savent être brefs. Ce qui diffère, c'est leur comportement : ce qu'ils choisissent de faire, spontanément, avec la même question.

Mon intuition de béotien rejoint ici ce qu'ont montré des chercheurs : pour beaucoup d'utilisateurs, le caractère d'un assistant pèse plus dans la préférence que les gains de capacité brute. Les benchmarks mesurent le savoir-faire. Ce qui fait la différence dans une vraie discussion, c'est le savoir-être. Et ça, rien ne le mesure.

## Le trou dans le classement

Résumons ce qu'on a appris. Les benchmarks classiques ne départagent plus les grands modèles : la capacité s'est uniformisée. Les benchmarks modernes départagent toujours, mais sur des tâches extrêmes sans rapport avec l'usage courant. Et le comportement, qu'il soit verbeux ou dense, direct ou précautionneux, exécutant ou partenaire, n'est mesuré nulle part dans aucun des deux.

Ça ne veut pas dire que les scores sont inutiles. Ils filtrent : un modèle à 60 % là où les autres sont à 90 % a de vraies lacunes. Mais entre deux modèles du même plateau, le classement ne dira rien de ce qui déterminera notre expérience. Est-ce qu'il me laisse cadrer avant d'exécuter ? Est-ce qu'il me dit non quand j'ai tort ? Est-ce qu'il me noie sous la longueur pour compenser le doute ?

Ces questions ont des réponses. Elles sont juste ailleurs que dans les scores. Et il se trouve que ce savoir-être, d'autres que nous le prennent au sérieux, des gens dont c'est le métier. C'est l'objet de l'épisode suivant.

*Épisode précédent : j'ai appris à travailler avec l'IA avant de savoir ce qu'elle valait.*  
*Épisode suivant : la personnalité d'un LLM, ça existe vraiment.*