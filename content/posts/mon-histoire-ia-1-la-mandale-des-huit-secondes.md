---
title: "Mon histoire IA — 1. La mandale des huit secondes"
date: 2026-09-16T00:00:00+02:00
draft: false
description: "Il y a quelques mois, je n'avais jamais causé à une IA de ma vie. Aujourd'hui, développer des solutions avec des IA occupe l'essentiel de mon activité professionnelle. Cette série raconte comment on passe de l'un à l'autre en quelques mois."
tags: ["IA", "retour d'expérience"]
series: "Mon histoire IA"
weight: 1
---

## Le besoin

Tout commence dans mon club de VTT. La com et l'organisation passent par Facebook depuis des années — moi qui déteste ce truc et tous les réseaux sociaux, je supporte. Plus récemment, un groupe WhatsApp est venu s'ajouter pour annoncer les entraînements officiels, et je suppose que le bureau et les coaches en utilisent un autre pour s'organiser entre eux. Bref : c'est devenu un peu le bordel pour savoir quoi surveiller, et tout le monde est à peu près d'accord sur le sujet.

<!--more-->

J'en touche un mot à un collègue de club qui siège au bureau, en lui disant que ça serait pas mal d'améliorer ça. Bingo : c'est pile poil en projet. Ils regardent les outils existants, ils consultent des développeurs pour un outil spécifique, tout ça. Je propose de le fournir de manière bénévole, j'aurais quelques idées et quelques compétences pour ça. Re Bingo : ça les intéresse.

J'avais dans l'idée d'utiliser un outil collaboratif de la famille Teams ou Google, mais open source : Nextcloud. Une plateforme solide, très utilisée, avec un développement vivant. Je creuse la question, j'en installe une instance sur mon serveur, je fais quelques tests plus un peu de customisation esthétique pour lui donner une identité club. Je présente ça au comité directeur : ils sont vraiment preneurs. On acte des comptes pour vingt-cinq personnes et un groupe de travail pour tester comment organiser les agendas, gérer les entraînements, etc.

## Le vrai projet

En attendant, je creuse de mon côté. Je teste, je reteste. Des trucs fonctionnent bien, d'autres pas trop mal, d'autres dégueulassement. Il va falloir trier, prendre des décisions d'organisation selon les possibilités techniques, ou des décisions techniques selon les choix d'organisation. Bref, ça commence à ressembler à un vrai projet d'implémentation d'applicatif, comme dans un contexte pro. Ceux qui connaissent le sujet savent que les brainstorms sur ce genre de projet se transforment vite en labyrinthe, et qu'il faut être méthodique. Je suis pas trop mauvais à ce jeu-là. Mais j'ai mes limites.

Je commence en effet à buter sur des problèmes techniques qui réclameraient du développement. Genre : automatiser la surveillance des renouvellements de licences et d'adhésions, pour vérifier qui a raqué ou pas en fin d'année. Et là, j'ai un problème de taille — je n'ai aucune connaissance en code. Zéro. Une lumière clignote au fond de mon crâne : et si c'était l'occasion de tester ce que savent faire ces fameuses IA ? Je googlise, et effectivement, leur capacité à produire, auditer et réparer du code commence à être notoire.

## Huit secondes

Go ChatGPT, version gratuite. Je lui file ce que je cherche à faire. Nextcloud étant totalement open source, tout le code et la documentation sont disponibles en ligne — donc accessibles à ChatGPT. Mon nouvel ami gratte, enthousiaste, un script en Python — le langage courant pour ce genre de truc — et me fait même un guide pas à pas en PDF pour l'installer.

En huit secondes.

Première mandale dans ma gueule. Le truc que je ne sais pas faire, que je n'apprendrai jamais faute de temps, gratté en huit secondes avec le mode d'emploi qui va avec.

Je passe au test sur mon serveur. Je suis le pas-à-pas, en commettant au passage toutes les erreurs possibles de débutant : il m'a fallu une heure pour mettre en place ce qu'il a gratté en huit secondes. Résultat : ça marche pas. On continue le chat pour essayer de réparer. Ça marche toujours pas. Et ChatGPT commence à s'embourber — il refait encore et encore les mêmes erreurs, en affirmant des choses fausses, carrément inventées ou extrapolées. Le tout en me causant comme un ado de quatorze ans. Bref, ça me saoule, et bye ChatGPT.

## Mais quand même

Huit secondes, quand même. Le signe était là, énorme : un outil capable de produire en quelques secondes ce qui me bloque depuis des semaines. Le problème n'était pas la capacité, c'était l'expérience — les réponses fausses affirmées avec assurance, le ton, l'embourbement. Je repense à un concurrent dont j'ai entendu parler, le chat d'une autre boîte, qu'on m'a décrit comme capable de causer à un adulte et de creuser un cahier des charges avant de foncer. Ça, c'est pour le prochain billet.