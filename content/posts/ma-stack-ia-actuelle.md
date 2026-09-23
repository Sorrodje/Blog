---
title: "Ma stack IA actuelle"
date: 2026-09-23T00:00:00+02:00
draft: false
description: "Open WebUI, LiteLLM, Open Terminal, des hébergeurs EU : la stack auto-hébergée qui remplace Claude AI sans y perdre. Retour d'usage, pas tutoriel."
summary: "Open WebUI, LiteLLM, Open Terminal, des hébergeurs EU : la stack auto-hébergée qui remplace Claude AI sans y perdre. Retour d'usage, pas tutoriel."
tags: ["IA", "retour d'expérience"]
---

# Ma stack IA actuelle

## Bien…

Au moment où j'écris ces lignes, je m'ennuie comme un rat crevé. Pourquoi ?

Parce que chercher et trouver des solutions dans un univers neuf et aussi mouvant que l'IA est vraiment intéressant. Du coup pourquoi je m'ennuie, me direz-vous ?

Parce qu'il me semble avoir trouvé un sweet spot dans mon organisation de travail actuelle et dans la stack que je me suis construite. Ça ne s'est pas fait en un jour et ce n'est sûrement pas une solution universelle, mais elle correspond à un contexte et à des workflows de travail qui me sont propres. Pour autant, j'imagine que mon expérience peut vous servir, au moins partiellement.

## Contexte

Je bosse essentiellement avec l'IA pour construire des petites solutions logicielles dans des cas d'usage qui sont aujourd'hui peu, mal ou pas du tout couverts par la DSI dans mon environnement professionnel. Ayant un peu de compétence en admin sys et très peu en code, je m'assiste donc de l'IA pour analyser les cas d'usage, les données à ma disposition, l'expérience utilisateur recherchée, et architecturer une réponse adéquate. Disons que c'est du vibe coding structuré, où je fais un mix de product owner, d'architecte et de dev à la petite semaine.

Le tout, c'est que mon environnement de prod est contraint : des VM cloisonnées sans aucun accès au web, un poste de travail Windows sur lequel je ne suis pas admin, un proxy qui interdit l'usage d'API externes depuis un IDE. Tout cela est assez logique d'un point de vue sécurité, mais ça me complique l'existence.

S'ajoute à ça que mon contexte professionnel exige une véritable hygiène dans le traitement de données le plus souvent sensibles et soumises au RGPD.

Du coup, le travail dans Claude AI ou ChatGPT, c'était largement du shadow IA en zone grise, voire pire.

Donc, moralité : je devais adopter une organisation de taf propre.

## Point de départ

Si vous avez suivi [mon histoire](/posts/mon-histoire-ia-5-la-gs-en-loa-et-la-rampe-fcr/), vous savez que j'ai tout misé sur Anthropic avant de réaliser que ce n'était pas l'idée du siècle d'avoir tout mon travail dépendant d'un outil fourni par une boîte opaque avec des modèles propriétaires, tout mon contenu soumis au Cloud Act. D'où la recherche d'une alternative, que j'ai d'ailleurs bâtie avec Claude avant de le quitter — il y a une forme de gratitude là-dedans.

En outre, n'étant pas dev de métier, je maîtrise mal CLI et IDE, et je bâtis mes outils en mode conversationnel. Donc un chat s'imposait.

La base, ça a donc été de trouver une solution où j'ai un endroit stable où ranger mon travail en cours, où je maîtrise mes données, et dans lequel je peux changer de fournisseur IA tout en assurant la continuité de mon travail. Considérant que j'ai un serveur dédié pour divers petits trucs que je gère, l'option auto-hébergée est apparue naturelle, tout comme le choix d'Open WebUI.

## Open WebUI et LiteLLM : la strate conversationnelle et son backend

Honnêtement, je n'ai pas pris le temps de tester d'autres solutions comme LibreChat. On a testé Open WebUI et ça m'a convenu assez directement. Certes, c'est complexe à prendre en main du fait de la multiplicité des options et réglages, mais le fait est que ça fait parfaitement le job et que, compte tenu que c'est mon outil de travail, ça mérite un peu d'investissement personnel.

Dès l'installation, j'ai adjoint à Open WebUI un routeur auto-hébergé : LiteLLM. Concrètement, tout tourne en Docker sur mon serveur, en trois conteneurs : Open WebUI d'un côté, et de l'autre LiteLLM avec sa base de données dédiée (un Postgres). Chacun a sa base, chacun a ses données, et les conteneurs ne sont exposés qu'en local — c'est un Apache en frontal qui gère le SSL et l'accès depuis l'extérieur. La connexion entre Open WebUI et LiteLLM se fait via une clé API spécifique à laquelle on ne touche qu'une fois. Ça paraît complexe comme ça, mais en fait ça simplifie tout : Open WebUI, c'est l'UI ; LiteLLM, c'est le backend qui gère l'accès aux modèles et aux fournisseurs. Un seul point de configuration pour tous les modèles, les clés fournisseurs ne traînent pas dans l'interface, et si un fournisseur disparaît ou change de tarif, je change une entrée côté LiteLLM sans toucher au reste.

La séparation UI / routeur, c'est précisément ce qui rend la stack fournisseur-agnostique : l'outil de travail ne sait pas quel modèle il appelle, et le modèle ne sait pas dans quel outil il travaille.

Avec Open WebUI, on se retrouve avec un harnais complet et riche, comportant toutes les bases pour gérer ses projets sur plusieurs sessions : mémoire, knowledge bases, RAG, outils… Tout ça nécessite du taf à mettre en place, je ne vous le cache pas. On est très loin de Claude AI où on donne sa CB et tout fonctionne sans mettre les mains dans le cambouis.

## …ça marche quand même pas tout seul

Dans un premier temps, j'ai voulu reconstituer mes workflows Claude dans Open WebUI et j'avoue que ce n'est pas si facile, parce qu'on bute sur des agacements qui s'accumulent.

Déjà, il faut trouver fournisseurs et modèles. Dans mon cas, du EU only, donc, et on a vite fait le tour de la question quand on cherche des modèles compétitifs : Scaleway, TensorX, Nebius, Mistral… Nebius, c'est quand même un peu trop russe à mes yeux donc j'ai passé mon tour. J'ai gardé TensorX (des Irlandais) et regardé Scaleway de près — et là les emmerdements commencent. Pour avoir un modèle rapide, performant, pas trop cher et qui offre un prompt caching fonctionnel — pour ne pas payer plein pot les milliards de tokens d'input de mes conversations à rallonge — ça m'a pris un moment. C'est un sujet à lui tout seul, j'y consacrerai un billet dédié. [Mistral m'a finalement résolu le problème](/posts/le-retour-de-mistral/) d'ailleurs.

Mais au-delà de ça, le fonctionnement du harnais lui-même n'est pas similaire à Claude. Les knowledge bases d'Open WebUI fonctionnent pas mal, mais on comprend vite que Claude utilise en plus un environnement interne où il a du contexte, des fichiers, des outils à disposition. On les voit à peine quand on n'y prête pas attention, mais quand on passe sur autre chose, on s'aperçoit que c'est un peu le cœur du réacteur du harnais autour du LLM. Donc j'ai un peu galéré. Open WebUI offre un environnement d'exécution de code pour que le modèle exécute ses propres scripts, et c'est Pyodide — du Python recompilé pour tourner dans le navigateur, en WebAssembly. Pas de vraies bibliothèques, pas d'accès système, pas de persistance : ça peut dépanner pour triturer un CSV, mais comme environnement de dev, on repassera.

Puis la solution est venue avec Open Terminal.

## Open Terminal : la couche agentique d'Open WebUI

Ça s'installe comme le reste, via un conteneur Docker dédié qui fonctionne de pair avec celui d'Open WebUI. Et là, le harnais devient complet : une vraie sandbox dans laquelle le modèle peut agir, coder, tester, échouer, recommencer — bref, du full agentique.

On a un accès complet à cet espace, via un explorateur de fichiers et un terminal web. Le point qui m'a frappé au départ : cet espace est un vrai dossier sur la machine qui héberge Open WebUI. Le modèle en a une vision interne, depuis l'intérieur du conteneur ; moi, j'en ai une vision réelle, depuis l'environnement natif du serveur. Le décalage est troublant les premières fois, mais c'est exactement ce qu'il faut : un espace de travail que le modèle et moi regardons depuis nos deux bouts, sans que rien ne sorte de la machine.

Du coup, on récupère un harnais absolument complet : mémoire, ressources documentaires sous forme de knowledge bases, une batterie d'outils à disposition du modèle, et une sandbox de développement transparente.

En tout et pour tout, j'ai donc un environnement IA performant, fournisseur-agnostique, dans lequel j'ai une totale maîtrise de mes données, et où je peux utiliser des IA 100 % hébergées en Union européenne. Que demande le peuple ?