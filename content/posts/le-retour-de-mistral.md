---
title: "Le retour de Mistral"
date: 2026-09-23T00:00:00+02:00
draft: false
description: "Après la bascule vers l'auto-hébergement racontée dans « Mon histoire IA », je gardais un œil sur le Chat Mistral. Entre un Medium 3.5 calamiteux, l'hébergement de GLM 5.2 dans l'UE et une clé API qui passe là où on ne l'attendait pas, retour sur un mois de retournement complet."
summary: "Après la bascule vers l'auto-hébergement racontée dans « Mon histoire IA », je gardais un œil sur le Chat Mistral. Entre un Medium 3.5 calamiteux, l'hébergement de GLM 5.2 dans l'UE et une clé API qui passe là où on ne l'attendait pas, retour sur un mois de retournement complet."
tags: ["IA", "retour d'expérience"]
---

# Le retour de Mistral

*(Suite directe de la série « Mon histoire IA » — à lire après [La GS en LOA et la rampe FCR](/posts/mon-histoire-ia-5-la-gs-en-loa-et-la-rampe-fcr/).)*

Outre OpenWebUI et Claude AI, j'ai toujours gardé un œil sur le Chat Mistral pour voir ce qu'on pouvait en tirer. J'avais même réussi un temps à me faire rembourser l'abonnement annuel par le taf, donc ça ne me coûtait pas cher. Et puis je me voyais mal préconiser au travail l'usage d'une IA externe américaine ou chinoise, soumise au Cloud Act ou à toute autre surveillance potentielle par les services de sécurité des pays concernés.

Mistral, donc.

## Le Chat

Au début, il y avait le Chat, le choix entre Mistral Large, Medium et Small, et ma foi ça marchait pas si mal — même si on restait loin du compte par rapport à Claude AI. J'arrivais à y traiter certaines tâches, à l'utiliser en usage général. J'ai d'ailleurs toujours trouvé que leur harnais était très correct, avec en particulier une très bonne gestion par projet et une mémoire supra conversationnelle assez convaincante, dont Claude ne disposait pas alors.

Ceci dit, Claude s'améliorant et les modèles d'Anthropic se révélant bien plus performants pour mon usage, mon utilisation de Mistral est restée fort erratique.

## Puis le Chat devint Vibe

Outre le fait que je préférais le nom le Chat à Vibe, la distinction entre deux modes — Chat et Work — en plus de l'interface de code, la disparition de Large 3 au profit de Medium 3.5 ont, dans mon expérience du moins, rendu l'expérience Mistral Web à la fois confuse et inefficace. Je n'ai jamais vraiment compris lequel des deux modes il fallait utiliser, tant ils paraissaient similaires. J'ai donc alterné, testant ici ou là, activant et désactivant la mémoire, les bibliothèques et autres options du harnais. J'ai vraiment poussé l'expérience en essayant de construire des solutions simples pour mon travail, pour invariablement buter sur les mêmes problèmes avec Mistral Medium 3.5 : contexte perdu au bout de N itérations d'un chat, consignes système oubliées très rapidement, code halluciné, traitement des données douteux, logorrhée inutile blindée de listes à puces et de phrases en gras, etc.

Bref, un désastre — qui commençait à sérieusement me faire douter de pouvoir l'utiliser dans mon job.

Pendant ce temps, je mettais en place ma stack OpenWebUI, LiteLLM et OpenTerminal, et j'étais donc en pleine recherche d'un fournisseur d'API IA serverless compétent, grâce auquel je pourrais congédier Claude AI sans que ça me coûte deux fois le prix de l'abonnement Max. J'ai tourné et retourné entre Scaleway et TensorX pour trouver un modèle où le prompt caching fonctionne suffisamment correctement. Je me stabilise sur MiniMax M3 et GLM 5.2, servis disons correctement chez TensorX. Scaleway avait bien un Qwen compétent, mais sans prompt caching implémenté, la facture s'est avérée salée…

## Le coup de théâtre

Début août, Mistral héberge GLM 5.2… wow. Là, c'est du modèle compétent. D'autant qu'avec mon abonnement Mistral Pro, j'ai 25 € de crédit API Studio offerts. Je mets donc en test immédiat… prompt caching KO, balises de raisonnement cassées… bref, ça a demandé un peu de travail pour configurer les choses proprement, afin que GLM 5.2 fonctionne fluidement et sans consommer des brassées de tokens. Avec 25 balles de crédit offert et une hygiène de travail stricte pour économiser la conso, je partais tranquillou pour travailler pepouze avec GLM pour 100–150 € par mois. Acceptable, pour un outil puissant auto-hébergé alimenté par une IA de pointe hébergée dans l'UE.

Du coup, j'en profite pour recreuser l'usage de Vibe Web, puisque mon contexte pro ne me permet pas d'utiliser Vibe CLI. Expérience toujours aussi dégueu : Medium toujours aussi incompétent, mémoire inexistante en mode Work. Ça partait mal — jusqu'à ce que je découvre la possibilité de créer dans Studio un agent basé sur GLM 5.2, qu'on peut rendre disponible dans Vibe Chat sans que la conso impacte le budget API. Franchement, ça a bien marché ; mais vu le harnais en mousse, ça ne m'a pas poussé à abandonner mon OpenWebUI…

## Quand les étoiles s'alignent

Courant septembre, pour une raison que j'ai oubliée, je dégaine vite fait Vibe pour une question générale sur mon téléphone. Même Medium fait le job pour ça. Sauf qu'en l'occurrence, le modèle répond sans listes à puces interminables ni autres tics agaçants du modèle Mistral. Je tique. En creusant un peu avec des prompts plus complexes, sur des jobs que je fais habituellement avec GLM 5.2 dans OpenWebUI, j'ai un comportement ultra-similaire dans Vibe Work. Donc Mistral a branché GLM dans son chat web !

Par contre, c'est pas stable : GLM disparaît souvent pour céder la place à Medium 3.5. C'est pas bien compliqué de repérer la différence. Mais même avec un GLM intermittent, j'ai enfin pu bosser sérieusement avec Vibe. Alléluia !

## La cerise sur le gâteau

Après quelques jours, ça se stabilise au niveau modèle, mais les mises à jour s'enchaînent dans l'interface de Vibe — genre plusieurs par jour. On sent que la team Mistral envoie du gros en backstage, et les améliorations UI/UX tombent. On se croirait dans une version alpha d'Ubuntu. Mais le gros, le très gros truc, c'est la livraison de la nouvelle mémoire dans Work : les apprentissages. Là, franchement, c'est une dinguerie. Ils ont livré un mix de mémoire et de sandbox interne où le modèle gère pour l'utilisateur la mémoire contextuelle, les fils rouges des projets et les documents associés. Un genre de super mémoire qui fait base de connaissances en plus et sur lequel on a en plus la vision et la main pour vérifier et modifier.

Le mix GLM 5.2, qui manipule les outils et les skills comme un magicien, et les apprentissages se combinent pour transformer Vibe en outil ultra-puissant !

## La cerise sur la cerise sur le gâteau

Pendant ce temps, en farfouillant les menus, je tombe sur les quotas d'usage, la gestion de l'abonnement et tout le monitoring standard — d'ailleurs bien amélioré au passage. Je vois le quota API Studio de 25 € que je connais, et celui de l'API Vibe, à 255 €, sur lequel je lorgne en sachant que je ne peux l'utiliser que dans Vibe CLI ou les extensions Mistral officielles, pas dans OpenWebUI. Je creuse un peu et je vois quand même que je peux copier la clé API en question dans Vibe Code. Quitte à en avoir le cœur net, je crée un profil Mistral Vibe dans LiteLLM et un modèle associé. Je teste la connexion sans trop d'espoir… putain, ça passe. Je teste une session de travail dans OpenWebUI et ça marche nickel : prompt caching avec un taux de hit de 92 %, et la conso s'impute sur le quota de la clé Vibe.

Wow. Là, je réalise que Mistral m'offre, pour mes 20 balles TTC d'abonnement, un harnais Web de premier plan avec un modèle de pointe en utilisation quasi illimitée, plus 280 € de crédits API pour utiliser leurs modèles dans OpenWebUI ou tout autre outil de mon choix…

## La touche finale

Je suis quasi sûr que Mistral utilise dorénavant GLM 5.3 dans Vibe Work depuis quelques jours.

Si ça c'est pas du très, très beau cadeau : merci Mistral ! Là, j'attends la livraison de la prochaine mise à jour de Vibe avec la nouvelle interface Web, et je vous en reparle :)
