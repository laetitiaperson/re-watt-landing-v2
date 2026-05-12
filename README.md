# Re-Watt — Landing page

One-pager statique en HTML/CSS/JS vanilla. Aucun build, aucune dépendance hors Google Fonts (Inter).

## Structure

```
re-watt-landing-v2/
├── index.html                       ← landing + bandeau cookies + modal RGPD (tout inline)
├── mentions-legales.html            ← page mentions légales (placeholder à rédiger)
├── README.md
├── DESIGN-HANDOFF.md                ← doc pour l'intégrateur WordPress
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

## 3. Pages légales

### `mentions-legales.html`

Volontairement minimal :
- un titre `<h1>Mentions légales</h1>`
- un placeholder `Contenu à venir.`
- un lien de retour vers `index.html`

**À compléter** : éditeur du site (raison sociale, forme juridique, siège, SIREN/RCS, capital), directeur de publication, hébergeur (GitHub Inc. ou Netlify), contact.

### Politique de confidentialité

La page dédiée a été supprimée. À sa place, un **bandeau de consentement aux cookies** + **modal de personnalisation** ont été intégrés dans `index.html`. Le modal contient une notice RGPD condensée (contact, droits, mention CNIL) ainsi que les choix par catégorie (mesure d'audience, contenus tiers).

- **Bandeau** : apparaît au bas de la page à la 1re visite. 3 boutons : *Tout refuser* / *Personnaliser* / *Tout accepter*.
- **Modal de personnalisation** : ouvert via *Personnaliser* ou via le lien "Politique de confidentialité" du footer.
- **Persistance** : le choix est stocké dans `localStorage` sous la clé `rewatt-cookie-consent`, version 1, durée 13 mois (recommandation CNIL).
- **Pour réinitialiser et revoir le bandeau** : ouvrir la console et exécuter `localStorage.removeItem('rewatt-cookie-consent')`, puis recharger.

Le bandeau est **prêt pour la bascule WordPress** : les toggles existent déjà, il suffira de brancher les scripts analytics / embeds réels sur les valeurs `localStorage.rewatt-cookie-consent`.

### `DESIGN-HANDOFF.md`

Document de référence pour la personne qui intégrera la landing sur WordPress. Couvre : palette extraite du PPTX, typographie, tokens layout, breakpoints, structure des 7 blocs avec specs détaillées (copy, comportements, mailto), accessibilité, SEO, et checklist de migration. À fournir à l'intégrateur ou intégratrice avec accès au dépôt.

### `MIGRATION-WORDPRESS.md`

Guide pratique de migration côté client. Couvre les décisions à prendre (WordPress.com vs .org, choix d'hébergeur, DIY vs prestataire), le calendrier-type sur une semaine, la bascule DNS J0, les coûts prévisionnels, et les checks J+1 / J+7. À lire en premier si tu envisages la migration.


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
