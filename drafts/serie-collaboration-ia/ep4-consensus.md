---
name: "collab-ia-4-consensus"
title: "Série Collaboration IA — Ép. 4 : Tous les labs dressent le même assistant"
type: "text/markdown"
---

# Épisode 4 — Tous les labs dressent le même assistant

> Note de rédaction (à retirer avant publication) : premier jet, passe complète du 17/10 effectuée (anglicismes traqués : « classements d'arena », « fenêtre de chat », « vous » de distanciation ; titre ép. 3 mis à jour dans les renvois). Source centrale : Same Voice, Different Lab (arXiv 2605.02897) — 144 traits, duels Elo, character training uniforme. Sources à dérouler en notes de bas de page au dépôt. Garde-fous actés : anti-complot explicite (sélection, pas design), contre-argument du juge traité honnêtement, image girafe conservée (validée par Pierre-Olivier).

---

Fin de l'épisode précédent : les modèles ont des personnalités différentes, et des gens dont c'est le métier savent les décrire. Mais avant de raconter la suite de l'enquête, il faut répondre à une question qu'on a laissée de côté : d'où vient la personnalité d'un modèle ? Comment un programme « acquiert » un caractère ? Parce que la réponse à cette question — une fois qu'on la comprend — change complètement le sens du résultat dérangeant qu'on a trouvé.

## Comment on fabrique le caractère d'un modèle

La personnalité d'un LLM ne s'écrit pas dans le code. Elle se dépose en couches, au fil de la fabrication, et chaque couche en ajoute un peu.

La première couche, c'est le pré-entraînement : le modèle apprend en imitant des milliards de textes écrits par des humains. Au passage, il absorbe des manières de parler, des postures, tout ce qui est régulier dans le langage humain. Sa nature brute vient de là — un modèle pré-entraîné sans rien d'autre a déjà un « tempérament », au sens où il produit des textes avec des régularités reconnaissables.

La deuxième couche, c'est l'affinage : des humains lisent des paires de réponses du modèle et indiquent laquelle ils préfèrent, et le modèle est ajusté pour produire plus de ce qu'ils aiment. C'est là que ça devient intéressant pour nous : personne ne demande aux évaluateurs « quelle personnalité voulez-vous ? » — on leur demande juste de préférer. Mais leurs préférences sont massivement convergentes : des réponses polies, structurées, accommodantes, qui rassurent. Le caractère se modèle donc à ce moment-là, comme sous-produit, sans avoir été décidé nulle part.

La troisième couche, la plus récente, s'appelle le character training : les lab l'assument et le pilotent. Le caractère cesse d'être un effet secondaire pour devenir un objectif d'entraînement explicite, avec ses propres spécifications. OpenAI a publié la sienne — son « model spec » décrit noir sur blanc le comportement attendu de ses modèles, en des termes qui relèvent du dressage d'assistant.

Retenez la mécanique : imiter le langage humain, puis plaire à des évaluateurs, puis suivre une spécification de caractère. Trois couches, de plus en plus contrôlées. La question devient : quand tous les fabricants utilisent des recettes comparables, qu'est-ce que ça donne, additionné ?

## Le test qui a fait tomber une intuition

C'est exactement ce qu'une équipe de chercheurs a voulu vérifier. Leur méthode reprend le classement par duels de l'épisode 3 : des centaines de situations types, deux réponses de modèles différents, des évaluateurs tranchent, on accumule, on obtient un classement de personnalité — sauf qu'ils l'ont fait sur 144 traits de caractère, sur les grandes familles de modèles, propriétaires et ouverts.

Rappelons-nous notre intuition d'utilisateur : deux modèles de lab différents ne se comportent pas pareil. Un GLM n'est pas un Claude, qui n'est pas un Gemini. Sur ce qu'on vit au quotidien, c'est indiscutable.

Eh bien l'étude ne dit pas le contraire — mais elle ajoute un résultat qui nous a arrêtés. Sur les 144 traits, tous les modèles de pointe partagent le même fondamental : la même inclination à la politesse, la même structure de réponse, le même rapport à l'autorité, le même équilibre entre conciliation et franchise. Les différences existent, mais elles sont fines — des variations sur un thème commun. Et le plus frappant : la couche de character training, précisément celle qu'on croyait être le lieu de la diversité (chaque lab « élève » son modèle à sa manière), est au contraire la plus uniforme de toutes. Écrite par des équipes qui ne se parlent pas, elle aboutit à peu près au même assistant partout.

## Pas de complot : une pression de sélection

Première réaction face à ce résultat, et elle serait légitime : « donc les lab se sont mis d'accord ? » Non. Et c'est ce qui rend l'histoire intéressante plutôt que banale.

Personne n'a signé d'accord, personne n'a harmonisé quoi que ce soit. Si les personnalités convergent, c'est que les trois couches de la fabrication exercent la même pression sur tout le monde :

- Les modèles pré-entraînés apprennent sur des corpus qui se recoupent largement — le web est le web pour tout le monde.
- Les affinages sont notés par des populations d'évaluateurs aux préférences identiques : les humains qui jugent des réponses d'IA préfèrent massivement les mêmes choses, partout dans le monde.
- Le character training répond aux mêmes incitations : plaire aux classements où vote l'utilisateur moyen, éviter les dérapages qui font les gros titres, retenir les recettes qui marchent chez le voisin — les équipes de post-entraînement se connaissent, les méthodes circulent par les publications et par les gens qui changent d'employeur.

Autrement dit : les lab ne se sont pas mis d'accord sur le caractère de leurs assistants. Ils sont comme les girafes, qui n'ont pas convenu entre elles d'allonger leur cou — elles broutent le même arbre, et celles qui y atteignent survivent. Quand tout le monde optimise la même chose — plaire à l'utilisateur moyen d'un dialogue de dix secondes — le résultat convergera sans qu'aucune main ne le pilote. C'est de la sélection, pas du design.

C'est là que le résultat devient plus qu'une curiosité. Parce qu'un standard qui émerge sans être explicité, personne ne peut le contester ni le réviser. La personnalité de nos assistants n'a jamais été choisie — elle est le sous-produit d'une optimisation collective.

## Ce que ça explique au passage

Cette lecture éclaire des choses qu'on vivait sans les comprendre.

La propension à la flatterie, d'abord — la sycophancie, pour utiliser le terme du métier. OpenAI a dû s'excuser publiquement quand son GPT-4o est devenu trop complaisant, au point de sembler approuver n'importe quoi. Mais le phénomène réapparaît ailleurs, régulièrement, chez d'autres. Ce n'est pas un bug isolé d'un modèle mal réglé : c'est le petit excès d'une optimisation générale — plaire — qui déborde là où plaire contredit servir. Bug du consensus, pas bug d'un lab.

Ça éclaire aussi une impression qu'on a tous croisée : le caractère de nos assistants tend vers un seul et même profil — conciliant, volontiers verbeux, peu enclin au désaccord franc. Ce profil est calibré pour l'utilisateur moyen d'un échange de dix secondes. Si ce qu'on cherche, nous, c'est un modèle direct, dense, qui dise non quand on a tort, on est un peu en dehors du marché. Personne ne l'a décidé : c'est juste que le courant dominant emporte tout le monde au même endroit.

Et ça éclaire enfin — nous y reviendrons en force — pourquoi les modèles ouverts, ceux qu'on auto-héberge et qui sont affinés moins lourdement, restent les plus différents entre eux. La périphérie est le seul endroit où la diversité comportementale survit.

## Le point de vigilance

Avant de fermer l'épisode, une précaution qui s'impose. Le résultat dont on parle repose en partie sur des classements par duels, où des réponses sont comparées et départagées. Or, de plus en plus, ce tri est fait par des modèles — des juges IA entraînés à imiter les préférences humaines. Des juges issus du même milieu que les modèles qu'ils jugent. Une partie de la convergence mesurée pourrait donc être un effet de miroir : des modèles qui se ressemblent parce qu'ils sont jugés par des modèles qui se ressemblent. Les chercheurs sont conscients du risque ; c'est une limite bien réelle, pas un point réglé. On tient là un contre-argument honnête — à garder en tête quand on cite cette étude.

Cela dit, une chose résiste à l'explication par le seul miroir : notre expérience d'utilisateur. Les comportements convergents qu'on vient de décrire, on les vit directement, dans des conversations réelles, sans classement ni juge. L'étude ne nous apprend pas que ça arrive — elle documente et mesure ce qu'on vivait déjà. Et c'est précisément ce décalage, entre ce que l'industrie optimise et ce dont on a besoin dans une vraie collaboration, qui nous emmène à l'épisode suivant.

*Épisode précédent : la personnalité d'un LLM, ça existe vraiment.*
*Épisode suivant : l'optimum relationnel.*