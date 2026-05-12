# Re-Watt — Landing page

One-pager statique en HTML/CSS/JS vanilla. Aucun build, aucune dépendance hors Google Fonts (Inter).

## Structure

```
re-watt-landing-v2/
├── index.html              ← landing principale (tout HTML + CSS + JS inline)
├── mentions-legales.html   ← page mentions légales (placeholder à rédiger)
├── README.md
└── assets/
    ├── logo-rewatt.png       ← header
    ├── picto-laureat.png     ← bloc partenaires (col. 1)
    ├── logo-rcube.jpg        ← bloc partenaires (col. 2)
    ├── logo-gsm-master.png   ← bloc partenaires (col. 3)
    ├── favicon.png           ← favicon (crop du RW du logo)
    ├── favicon.ico           ← favicon legacy (16/32/48)
    └── apple-touch-icon.png  ← apple touch icon 180×180
```

## 1. Changer l'email destinataire

Une seule constante JS à modifier, en haut du `<script>` de `index.html` :

```js
const CONTACT_EMAIL = 'contact@re-watt.fr';
```

Cette constante alimente automatiquement :
- les 4 cartes mailto du bloc "Vous êtes…" (avec objet et corps pré-remplis),
- le lien email du footer.

Les objets et corps des 4 messages se modifient juste en dessous, dans l'objet `PROFILE_TEMPLATES`. L'encodage URL (espaces, accents, em-dashes, retours à la ligne) est fait automatiquement par `encodeURIComponent` — tu peux écrire en français naturel.

## 2. Changer les couleurs

Toute la palette est en variables CSS dans `:root`, en haut du `<style>` de `index.html` :

```css
:root {
  --bleu-rewatt:      #2B82C9;  /* extrait du PPTX */
  --vert-rewatt:      #4CAF50;  /* extrait du PPTX */
  --anthracite:       #2B2B2B;
  --gris-texte:       #5C5C5C;
  --bg:               #FAFAF7;
  --bg-footer:        #F4F7F9;
  --border:           #E5E5E5;
  /* ... */
}
```

Modifier ici → propagation dans toute la page.

## 3. Mentions légales

Le fichier `mentions-legales.html` est volontairement minimal :
- un titre `<h1>Mentions légales</h1>`
- un placeholder `Contenu à venir.`
- un lien de retour vers `index.html`

**Le contenu réel reste à rédiger** (RGPD : éditeur du site, hébergeur, données collectées, etc.).

## 4. Déploiement Netlify (drag-and-drop)

1. Ouvre [https://app.netlify.com/drop](https://app.netlify.com/drop).
2. Glisse le dossier **`re-watt-landing-v2/`** entier sur la zone de drop (le dossier complet, pas un fichier seul).
3. Netlify déploie en quelques secondes et fournit une URL en `*.netlify.app`.
4. Pour brancher un domaine personnalisé (`re-watt.fr`) : onglet **Domain settings** → **Add custom domain**.

Mise à jour ultérieure : re-glisser le dossier sur la même URL Netlify, ou `netlify deploy` en CLI.

## Notes techniques

- Police : Google Fonts **Inter** (poids 400, 500, 700, 800).
- Favicon : crop du graphique **RW** depuis `logo-rewatt.png` (fond transparent). Trois formats fournis pour couvrir tous les navigateurs : `assets/favicon.png` (512×512), `assets/favicon.ico` (16/32/48 multi-résolutions) et `assets/apple-touch-icon.png` (180×180).
- Couleurs Bleu & Vert Re-Watt extraites directement du PPTX `Re-Watt Offre Partenaires Corners Phase 1.pptx` (analyse des slides XML). Le PNG d'essais ("Police avec contour blanc…") les confirme visuellement.
- Header sticky avec `position: sticky` + `backdrop-filter` (effet verre dépoli).
- Bouton "Back to top" : apparaît après 400 px de scroll.
- Menu burger plein écran sur mobile (`<768px`), avec gestion clavier (Échap pour fermer).
- Accessibilité : WCAG AA — skip link, focus visible, ARIA labels, zones de tap ≥ 44 px, `prefers-reduced-motion` respecté.
- SEO : `<title>`, meta description, Open Graph, Twitter Card, `lang="fr"`.
- Aucun tracking, aucun cookie banner.

## Aperçu local

```bash
cd re-watt-landing-v2
python3 -m http.server 8000
# puis http://localhost:8000
```
