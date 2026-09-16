# Site — Aurélie Diméglio, Ostéopathe D.O. à Meudon

Site vitrine statique (HTML/CSS pur, aucune dépendance, aucun build).
Les images sont des fichiers WebP dans `images/`, les polices viennent de Google Fonts.

## Pages

- `index.html` — accueil
- `apropos.html` — à propos
- `cycle.html` — règles douloureuses & troubles du cycle
- `femme-enceinte.html`
- `nourrisson.html`
- `endometriose.html`
- `machoire.html`
- `politique-cookies.html`

Les images sont dans `images/` (WebP) et doivent être déployées avec les pages.

## Déploiement sur Render (site statique)

### Option A — Blueprint (recommandé)

Le fichier `render.yaml` est déjà présent. Sur Render :

1. New → **Blueprint**
2. Connecter ce dépôt GitHub
3. Render lit `render.yaml` et crée le static site automatiquement

### Option B — Réglages manuels

Sur Render : New → **Static Site**, connecter le dépôt, puis :

- **Build Command** : *(laisser vide)*
- **Publish Directory** : `.`

C'est tout — il n'y a rien à compiler.

## Domaine personnalisé

Une fois déployé, dans les réglages du service Render → **Custom Domains**,
ajouter `osteopathe-meudon.fr` (et `www.`) puis pointer les DNS chez le
registrar vers la cible fournie par Render.

## Aperçu en local

Ouvrir `index.html` dans un navigateur (les images sont en chemins relatifs,
elles s'affichent tant que `images/` est à côté).
Ou avec Python : `python3 -m http.server` puis http://localhost:8000
