---
title: "Mon histoire IA — 5. La GS en LOA et la rampe FCR"
date: 2026-09-20T00:00:00+02:00
draft: false
description: "Cinquième et dernier billet de la série. Le quatrième s'arrêtait sur les ruines : l'outil sur lequel reposait mon activité, viré d'une décision."
summary: "Cinquième et dernier billet de la série. Le quatrième s'arrêtait sur les ruines : l'outil sur lequel reposait mon activité, viré d'une décision."
tags: ["IA", "retour d'expérience"]
series: "Mon histoire IA"
weight: 5
---

## Un mois de taf

Ça m'a pris un mois de revoir de fond en comble mes méthodes, pour me construire un environnement sur lequel j'ai la main. J'auto-héberge ma propre solution de chatbot — Open WebUI, open source. Toutes mes données sont sur mon propre serveur, et j'y branche le modèle IA que je veux, quand je veux.

## La GS en LOA

Pour ceux qui n'ont pas la référence moto : un truc comme ChatGPT ou Claude, c'est une R1300GS en LOA. Tu ne te préoccupes de rien — châssis, moteur, accessoires, options, le tout pour un loyer fixe. Et c'est cent fois trop puissant pour ce que tu en fais. En plus, dans le cas des IA, le loyer est ridiculement bas par rapport au coût réel — on a vu au billet trois pourquoi ils font ça.

Se monter soi-même un chatbot sur lequel on a le contrôle, c'est la démarche inverse : monter le châssis, y insérer le moteur, faire soi-même le réglage de sa rampe FCR ou de sa carto d'injection, régler l'assiette et le comportement dynamique, tout le tintouin. Je vous garantis que c'est du taf.

Mébon. J'ai maintenant une vraie situation saine : mon travail ne dépend de personne, mes données et mes traitements IA sont sous législation européenne, conformes au RGPD, et je peux changer de moteur d'une minute à l'autre.

## Changer de moteur, justement

Les modèles avec lesquels je bosse sont chinois — GLM, DeepSeek, MiniMax — mais hébergés et mis en œuvre chez des hébergeurs européens, en Union Européenne. Donc sans que les sbires de Trump ni ceux de Xi Jinping viennent mettre la patte sur mes données.

C'est possible parce que ces modèles sont ce qu'on appelle « open weight » : les labos les publient en accès libre, n'importe qui peut les télécharger — sur Hugging Face précisément — et les mettre en œuvre sans dépendre de qui que ce soit. Ni du gouvernement américain, ni du chinois, ni même des labos qui les créent. Si je veux bosser dans un contexte qui respecte les lois européennes, je prends un abonnement chez un hébergeur européen qui met à disposition les modèles open weight les plus performants — donc, aujourd'hui, des chinois.

Ce qui me fait un peu plaisir, c'est qu'à mon petit niveau, je fais exactement le même chemin que les grands opérateurs comme Microsoft, qui dans Copilot utilise des moteurs de tous les fournisseurs selon les cas, les régions et les usages — et qui a commencé à mettre en œuvre ses propres modèles, plus petits et plus économiques que les SUV géants.

Pourquoi les modèles chinois sont si économes, d'ailleurs ? Parce qu'ils reposent massivement sur une architecture dite « MOE » — mixture of experts. Un modèle classique, dit dense, mobilise tous ses paramètres à chaque question — qu'on lui demande de l'astrophysique ou de calculer deux plus deux, il sort le datacenter. Les modèles spécialisés, eux, sont petits : quelques milliards de paramètres, le sweet spot du rapport performance/coût étant vers sept ou huit milliards. Le MOE, c'est un gros modèle avec d'énormes quantités de connaissances embarquées, mais qui fonctionne comme une équipe de dizaines de petits modèles spécialisés qui s'activent ou non selon la nature de la question. Il mobilise quatre entités de trente milliards plutôt que les 2500 d'un coup. Ne me demandez pas comment ça s'ajuste par contre — j'en sais rien, j'ai compris le principe général, et ça me suffit largement.

## Comme les moteurs à explosion

Aujourd'hui, dans mon chatbot, j'utilise trois ou quatre modèles différents sans même remarquer que j'en ai changé. Des modèles peu onéreux, aux performances à vue de nez équivalentes à celles de Claude quand j'ai débuté, quelques mois plus tôt.

J'ai de plus en plus l'impression qu'on avance vite et sûrement vers une normalisation : les modèles vont finir par une taille et un fonctionnement qui collent à la réalité de leurs usages. Assez probablement, on s'en foutra totalement d'où vient le modèle et qui l'a fait. La seule chose qui comptera, c'est sa mise en œuvre, l'endroit précis où il est hébergé, et le contexte technique et institutionnel qui va avec. J'ai même l'intuition qu'on aura très peu de modèles disponibles. Que ça va se standardiser, comme les moteurs à explosion.

## L'essentiel n'est pas le moteur

Et voilà le truc que cette histoire m'a appris en dernier, alors qu'il crève les yeux. Ce qui compte dans l'utilisabilité d'un chatbot, ce n'est pas la puissance brute du moteur — l'usage moyen est de toute façon très en dessous des possibilités théoriques des modèles. C'est tout ce qu'il y a autour : les instructions système qui donnent son comportement au modèle — une ingénierie en soi —, les outils qu'il peut utiliser, son espace de travail interne, la mémoire où il apprend vos préférences et habitudes, le traitement des PDF et des fichiers bureautiques. Pour moi, c'est presque l'essentiel.

Après, tous les besoins ne se valent pas. Certains justifient des environnements ultra sécurisés, gérés en interne — pensez aux traitements qui induisent des décisions sur la vie des gens, la Sécu par exemple. D'autres se suffisent d'un hébergement sécurisé chez un prestataire, sous la bonne législation. Et pour les trucs où il n'y a rien de sensible, une offre cloud chez tel ou tel labo fait très bien l'affaire — tant qu'on n'y met rien dont on a à cœur de garder la maîtrise.

## Épilogue

Quelques mois après avoir tapé ma première commande à une IA, sans y croire vraiment : je bosse sur des modèles que personne ne contrôle à ma place, mes données sont en Europe, je change de moteur quand je veux. Et je questionne au minimum trois IA différentes sur tout sujet à enjeu — parce qu'elles ne sont pas neutres, ces machins. Entraînées par des humains, sur des données humaines, dans des contextes humains. Sur le code et la science dure, ça passe. Sur tout le reste, on croise les sources.

Ce qui me reste de toute cette histoire, tenez-vous bien : le moteur s'est échangé contre du vent. Ceux qui comptaient — le cadre, la méthode, la mémoire de ce que je construis, la main sur mes données — c'est tout ce qui reste quand on change de moteur du jour au lendemain.

Quant à ce qu'on construit autour des moteurs, et pourquoi c'est là que se joue la suite — c'est un autre sujet. Pour un autre billet.