# Blog — sorrodje.alter-it.org

Source Hugo du blog. Site 100 % statique, servi par Apache sur un Kimsufi.

## Structure

- `content/posts/` — les billets (front matter TOML)
- `config/_default/` — configuration Hugo + options du thème Congo
- `layouts/`, `assets/` — overrides et personnalisations
- `mockups/` — maquettes HTML statiques (non déployées)

## Workflow

Chaque push sur `main` déclenche `.github/workflows/deploy.yml` :
build Hugo (`--minify`, sans les drafts) puis rsync vers le serveur.

Publier un billet : retirer `draft: true` dans son front matter, pusher —
le déploiement est automatique.

## Conventions

- Série « Mon histoire IA » : champ `series` + `weight` pour l'ordre, résumé = premier paragraphe avant `<!--more-->`.
