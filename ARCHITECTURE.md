# ARCHITECTURE — Blog sorrodje.alter-it.org

**Projet :** blog personnel Hugo, retours d'expérience terrain sur l'usage de l'IA.
**URL :** https://sorrodje.alter-it.org
**Emplacement du code :** basculé sur **Mistral Vibe** au **21/09/2026**. L'arbre de dev `Blog perso/hugo/` n'est plus l'espace de travail actif ; il a été archivé dans `Blog perso/hugo-archive-20260921.tar.gz` puis supprimé de la sandbox. La version à jour vit sur GitHub.
**Date de dernière révision :** 2026-09-21. Ajouté au dépôt le 20/09/2026, mis en cohérence avec le pipeline GitHub Actions. **Ce document vit dans ce dépôt : le mettre à jour au fil des changements d'architecture, dans le même commit que le changement quand c'est possible.**

---

### Signatures d'auteur (23/09/2026)

Chaque billet porte un champ `author` dans son front matter (`Sorrodje` par défaut, `Mistral Vibe` sur les billets majoritairement écrits par l'IA). Le rendu se fait dans la ligne de métadonnées via les overrides `layouts/_partials/article-meta.html` et `layouts/_partials/meta/author.html` (Congo ne gère pas l'auteur par article nativement).

## 1. Vue d'ensemble

| Point | Valeur |
|---|---|
| Générateur | Hugo extended v0.165.0 (requis pour SCSS/SASS) |
| Thème | Congo (jpanther/congo), cloné en mode « theme simple » dans `themes/` |
| Hébergement | Kimsufi, Apache natif, DocumentRoot `/var/www/sorrodje.alter-it.org/` |
| HTTPS | Let's Encrypt via Certbot |
| Stack | 100 % statique — pas de Docker, pas de BDD, pas de PHP |
| Recherche | Fuse.js côté client (thème Congo), index `public/index.json` |
| Statistiques | Matomo auto-hébergé (sous-domaine `matomo.alter-it.org`, site id 2) |

### Flux de publication (courant — depuis le 20/09/2026)

```
push sur main du dépôt GitHub Sorrodje/Blog
   →  GitHub Actions : build Hugo extended (même version que la CI), --minify
   →  rsync vers /var/www/sorrodje.alter-it.org/ sur le Kimsufi
```

**Le dépôt GitHub `main` est la source de vérité.** Plus aucun build manuel côté Kimsufi, plus de `rsync` lancé à la main. Le workspace local du Kimsufi (`~/blog`) n'est plus la référence : `git pull` réflexe avant toute modif locale.

**Règle de fiabilité :** tout commit est validé par un build Hugo local (même version que la CI, ex. v0.166.0 extended) avant push — suite à une série d'échecs CI le 20/09/2026.

**Règle absolue : rien ne se modifie jamais directement côté serveur.** Le dépôt est la source, `public/` compilé par la CI est le seul livrable poussé.

> **Ancien flux (avant le 21/09/2026, pour mémoire — sessions 1 à 7) :**
> ```
> Édition dans Blog perso/hugo/  →  hugo (build)  →  public/
>    →  sudo rsync -av --delete public/ /var/www/sorrodje.alter-it.org/
> ```
> Build et publication manuels depuis le Kimsufi. Remplacé par le pipeline GitHub Actions ci-dessus.

### Piège des UID — `public/` n'est pas un dossier partagé

La sandbox est un conteneur (UID **1000**). Sur l'hôte Kimsufi, `pierre-olivier` est UID **1001**. Un `chown` fait d'un côté casse les droits de l'autre :

- un `sudo chown -R` lancé côté Kimsufi sur `hugo/public/` le passe à **1001:1001** → la sandbox (1000) perd tout droit dessus, le build échoue (`permission denied`, `chtimes ... operation not permitted`) ;
- inversement, un `chown` vers 1000 côté sandbox casserait le Kimsufi.

**Conséquence : `public/` est un dossier généré et jetable, qui ne doit pas être partagé entre les deux environnements.** Le build final se fait côté Kimsufi par PO. En cas d'erreur de permission :
```bash
sudo rm -rf ".../hugo/public"   # puis relancer le build
```
**Ne jamais faire de `chown` sur `public/`.** Symptôme associé : des fichiers de `public/` appartenant à `root` (reliquat d'un `hugo` ou `rsync` lancé en root).

---

## 2. Emplacements (historique important)

Trois emplacements se sont succédé :

- La **sandbox** : `/home/user/Blog perso/hugo/` (vue depuis la sandbox) = `/home/pierre-olivier/open-terminal-data/Blog perso/hugo/` (vue depuis le Kimsufi). **Espace de dev historique (Sessions 1 à 7), désormais supprimé.**
- Un ancien doublon : `/home/pierre-olivier/dev/blog-sorrodje/`, créé au premier déploiement.
- **Mistral Vibe** (depuis le 21/09/2026) : espace de gestion actuel du blog, avec GitHub comme dépôt de référence.

Le doublon `dev/blog-sorrodje` a été **supprimé** en Session 3 après vérification (aucune référence cron / borgmatic / service ; le vhost pointe vers `/var/www`). **Ne pas recréer de copie parallèle.**

L'arbre de la sandbox `Blog perso/hugo/` a été **archivé** dans `Blog perso/hugo-archive-20260921.tar.gz` (27 Mo, thème et build inclus) puis **supprimé** le 21/09/2026, la gestion étant transférée sur Mistral Vibe. L'archive est figée : elle n'est plus alimentée et ne doit pas servir de base de travail — **la source à jour est GitHub**.

---

## 3. Arborescence du projet

```
hugo/
├── config/_default/
│   ├── hugo.toml          baseURL, theme, summaryLength, buildFuture, pagination, outputs, privacy
│   ├── languages.fr.toml  locale fr-FR, titre, dateFormat, mainSections, author
│   ├── menus.fr.toml      menu principal (Archives, À propos, recherche)
│   ├── params.toml        options du thème (colorScheme, header, homepage, article, list)
│   ├── markup.toml        Goldmark (requis par le thème)
│   └── taxonomies.toml    tag = "tags"
├── content/
│   ├── _index.md          accroche éditoriale de la home (3 paragraphes)
│   ├── about.md           page À propos
│   └── posts/             articles
├── layouts/               OVERRIDES PROJET (voir §4)
├── assets/
│   ├── css/custom.css     @font-face Ubuntu + police globale + header/hiérarchie
│   ├── css/schemes/cuivre.css   palette cuivre (voir §5)
│   └── img/logo-arbre.png       logo arbre (fond transparent) + logo-arbre-dark.png (inversé)
├── static/
│   ├── fonts/ubuntu/      4 WOFF2 auto-hébergés
│   ├── llms.txt           description du site pour les LLM
│   ├── favicon-16.png, -32, -48, favicon.ico   favicons arbre recadrés
│   ├── apple-touch-icon.png   180×180
│   ├── site.webmanifest   écrase celui du thème (nom « sorrodje », cuivre)
│   └── google*.html       vérification Google Search Console
├── themes/
│   ├── congo/             thème actif (contient son propre .git)
│   ├── hugo-PaperMod/     INUTILISÉ (test écarté) — à nettoyer
│   └── hugo-theme-anubis/ INUTILISÉ (non maintenu) — à nettoyer
├── mockups/               11 HTML de travail (tests de palette) — zone de transit, à supprimer
├── archetypes/default.md  gabarit de nouvel article
├── data/  i18n/           vides
├── public/                sortie compilée (généré, non versionné)
├── resources/             cache Hugo (généré)
└── .git/                  dépôt git du projet (voir §6)
```

---

## 4. Overrides projet (survivent aux MAJ du thème)

Ces fichiers vivent dans `hugo/layouts/` et **non** dans `hugo/themes/congo/`. C'est volontaire : ils ne sont pas écrasés lors d'une mise à jour du thème.

| Fichier | Rôle |
|---|---|
| `layouts/_partials/logo.html` | Marque du header : logo arbre à gauche + marque/sous-titre cuivre |
| `layouts/_partials/header/basic.html` | Copie du header du thème + classe `site-header` (nécessaire pour le liseré cuivre, voir §5.2) |
| `layouts/_partials/favicons.html` | Override des favicons — Congo le détecte et ignore son défaut (voir §5.2) |
| `layouts/_partials/extend-head.html` | Injection du script Matomo |
| `layouts/_partials/home/edito.html` | Page d'accueil éditoriale (accroche + articles récents + rubriques) |
| `layouts/index.json` | Index de recherche (voir §5.3) |
| `layouts/_partials/search-normalize.html` | Normalisation du texte indexé (voir §5.3) |

Même logique côté assets : `assets/css/schemes/cuivre.css`, `assets/css/custom.css` et `assets/img/logo-arbre*.png` sont dans le **projet**, pas dans le thème → ils survivent aux MAJ. Le `head.html` de Congo résout `resources.Get "css/schemes/<nom>.css"` avec repli automatique sur `congo.css`.

**Piège du partial `logo.html` :** il utilise `resources.Get`, qui cherche dans **`assets/`** et non dans `static/`. Un logo placé dans `static/img/` reste invisible. Vérifié en Session 6 (premier essai raté).

---

## 5. Éléments d'identité et fonctionnels

### 5.1 Identité visuelle

- **Palette** : scheme `cuivre` (activé par `colorScheme = "cuivre"` dans `params.toml`), 3 palettes × 11 nuances RGB au format Tailwind. Cuivre `#c87f4a` identique en clair et sombre ; accent secondaire `#a8693e`.
- **Police** : Ubuntu auto-hébergée, 4 WOFF2 dans `static/fonts/ubuntu/` (≈ 504 Ko), déclarée dans `assets/css/custom.css` avec `font-display: swap`. Pas de CDN tiers.
- **Mode sombre** : fond `#0f0f14`, texte ivoire `#f0e6d2`. **Mode clair** : fond `#f0f2f5`, texte `#2d3142`. Le mode clair n'est pas définitivement validé.

### 5.2 Header, logo et hiérarchie (Session 6)

Refonte UI de la Session 6 : le cuivre devient **structurel**, plus seulement décoratif.

| Élément | Valeur |
|---|---|
| Marque (`.site-header-marque`) | 40 px, gras 800, cuivre `#c87f4a` |
| Sous-titre | 20 px (16 px en mobile), cuivre foncé `#a8693e` en clair / cuivre en sombre |
| Liseré cuivre | 3 px sous le header + marge 2,5 rem |
| Logo arbre | 64 px de haut (44 px en mobile), à gauche du titre |
| Titres de section (`.edito-section-titre`) | 30 px + barre cuivre 56×4 px |
| Cartes rubriques (`.edito-rubrique`) | bordure gauche cuivre 4 px |

**Le liseré cuivre impose l'override du header.** Le CSS cible `header.site-header`, classe absente du header du thème — d'où `layouts/_partials/header/basic.html`, copie du header Congo avec la classe ajoutée.

**Le mode sombre inverse le logo** via une classe `.logo-sombre` (filtre d'inversion), d'où les deux fichiers `logo-arbre.png` et `logo-arbre-dark.png`.

**Favicons : passer par `favicons.html`, jamais par `extend-head.html`.** Congo gère les favicons nativement (`head.html`). Si `_partials/favicons.html` existe dans le projet, il l'utilise et ignore son défaut. Mettre les balises dans `extend-head.html` crée un **doublon**.

**Fichiers orphelins du thème (laissés en place, volontairement) :** Hugo copie tout `themes/congo/static/` dans `public/` — `favicon-16x16.png`, `favicon-32x32.png`, `android-chrome-*`, `site.webmanifest`. Aucun n'est référencé. Décision : **ne pas toucher au thème** (un `git pull` écraserait les suppressions). Coût : quelques Ko inutiles.

### 5.3 Recherche interne — normalisation de l'index

**Le problème (constaté, corrigé en Session 5) :**

L'index `public/index.json` contenait du texte **non aligné avec ce qu'un visiteur tape au clavier** :
- Entités HTML littérales (`&rsquo;` au lieu de `'`), car le template d'origine utilisait `.Plain` / `.Summary` sans décodage.
- Marqueurs de titre Markdown `#` collés au texte (`L'infra #Une seule machine`).
- Pages sans contenu (tags, sections vides) indexées → résultats fantômes.

Conséquence : la recherche Fuse.js est configurée avec **`threshold: 0.0` (match exact, voir `themes/congo/assets/js/search.js`)**. Chercher `l'infra` ne renvoyait rien, car l'index contenait `l&rsquo;infra`.

**Le correctif :** override `layouts/index.json` + partial `layouts/_partials/search-normalize.html` :

1. **Décodage** des entités HTML (`htmlUnescape`).
2. **Normalisation typographique** vers ce qu'un clavier produit : apostrophes courbes → droites, tirets longs → courts, guillemets français → droits. **Les accents sont préservés** (les décoder dégraderait la recherche de mots accentués).
3. **Nettoyage** des `#` de titres Markdown.
4. **Exclusion** des pages sans contenu textuel.

**Point délicat — l'échappement (à ne pas « simplifier ») :**

Hugo **échappe automatiquement** toute apostrophe droite en `&#39;` et tout guillemet en `&#34;` dès qu'une valeur est écrite dans un contexte HTML, ou via un `jsonify` global. **`safeJS` ne protège pas de cela.**

Seule méthode fiable trouvée : chaque champ est passé par `jsonify` **individuellement**, produisant une chaîne JSON déjà échappée, puis le tableau JSON est assemblé à la main dans `layouts/index.json`.

> ⚠️ **Ne pas revenir à un `dict ... | jsonify` global** dans `index.json` : cela réintroduit l'échappement HTML des apostrophes (`&#39;`) et casse à nouveau la recherche.

**Vérification après modification :** après un build, inspecter `public/index.json` — aucune entité HTML (`&#39;`, `&rsquo;`, etc.) ne doit apparaître, et les apostrophes doivent être droites.
```bash
cd "Blog perso/hugo" && hugo
python3 -c "
import json,re
d=json.load(open('public/index.json'))
bad=[(x.get('title'),k) for x in d for k in ('content','summary','title','section')
     if re.search(r'&#?\w+;', x.get(k,'') or '')]
print('entites HTML restantes:', bad or 'AUCUNE')
"
```

### 5.4 SEO

- `sitemap.xml`, `robots.txt`, RSS/JSON, schema.org Article/Breadcrumb, Open Graph, Twitter Cards : gérés nativement par Congo.
- `llms.txt` (`static/llms.txt`) : rédigé, décrit le blog et sa démarche pour les LLM.
- Search Console : propriété validée via préfixe d'URL, sitemap soumis.
- **Réflexe pour chaque nouvel article** : renseigner une `description:` courte dans le front matter (sinon Hugo retombe sur le résumé tronqué, moins propre).

### 5.5 Articles et séries

**Front matter d'un article :** `title`, `date`, `description`, `tags`. Optionnel : `slug`, `weight`.

**Le H1 ne doit pas figurer dans le corps** de l'article : il est déjà produit par le template à partir du `title`. Un `# Titre` dans le Markdown crée un doublon H1 (bug corrigé en Session 4). Les titres de section dans le corps sont en `##`.

**Séries d'articles :** ordonner avec un `weight` explicite (entier croissant) plutôt que de compter sur les dates. Le tri Hugo se fait par date par défaut, ce qui rend l'ordre fragile si les dates bougent. La série « Mon histoire IA » (5 billets, Session 7) utilise `weight: 1..5` plus un tag commun `"mon histoire IA"` comme fil.

**Slugs et caractères non-ASCII :** un nom de fichier contenant `œ`, `é`, etc. produit un slug d'URL dépendant de la translittération de Hugo. Pour fiabiliser l'URL sans toucher au `title` (qui doit garder ses caractères typographiques), ajouter un `slug:` explicite en ASCII dans le front matter.

### 5.6 `buildFuture` — contenus datés dans le futur

**`buildFuture = true` est activé dans `hugo.toml`.** Sans ce réglage, Hugo **ignore silencieusement** toute page dont la `date` dépasse l'horloge de la machine qui build : pas d'erreur, pas d'avertissement, la page n'existe simplement pas dans `public/`.

Cas d'usage concret (Session 7) : la série est datée du 16 au 20 septembre, le build est lancé le 15. Sans `buildFuture`, les 4 billets à venir disparaissent du `public/` et le `rsync` pousse un site incomplet.

**Conséquence opérationnelle :** le réglage vit dans la config versionnée du dépôt GitHub (`config/_default/hugo.toml`), donc il s'applique à la fois au build CI et aux builds locaux de vérif. La vérification avant publication reste un réflexe :
```bash
grep buildFuture config/_default/hugo.toml   # à la racine du clone du dépôt
```

---

## 6. Points connus / dette

- **`summaryLength = 40`** dans `hugo.toml` (était à 0, ce qui vidait les résumés de liste — corrigé en Session 5).
- **`mockups/`** : 11 fichiers HTML de travail (tests de palette) **confirmés présents dans le dépôt** (vérifié le 20/09/2026). Zone de transit, pas du livrable — à supprimer.
- **Thèmes inutilisés** : `themes/hugo-PaperMod` et `themes/hugo-theme-anubis` **confirmés présents dans le dépôt** (vérifié le 20/09/2026) — à nettoyer.
- **`.git` à la racine du projet** : obsolète — l'ancien dépôt local était vide (aucun remote, aucun commit) et l'arbre a été archivé/supprimé le 21/09/2026. La référence est désormais le dépôt GitHub.
- **`.git` dans `themes/congo/`** : idem, parti avec l'archive. Décision sans objet.
- **Rubriques non cliquables** : les 3 cartes de la home (`edito.html`) sont des `<div>` sans lien, avec badge « En cours ». C'est **volontaire** — aucun article n'est encore classé par rubrique, un lien mènerait à une page vide. À rendre cliquables quand le classement des articles sera défini.
- **Logo / favicons** : en place depuis la Session 6 (arbre PCB acheté par PO). Deux fichiers PNG dans `assets/img/` (clair + inversé), favicons dans `static/`.
- **Mode clair** : non définitivement validé.
- **Sandbox non sauvegardée** : sans objet — l'arbre sandbox a été archivé puis supprimé le 21/09/2026 ; le dépôt GitHub est la référence.
- **`data/` et `i18n/`** : vides (structure héritée du thème, sans usage pour l'instant).

---

## 7. Historique

- **Session 1 (2026-08-14)** — Méthode de travail, choix du thème (Congo), structure du projet, build fonctionnel.
- **Session 2 (2026-09-08)** — Identité visuelle : palette cuivre + police Ubuntu auto-hébergée.
- **Session 3 (2026-09-13)** — Déploiement en ligne (vhost Apache, Certbot, DNS Gandi), premier contenu, header, home éditoriale, `llms.txt`.
- **Session 4 (2026-09-13)** — About & `llms.txt` révisés, fix doublon H1, accroche home, Matomo, Search Console.
- **Session 5 (2026-09-14)** — Audit du site. Fix `summaryLength` (0 → 40). Refonte de l'index de recherche (décodage, normalisation, exclusion des pages vides). Création de ce document.
- **Session 6 (2026-09-14)** — Refonte UI : logo arbre (header, favicons), hiérarchie de la home, liseré cuivre, override `header/basic.html` et `favicons.html`. Découverte du piège des UID sandbox/Kimsufi.
- **Session 7 (2026-09-15)** — Publication de la série « Mon histoire IA » (5 billets, dates 16→20/09, `weight` 1→5). Retouches de « Pourquoi ce blog » et « À propos ». Nouvelle accroche de home. Ajout de `buildFuture = true` (contenus datés du futur ignorés silencieusement).
- **2026-09-21 (hors session)** — Bascule complète de la gestion du blog sur **Mistral Vibe**. Archivage de l'arbre de dev `Blog perso/hugo/` (`hugo-archive-20260921.tar.gz`, 27 Mo) puis suppression de la sandbox. GitHub devient le dépôt de référence.

---

*Document de référence stable. Il décrit la solution ; les issues / résumés de session font foi sur l'état courant et le reste-à-faire.*