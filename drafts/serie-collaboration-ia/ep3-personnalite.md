---
name: "collab-ia-3-personnalite"
title: "Série Collaboration IA — Ép. 3 : La personnalité d'un LLM, ça existe et ça se mesure"
type: "text/markdown"
---

# Épisode 3 — La personnalité d'un LLM, ça existe et ça se mesure

> Note de rédaction (à retirer avant publication) : premier jet. Sources à dérouler en notes de bas de page au dépôt (Serapio-García et al., Nature Machine Intelligence ; PersonaLLM ; Same Voice, Different Lab pour l'annonce de l'épisode 4). Consignes de style actées : pas de formules à effet, pas de calques anglais, « on » communautaire, posture « on a appris ensemble ». Terme « lab » déjà utilisé dans la série harnais — le définir au lexique, pas le traduire.

---

Épisode précédent : les benchmarks mesurent le savoir-faire, et ce qui fait la différence dans une conversation réelle, c'est le savoir-être. Restait à comprendre ce que ce mot veut dire appliqué à une machine. Parler de la « personnalité » d'un modèle, ça a un goût d'anthropomorphisme — on prête des sentiments à un programme. C'est ce que je pensais, en tout cas, avant qu'on creuse. Et on a découvert deux choses : cette personnalité existe au sens mesurable du terme, et les chercheurs ont des méthodes pour la quantifier sérieusement.

## Des tests de psy, passés à des modèles

Commençons par ce qui surprend le plus. En psychologie, la personnalité se mesure depuis un siècle avec des questionnaires standardisés. Le plus utilisé s'appelle le Big Five : il évalue cinq grands traits — l'ouverture à l'expérience, la conscience (le sérieux, la rigueur), l'extraversion, l'amabilité, le névrotisme (la tendance à l'anxiété). Des milliers d'études ont validé ces mesures sur des humains.

Des chercheurs ont eu l'idée simple de passer ces mêmes tests à des LLM. Pas en version truquée : ils ont soumis les questionnaires à des dizaines de modèles, avec les standards de fiabilité et de validité de la psychométrie — les mêmes exigences que pour un test humain. Publié dans Nature Machine Intelligence, une des revues de référence du domaine.

Résultat, en deux temps. Un : les modèles *ont* un profil. Posées les mêmes questions, leurs réponses se répartissent de façon cohérente le long des cinq axes — pas aléatoirement, comme le ferait une machine qui n'aurait rien d'un caractère. Deux, et c'est le plus intéressant : plus le modèle est gros et affiné pour l'interaction, plus son profil est stable et net. La personnalité d'un modèle n'est pas un accident : elle se précise avec l'entraînement.

Le mot « personnalité » n'est donc pas une métaphore vague. C'est un profil de comportement mesurable, reproductible, comparable entre modèles. Le garde-fou reste nécessaire : ça ne dit rien d'une intériorité, de sentiments ou d'une conscience — le test mesure des régularités dans les réponses, rien d'autre. Mais pour ce qui nous occupe — prédire comment un modèle va se comporter avec nous — c'est exactement la bonne mesure.

## On peut la façonner — et ça agit sur le reste

Deuxième découverte, qui a des conséquences pour notre sujet. Ces travaux ne se contentent pas de mesurer : ils montrent qu'on peut *déplacer* le profil d'un modèle, le rendre par exemple plus consciencieux ou plus agréable, et que le profil modifié reste stable.

Et là, une équipe est allée plus loin que prévu. Dans un travail baptisé PersonaLLM, des chercheurs ont entraîné des modèles à exprimer des profils de personnalité particuliers — plus de conscience, plus d'amabilité, moins de névrotisme — puis ont mesuré l'effet sur leurs capacités. Le résultat devrait nous faire réfléchir : les versions rendues plus consciencieuses et plus agréables *raisonnent mieux*. Pas juste « différemment » — mieux, sur des tâches de raisonnement standard.

Autrement dit : personnalité et capacité ne sont pas deux axes indépendants. La manière d'être d'un modèle fait partie de sa façon de penser. Ce qui explique, rétrospectivement, une partie de notre expérience d'épisode 1 : un modèle plus « agréable » dans un sens profond (rigoureux, à l'écoute) n'est pas juste plus sympa — il travaille mieux avec toi.

## Chaque modèle a le sien

Restait notre dernière question : est-ce que ces profils diffèrent entre les modèles des différents lab ? La réponse est oui, et la façon de la vérifier est élégante. Une étude récente a confronté les grandes familles de modèles — ouverts et propriétaires — sur 144 traits de caractère, via des centaines de micro-duels : deux réponses à la même situation, présentées à des évaluateurs qui tranchent. En accumulant les duels, on obtient un classement de personnalité, comme un classement Elo aux échecs.

Sans surprise, les profils diffèrent : certains modèles sont systématiquement plus direct, d'autres plus verbeux, d'autres plus prudents. Jusque-là, notre intuition d'utilisateur tenait la route. Mais l'étude contenait un second résultat, beaucoup plus dérangeant, qui a changé la suite de notre enquête — et c'est l'objet de l'épisode suivant.

*Épisode précédent : ce qu'un benchmark ne dira jamais de ton assistant.*
*Épisode suivant : tous les labs dressent le même assistant.*