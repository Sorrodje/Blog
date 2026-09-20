---
title: "À propos"
description: "Comment ce blog est fait : l'infra, la méthode de travail, et pourquoi ça ressemble à ça."
date: 2026-09-13T00:00:00+02:00
draft: false
---

Quelques mots sur la mécanique, puisque c'est aussi le sujet de ce blog : comment et pourquoi ça tourne derrière.

## L'infra

Une seule machine, un serveur Kimsufi. Pas de Docker, pas de base de données, pas de PHP : c'est un choix, pas un exploit. Le site est **100 % statique**, généré par Hugo à partir de simples fichiers Markdown. Apache sert le résultat directement, le certificat HTTPS vient de Let's Encrypt via Certbot, le domaine vit chez Gandi. Tout ça tient dans ce qu'on sait réparer soi-même — pas de brique dont je ne comprends pas le fonctionnement.

## L'identité

Un fond froid, un accent **cuivre**, la police Ubuntu auto-hébergée — quatre fichiers WOFF2 qui dorment sur le serveur, pas de CDN tiers. Le thème est Congo, un thème Hugo modifié avec parcimonie, pour ne pas le casser à la prochaine mise à jour.

## La méthode

L'édition et le build se font dans un espace de travail dédié ; la mise en ligne tient en deux commandes : `hugo` pour générer le site, puis `rsync` pour le copier vers le serveur. Un flux reproductible sans réfléchir. Et si un jour ce blog s'arrête, rien n'est otage : le contenu vit dans des fichiers `.md` exploitables ailleurs.

## La collaboration

Les billets comme le site lui-même sont toujours le produit d'une collaboration avec des IA — dans Mistral Vibe, Deepseek, Gemini, et dans **Open WebUI**, mon harnais open source auto-hébergé sur le Kimsufi. Rien d'automatique : la plume, les choix et le regard restent humains, les IA servent d'appui et de vérification. C'est aussi, à sa façon, un exemple concret de ce que ce blog raconte — la série « Mon histoire IA » raconte comment j'en suis arrivé là, et pourquoi je tiens à garder la main.

## Les stats

Le site utilise **Matomo**, auto-hébergé sur le même Kimsufi que ce blog. Pas de Matomo Cloud, pas de profilage tiers : tout reste sur ma machine, je suis le seul à voir les chiffres. Ils ne valent pas le détour, mais ils sont à moi. Les adresses IP sont anonymisées après 24 heures, aucun cookie publicitaire, aucune donnée partagée. C'est mon outil, pas celui d'un annonceur.

## Pourquoi comme ça

Le même fil conducteur que le premier billet : *light is right*. Un site qui consomme peu pour exister peut durer sans rien peser. Léger à charger, léger à héberger, léger à maintenir. Cohérent avec ce que je défends par ailleurs — inutile de prôner la sobriété avec un site qui pèse trois mégaoctets et quatre-vingt-dix scripts de tracking. Le tout, toujours, hébergé et géré en Europe.