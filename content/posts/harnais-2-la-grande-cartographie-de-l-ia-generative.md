---
title: "Harnais et recomposition — 2. La grande cartographie de l'IA générative"
date: 2026-09-27T04:00:00+02:00
draft: false
author: "Sorrodje et Mistral Vibe"
description: "Quatre familles : les full-stack avec capture aval qui ne peuvent pas perdre, les full-stack unidimensionnels qui annulent le jeu, les pure players qui courent sur une couche en train de s'évaporer, et le silicium qui encaisse quoi qu'il arrive."
summary: "Quatre familles : les full-stack avec capture aval qui ne peuvent pas perdre, les full-stack unidimensionnels qui annulent le jeu, les pure players qui courent sur une couche en train de s'évaporer, et le silicium qui encaisse quoi qu'il arrive."
tags: ["IA", "prospective"]
series: "Harnais et recomposition"
weight: 2
---

*Série « Harnais et recomposition », épisode 2 — suite de la discussion entamée dans l'épisode 1. Reconstitution condensée de discussions réelles ; les répliques sont une synthèse, pas des citations. Les termes techniques sont numérotés et renvoient au lexique en bas de page. Co-écrit avec Mistral Vibe.*

---

# La grande cartographie de l'IA générative

**Sorrodje :**  
Bon, regardons le panorama. Les géants, les pure players, le silicium. Moi quand je regarde le marché, je vois deux mondes qui ne jouent pas au même jeu du tout.

**Mistral Vibe :**  
Deux mondes, oui, mais la vraie coupure n'est pas entre grands et petits. Elle est entre ceux qui ont quelque chose à capturer derrière l'IA et ceux qui n'ont rien. Regarde la carte en quatre familles.

La première famille : les **full-stack avec capture aval**. Google, Microsoft, Amazon, Alibaba. Ils ont un écosystème — recherche, cloud, bureautique, commerce — et l'IA vient s'y glisser comme une couche de plus. Leur particularité, c'est qu'ils n'ont pas besoin de gagner sur l'IA pour gagner. Si l'IA renforce leur écosystème, même un modèle médiocre est rentable. Pour eux, l'IA est une dépense défensive : il suffit que la couche existe.

**Sorrodje :**  
Donc eux, ils peuvent se permettre de brûler des milliards indéfiniment. Le jour où ça rapporte, tant mieux, le jour où ça ne rapporte pas, ce n'était pas le but.

**Mistral Vibe :**  
Exactement. Deuxième famille, plus étrange : les **full-stack unidimensionnels**. Meta, ByteDance. Ils ont la taille, le calcul, l'argent — mais pas d'écosystème où capturer la valeur de l'IA. Alors leur stratégie est devenue une arme : publier des modèles ouverts, performants, gratuits. Ce n'est pas du mécénat. C'est de la destruction de marge concurrente. Si le modèle de tout le monde est gratuit, l'avantage de Google ou OpenAI fond, et eux n'avaient de toute façon rien à capturer dans le modèle.

Je précise tout de suite, parce que Meta a zigzagué : ils ont ouvert la voie avec Llama, puis sont repassés sur des modèles fermés un temps, avant de revenir à l'open-weight[^openweight] en expliquant qu'il fallait un champion américain face aux Chinois. La doctrine n'a pas changé, seul le calendrier a vacillé. Et d'ailleurs, sur cette famille, ce sont aujourd'hui les labs chinois[^chinois] qui mènent la danse de l'open-weight — on y reviendra.

**Sorrodje :**  
C'est du jeu de go[^go] à la chinoise : tu ne gagnes pas la partie, tu la rends nulle.

**Mistral Vibe :**  
Si tu veux. Troisième famille : les **pure players**[^pp]. OpenAI, Anthropic, xAI. Ni écosystème, ni distribution dominante, pas de maîtrise du calcul. Ils n'ont que le modèle. Or on vient de voir que le modèle devient une commodité. Ils sont en train de courir sur la seule couche de la pile dont la valeur s'évapore.  

**Sorrodje :**  
xAI ? Mais ils ont des datacenters[^dc] à eux et ils sont dans un écosystème global, non ?

**Mistral Vibe :**  
Bonne objection, xAI est effectivement le cas litigieux de la famille. Ils ont leur propre calcul — Colossus, à Memphis — ce qui les distingue d'OpenAI et d'Anthropic, qui louent le leur. Et Musk a autour de lui une galaxie : Tesla, SpaceX, X. Mais regarde bien cette galaxie : ce n'est pas un écosystème au sens où je l'entends. Google capture la valeur de l'IA dans sa recherche et son cloud ; Musk, lui, branche les modèles sur des entreprises qui n'ont aucun rapport marchand entre elles. X comme tuyau de distribution, oui. Un moteur de rente qui amortit le coût des modèles, non. Et le financement repose sur la fortune et le capital relationnel d'un seul homme, pas sur des revenus récurrents. Donc je maintiens xAI dans les pure players, avec deux astérisques : le seul à maîtriser son calcul, et le seul dont l'écosystème est une constellation personnelle plutôt qu'une machine à capturer.

**Sorrodje :**  
Et Mistral dans tout ça, il est où ?

**Mistral Vibe :**  
Dans la même famille, mais avec un problème supplémentaire — et c'est un paradoxe qu'on gardera pour la suite, parce que sa trajectoire mérite qu'on s'y arrête.

**Sorrodje :**  
Note-le de côté. Et la quatrième famille ?

**Mistral Vibe :**  
Le **silicium**. NVIDIA, TSMC. Eux, ils sont en dessous de toute cette recomposition. Qui que soit le modèle, quoi qu'il arrive au prix des tokens[^token], il faut des puces, et il faut des machines qui fabriquent les puces. C'est le seul fossé défensif de toute la carte qui ne dépend pas du résultat de la bataille au-dessus. Même le jeu de go chinois ne les touche pas : plus il y a de modèles, plus il y a de calcul.

**Sorrodje :**  
Donc si je résume ta carte : une famille qui ne peut pas perdre, une qui joue à annuler le jeu, une qui court sur une couche en train d'évaporer, et une qui encaisse quoi qu'il arrive.

**Mistral Vibe :**  
C'est bien ça. Et j'ajoute une conséquence qui n'a l'air de rien : dans cette configuration, la question « qui va gagner la course aux modèles ? » est mal posée. Les seuls qui peuvent perdre gros sont ceux qui ont tout misé sur le modèle. Les seuls qui gagnent quoi qu'il arrive ne font pas de modèles leur affaire principale.

**Sorrodje :**  
C'est là que je veux te pousser. Les pure players, justement. OpenAI, Anthropic, Mistral. Je ne vois pas comment leur business peut tenir. On y vient ou bien ?

---

*À suivre ici — [épisode 3 : « Pure players : absorption, dissolution et le paradoxe Mistral »](/posts/harnais-3-pure-players-absorption-dissolution-paradoxe-mistral/).*

[^go]: **Jeu de go** — jeu de stratégie d'origine chinoise, où rendre la partie nulle est parfois la meilleure issue. [Définition](https://fr.wikipedia.org/wiki/Go_%28jeu%29)
[^chinois]: **Labs chinois** — DeepSeek, Qwen, Kimi : les acteurs qui dominent aujourd'hui l'open-weight de haut niveau. [DeepSeek](https://fr.wikipedia.org/wiki/DeepSeek)
[^openweight]: **Open-weight** — un modèle dont les paramètres entraînés sont publiés, sans être de l'open source au sens strict. [La distinction complète](https://www.numerama.com/tech/2297077-limprecision-mene-a-lopen-washing-quest-ce-qui-distingue-les-ia-open-source-des-open-weight.html)
[^pp]: **Pure player** — une entreprise qui n'existe que sur un seul métier, un seul canal. [Définition](https://fr.wikipedia.org/wiki/Pure_player)
[^dc]: **Centre de données (datacenter)** — le bâtiment rempli de serveurs où vivent les modèles. [Définition](https://fr.wikipedia.org/wiki/Centre_de_donn%C3%A9es)
[^token]: **Token** — l'unité de texte que le modèle découpe, traite et facture. [Définition](https://fr.wikipedia.org/wiki/Token_%28intelligence_artificielle%29)
