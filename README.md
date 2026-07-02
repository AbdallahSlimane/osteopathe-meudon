# Site — Aurélie Diméglio, Ostéopathe D.O. à Meudon

Site vitrine statique (HTML/CSS pur, aucune dépendance, aucun build).
Toutes les images sont embarquées en base64, les polices viennent de Google Fonts.

## Pages

- `index.html` — accueil
- `apropos.html` — à propos
- `femme-enceinte.html`
- `nourrisson.html`
- `sportifs.html`
- `machoire.html`
- `endometriose.html`
- `politique-cookies.html`

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

Aucun serveur requis, ouvrir `index.html` dans un navigateur.
Ou avec Python : `python3 -m http.server` puis http://localhost:8000
