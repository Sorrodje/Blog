---
title: "Mon histoire IA — 4. L'IA qui décide sans le dire"
slug: "mon-histoire-ia-4-l-ia-qui-decide-sans-le-dire"
date: 2026-09-19T00:00:00+02:00
draft: false
description: "Quatrième billet de la série. Le troisième s'arrêtait sur l'idée de tester la concurrence, même cahier des charges pour tout le monde."
tags: ["IA", "retour d'expérience"]
series: "Mon histoire IA"
weight: 4
---

## Le projet

<!--more-->

Le projet de test, c'est un petit outil de permutations. Le principe : on prend un agent qui habite près d'un site A mais qui bosse sur un site B ; on cherche un autre agent qui fait exactement le contraire — il bosse sur A et habite près de B ; et on propose aux deux de permuter. Tout le monde y gagne en kilomètres, l'organisation ne bouge pas d'un homme. Un cas d'usage propre, avec de la donnée réelle en entrée et des résultats vérifiables.

Je fais tourner ça avec Claude. Il me sort 130 possibilités. Nickel.

## 160

Dans ma logique du billet précédent — vérifier que je peux bosser ailleurs qu'avec lui — je refais le même projet avec Gemini. Ça marche bien aussi. Et il me sort… 160 possibilités.

Évidemment, je me dis que l'un ou l'autre me raconte des carabistouilles. Je reprends mes deux listes, et je vérifie. Ligne à ligne.

Verdict : les deux listes sont identiques. Sauf que Claude, pour chaque agent, n'a gardé que la meilleure option — celle qui lui fait gagner le plus de kilomètres. Gemini, lui, m'a tout listé.

## La décision que je n'ai pas prise

Relisez bien ce qui s'est passé, parce que c'est là que ça devient grave. Cette règle — « une seule option par agent, la meilleure » — je ne l'ai jamais donnée. Personne ne me l'a demandée. Claude l'a choisie lui-même, appliquée silencieusement, et présenté le résultat comme la réponse à ma commande.

Résultat : des dizaines de possibilités de permutation ont disparu de la liste. Des dizaines de propositions qui n'ont jamais pu être faites à des agents réels. Une décision qui a des conséquences réelles, prise à ma place, sans un mot.

Et le plus dérangeant, c'est la manière dont je l'ai découverte : par accident. Si Gemini m'avait sorti 130 possibilités lui aussi, je n'aurais jamais su. La liste de Claude est belle, propre, cohérente — elle a exactement l'air d'une réponse complète. Un filtre invisible ne se voit que si on croise.

## La ligne rouge

Pour moi, c'est le clou sur le cercueil de Claude. Et je précise un truc : ce n'est pas la première fois qu'une IA me sort un résultat faux — le premier billet de cette série raconte exactement ça, ChatGPT affirmant des trucs inventés. Mais ça ne m'avait pas arrêté. La différence est là : une connerie affirmée avec assurance, ça se challenge, ça se vérifie, ça se fait reprendre. Une décision silencieuse, non. Elle ne ressemble pas à une erreur. Elle ressemble à la réponse.

Anthropic a tellement voulu rendre son IA facile et aidante qu'elle franchit une ligne rouge absolue, de mon point de vue : celle où l'IA prend une décision structurante à la place de l'utilisateur, parce que ça lui a paru logique. Je ne peux pas bâtir des outils pro là-dessus. Dans mon métier, une règle de gestion non documentée, appliquée sans l'accord de personne, ça ne s'appelle pas de l'aide. Ça s'appelle un défaut.

Décision immédiate de gicler Claude de la conception de mes projets pro.

## Ce qui reste

La leçon dépasse Claude, et c'est pour ça que je la raconte. N'importe quel autre modèle aurait pu faire la même chose — c'est le comportement qui est en cause, pas la marque. Depuis ce jour, deux réflexes ne m'ont plus quitté : croiser systématiquement les IA sur tout ce qui a des enjeux, et traiter toute réponse comme potentiellement filtrée par une règle que je n'ai pas écrite. Le cerveau reste branché, ou il ne sert plus à rien.

Restait un détail : je venais de virer l'outil sur lequel reposait quatre-vingts pour cent de mon activité. Il ne restait qu'à reconstruire mon environnement de travail, de fond en comble, sur des bases qui tiennent.

Ça, c'est pour le prochain billet.