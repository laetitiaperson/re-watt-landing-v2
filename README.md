# Re-Watt — Landing page

One-pager statique en HTML/CSS/JS vanilla. Aucun build, aucune dépendance hors Google Fonts (Inter).

## Structure du projet

```
re-watt-landing/
├── index.html              ← tout le HTML + CSS + JS dans un seul fichier
├── README.md               ← ce fichier
├── favicon.ico             ← (déjà fourni)
├── favicon-16.png          ← (déjà fourni)
├── favicon-32.png          ← (déjà fourni)
├── apple-touch-icon.png    ← (déjà fourni)
└── assets/
    ├── logo-rewatt.png     ← À PLACER (logo sans baseline)
    └── picto-trophee.png   ← À PLACER (picto société à mission)
```

## 1. Où poser les 2 images

Crée le dossier `assets/` à côté de `index.html` et place-y les deux fichiers tels quels :

- `assets/logo-rewatt.png`   — utilisé uniquement dans la section 4 (signature).
- `assets/picto-trophee.png` — utilisé uniquement dans la section 4, à 80 px.

Les chemins sont relatifs, donc le site fonctionne aussi bien en local qu'une fois déployé.

## 2. Où remplacer `LINKEDIN_URL_PLACEHOLDER`

Dans `index.html`, section 4 (signature visuelle), bloc `<nav class="signature__socials">` :

```html
<a class="social-link"
   href="LINKEDIN_URL_PLACEHOLDER"   ← remplacer par l'URL réelle
   target="_blank"
   rel="noopener noreferrer"
   aria-label="LinkedIn Re-Watt">
```

(Un seul remplacement à faire, une seule fois.)

## 3. Comment changer l'email destinataire

L'email est centralisé dans une **constante JavaScript unique**, en haut du `<script>` en fin de `index.html` :

```js
const CONTACT_EMAIL = 'contact@re-watt.fr';
```

Le changer ici met à jour automatiquement :

- les 4 cartes mailto de la section "Vous êtes…",
- le lien `contact@re-watt.fr` du footer.

Pour modifier les objets et corps de message des 4 cartes, édite l'objet `PROFILE_TEMPLATES` juste en dessous. L'encodage URL (espaces, accents, retours à la ligne, em-dashes) est fait automatiquement par `encodeURIComponent`, donc tu peux écrire les chaînes en français naturel sans te soucier des caractères spéciaux.

## 4. Comment swap les variantes de la question hero

La section 1 (`<section class="section hero">`) contient le `<h1>` avec **3 variantes** : la première active, les deux autres en commentaire HTML.

```html
<h1 class="hero__question" id="hero-title">
  <!-- Variante par défaut (active) -->
  Et si 80&nbsp;% des batteries jetées étaient réparables&nbsp;?

  <!-- Variante A — décommenter pour activer (et commenter la variante par défaut)
  80&nbsp;% des batteries au recyclage sont réparables. Et si on s'y mettait&nbsp;?
  -->

  <!-- Variante B — décommenter pour activer (et commenter la variante par défaut)
  Pourquoi jeter une batterie sur 5 qui est réparable… alors qu'elles le sont toutes à 80&nbsp;%&nbsp;?
  -->
</h1>
```

Pour swap : commente la variante active, décommente celle que tu veux.

### Hero de repli (si la question ne fonctionne pas visuellement)

Juste sous la section 1, un bloc `<!-- ===== HERO DE REPLI (désactivé) ===== -->` contient une version sobre avec uniquement la phrase mission (sans logo). Pour l'activer :

1. Commente toute la `<section class="section hero">` du dessus.
2. Décommente le bloc `<section class="section hero hero--fallback">`.

## Aperçu local

Ouvre `index.html` dans un navigateur (double-clic), **ou** sers le dossier :

```bash
cd re-watt-landing
python3 -m http.server 8000
# puis http://localhost:8000
```

## Déploiement Netlify (drag-and-drop)

1. Ouvre [https://app.netlify.com/drop](https://app.netlify.com/drop) dans ton navigateur.
2. Glisse le dossier **`re-watt-landing/`** entier sur la zone de drop (pas le fichier seul — le dossier).
3. Netlify déploie en quelques secondes et te fournit une URL en `*.netlify.app`.
4. Pour brancher un domaine personnalisé (`re-watt.fr`) : onglet **Domain settings** → **Add custom domain**.

Pour mettre à jour le site plus tard : re-glisse le dossier sur la même URL Netlify, ou utilise `netlify deploy` en CLI.

## Accessibilité & SEO

- WCAG AA : contraste OK sur palette, focus clavier visible (`:focus-visible`), zones tactiles ≥ 44 px sur les liens sociaux, lien "skip to content", balises sémantiques (`<header>`, `<main>`, `<section>`, `<footer>`, `<nav>`).
- SEO : `<title>`, `<meta description>`, Open Graph, Twitter Card, favicons multi-tailles, `lang="fr"`.
- Préférence "reduced motion" respectée.
- Aucun tracking, aucun cookie banner.

## Tokens design

Toutes les valeurs (couleurs, espacements, rayons, ombres) sont en variables CSS dans `:root`, en haut du `<style>`. Un seul endroit à modifier pour propager.
