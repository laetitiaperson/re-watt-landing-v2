# Re-Watt — Design handoff pour intégration WordPress

Document de référence pour la personne (interne ou prestataire) qui intégrera la landing Re-Watt sur WordPress.

L'implémentation statique de référence (HTML/CSS/JS vanilla) est dans ce dépôt :
[`index.html`](./index.html). Elle sert de **source de vérité visuelle** — l'intégration WP doit la reproduire à l'identique au pixel près.

Aperçu live : https://laetitiaperson.github.io/re-watt-landing-v2/

---

## 1. Identité visuelle

### 1.1 Palette

Toutes les couleurs ont été extraites du deck partenaires (`Re-Watt Offre Partenaires Corners Phase 1.pptx`, analyse des XML des slides) et confirmées par le PNG d'essais "Police avec contour blanc pour compatibilité mode sombre.png".

| Token              | Hex        | Usage                                                |
|--------------------|------------|------------------------------------------------------|
| `--bleu-rewatt`    | `#2B82C9`  | Chiffre 80 %, labels profils, aplat section mission  |
| `--bleu-rewatt-dark` | `#1F6BAB`| Hover dérivé du bleu                                 |
| `--vert-rewatt`    | `#4CAF50`  | Claim "réparables", liens, CTA, hovers, favicon      |
| `--vert-rewatt-dark` | `#3D9140`| Hover dérivé du vert                                 |
| `--anthracite`     | `#2B2B2B`  | Texte principal                                      |
| `--gris-texte`     | `#5C5C5C`  | Texte secondaire (nav, descriptions cartes, footer)  |
| `--gris-sec`       | `#8A9199`  | Texte tertiaire (légales, captions)                  |
| `--bg`             | `#FAFAF7`  | Fond global                                          |
| `--bg-footer`      | `#F4F7F9`  | Fond footer                                          |
| `--border`         | `#E5E5E5`  | Bordures cartes, séparateurs                         |
| `--white`          | `#FFFFFF`  | Texte sur aplat bleu, fond cartes profils            |

**Contraste WCAG AA validé** sur les paires utilisées (texte/fond).

### 1.2 Typographie

- **Famille unique** : Inter (Google Fonts).
- **Poids utilisés** : 400 (regular), 500 (medium), 700 (bold), 800 (extra-bold).
- **Sur WordPress** : enqueue de la police via `wp_enqueue_style` ou plugin (ex. *Custom Fonts*, *OMGF* pour self-host).
  Lien officiel : `https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;800&display=swap`

### 1.3 Iconographie / assets fournis

Tous dans le dossier [`/assets/`](./assets/) :

| Fichier                  | Description                                | Format     | Usage                             |
|--------------------------|--------------------------------------------|------------|-----------------------------------|
| `logo-rewatt.png`        | Logo Re-Watt avec wordmark                 | PNG 850×681| Header (hauteur 48 px)            |
| `favicon.png`            | Marque RW seule, crop du logo, transparent | PNG 512×512| Favicon moderne                   |
| `favicon.ico`            | Multi-tailles 16/32/48                     | ICO        | Favicon legacy                    |
| `apple-touch-icon.png`   | RW sur fond transparent                    | PNG 180×180| iOS écran d'accueil               |
| `picto-laureat.png`      | Picto "Trophée du Réemploi 2025" recadré   | PNG 744×698| Bloc partenaires col. 1           |
| `logo-rcube.jpg`         | Logo RCube                                 | JPG        | Bloc partenaires col. 2           |
| `logo-gsm-master.png`    | Logo GSM Master                            | PNG        | Bloc partenaires col. 3           |

Sur WordPress, uploader le tout dans la Media Library.

---

## 2. Tokens layout

| Token                  | Valeur          | Note                                  |
|------------------------|-----------------|---------------------------------------|
| `--header-h`           | `72px`          | Hauteur du header sticky              |
| `--container-max`      | `1120px`        | Largeur max du contenu centré         |
| `--container-px`       | `24px`          | Padding latéral min (mobile + desktop)|
| `--section-py-desktop` | `96px`          | Padding vertical desktop (≥768 px)    |
| `--section-py-mobile`  | `56px`          | Padding vertical mobile (<768 px)     |
| `--radius`             | `12px`          | Rayon des cartes                      |
| `--transition`         | `200ms ease`    | Transitions UI                        |

**Breakpoints** :

| Nom       | Min-width   | Grilles                                           |
|-----------|-------------|---------------------------------------------------|
| Mobile    | < 640 px    | Cartes profils 1 col, partenaires 1 col, burger   |
| Tablette  | ≥ 640 px    | Cartes profils 2 col                              |
| Large tab | ≥ 768 px    | Partenaires 3 col, nav desktop, baseline visible  |
| Desktop   | ≥ 1024 px   | Cartes profils 4 col                              |

**Ombres** :

```css
--shadow-soft:   0 1px 2px rgba(0, 0, 0, .04);            /* repos cartes */
--shadow-hover:  0 12px 28px rgba(43, 130, 201, .14);     /* hover cartes */
--shadow-header: 0 2px 12px rgba(0, 0, 0, .06);           /* header au scroll */
```

---

## 3. Structure de la page

L'ordre vertical et les ancres doivent être respectés pour préserver les liens du menu :

1. **Header sticky** (`<header>`) — logo + baseline inline + nav 3 entrées
2. **`#hero`** — chiffre choc 80 %
3. **`#concept`** — phrase mission (aplat bleu)
4. **Promesse** — verbes "Diagnostiquer · réparer · reconditionner · prolonger."
5. **`#contact`** — "Vous êtes…" 4 cartes mailto
6. **`#partenaires`** — 3 colonnes Lauréat / RCube / GSM Master
7. **Footer**
8. **Bouton back-to-top** (flottant, hors flux)

⚠️ **Slugs à préserver** lors de la migration WP (pour ne pas casser les liens externes éventuels) :
- `/mentions-legales` (page WP avec slug `mentions-legales`)
- `/politique-confidentialite` (page WP avec slug `politique-confidentialite`)
- Ancres on-page : `#hero`, `#concept`, `#contact`, `#partenaires`, `#top`

---

## 4. Spécifications par bloc

### 4.1 Header (sticky)

- `position: sticky; top: 0;`, z-index 100.
- Fond `rgba(255,255,255,0.85)` + `backdrop-filter: blur(12px)`.
- Au scroll (> 8 px), classe `.is-scrolled` ajoutée → bordure basse `--border` + `box-shadow: var(--shadow-header)`.
- **À gauche** : logo Re-Watt (48 px de haut) + baseline "Redonnez vie à vos batteries" inline à droite immédiate, taille `0.875rem`, `--gris-texte`. Baseline masquée à <768 px.
- **Au centre** (visible ≥768 px) : nav avec 3 liens — *Notre concept* / *Nos partenaires* / *Contact*. Hover et focus : couleur passe à `--vert-rewatt`, soulignement vert (`::after` animé via `transform: scaleX`).
- **À droite** (visible <768 px) : burger 44×44 px qui ouvre un menu plein écran. Animation barres → croix sur état ouvert.

### 4.2 Bloc Hero `#hero`

Hiérarchie typographique stricte, centrée :

| Élément          | Texte                                           | Style                                                                                      |
|------------------|-------------------------------------------------|--------------------------------------------------------------------------------------------|
| Kicker           | "Le saviez-vous ?"                              | `0.875rem`, weight 500, anthracite, letter-spacing `0.2em`, uppercase                      |
| Chiffre          | "80 %" (avec espace insécable)                  | `clamp(6rem, 18vw, 14rem)`, weight 800, **bleu Re-Watt**, line-height 0.9                  |
| Lead             | "des batteries électriques qui sont remplacées" | `clamp(1.5rem, 3vw, 2.25rem)`, weight 400, anthracite, max-width 22ch                      |
| Claim (H1)       | "sont en réalité réparables"                    | `clamp(1.5rem, 3vw, 2.25rem)`, weight 700, **vert Re-Watt**, uppercase, letter-spacing 0.02em |

L'ordre et les couleurs doivent rester exactement comme ça.

### 4.3 Bloc Mission `#concept`

- **Aplat pleine largeur** : `background: var(--bleu-rewatt)`.
- Texte blanc, weight 500, taille `clamp(1.5rem, 2.5vw, 2rem)`, max-width 800 px, centré.
- Phrase : « Re-Watt prolonge la durée de vie des batteries électriques amovibles, près de chez vous. »
- **Aucun séparateur décoratif** (filets précédents supprimés).

### 4.4 Bloc Promesse

Phrase unique centrée :
> Diagnostiquer Réparer Reconditionner Prolonger

- Taille `clamp(1.25rem, 2.25vw, 1.75rem)`, weight 500, letter-spacing 0.04em, word-spacing 0.25em, couleur `--vert-rewatt`.
- 4 verbes capitalisés, séparés par des espaces (pas de ponctuation, pas de point final).

### 4.5 Bloc "Vous êtes…" `#contact`

- Titre H2 centré : « Vous êtes… »
- Grille de 4 cartes : 1 col mobile → 2 col tablette → 4 col desktop. Utiliser `minmax(0, 1fr)` pour éviter qu'un mot long élargisse une colonne.
- **Chaque carte** est un `<a href="mailto:...">` (toute la zone cliquable) :

| Profil         | Label (bleu Re-Watt, weight 700) | Description (gris)                                                                                                |
|----------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Particulier    | Particulier                      | Vous voulez faire diagnostiquer ou réparer la batterie de votre vélo, scooter, trottinette ou outil portatif.     |
| Professionnel  | Professionnel                    | Vous gérez une flotte, un atelier ou une activité qui dépend de batteries amovibles.                              |
| Partenaire     | Partenaire                       | Vous souhaitez rejoindre notre réseau d'ateliers de réparation/reconditionnement.                                 |
| Écosystème     | Écosystème                       | Vous êtes investisseur, institutionnel, journaliste ou acteur de la transition écologique.                        |

- Style carte : padding 24 px, fond blanc, bordure 1 px `--border`, `border-radius: 12px`, `box-shadow: var(--shadow-soft)`.
- Hover/focus : `translateY(-3px)`, `box-shadow: var(--shadow-hover)`, bordure passe à `--vert-rewatt`. La flèche `→` du CTA se décale de 4 px.

**Mailto pré-rempli (UTF-8 encodé) — objets et corps à reproduire à l'identique** :

| Profil         | Subject                                | Body                                                                                                                                                                       |
|----------------|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Particulier    | `Re-Watt — Demande Particulier`        | `Bonjour,\n\nJe souhaite en savoir plus sur vos services pour particuliers.\nMa demande concerne : ...\n\nMerci !`                                                          |
| Professionnel  | `Re-Watt — Demande Professionnel`      | `Bonjour,\n\nJe gère une activité qui dépend de batteries amovibles et souhaite en savoir plus sur vos services pour professionnels.\nMa demande concerne : ...\n\nMerci !`|
| Partenaire     | `Re-Watt — Demande Partenaire`         | `Bonjour,\n\nJe souhaite rejoindre votre réseau d'ateliers de réparation/reconditionnement.\nMon profil / mon atelier : ...\n\nMerci !`                                    |
| Écosystème     | `Re-Watt — Demande Écosystème`         | `Bonjour,\n\nJe vous contacte en tant qu'investisseur / institutionnel / journaliste / acteur de la transition écologique.\nMa demande concerne : ...\n\nMerci !`         |

**Destinataire** : `contact@re-watt.fr` — à centraliser dans une variable / option du thème pour modification facile.

> Note WP : si tu remplaces les `mailto:` par un **formulaire de contact** (Contact Form 7, WPForms, Fluent…), prévoir un dropdown "Vous êtes…" avec ces 4 valeurs comme premier champ pour conserver la logique de qualification. Mettre à jour la politique de confidentialité en conséquence (mention RGPD au-dessus du bouton submit).

### 4.6 Bloc Partenaires `#partenaires`

- Titre H2 centré, max-width 720 px :
  > « Une expertise reconnue au service de l'économie circulaire »
- Grille 1 col mobile → 3 col ≥768 px, gap 48 px desktop.
- **Chaque colonne** est un `<a>` cliquable (toute la zone) :

| Col. | Visuel                    | Titre sous l'image                                          | URL externe (`target="_blank" rel="noopener noreferrer"`)                          |
|------|---------------------------|-------------------------------------------------------------|------------------------------------------------------------------------------------|
| 1    | `picto-laureat.png`       | Lauréat du Réemploi aux Assises Nationales du Réemploi      | `https://www.youtube.com/watch?v=ZKKCYCPfzB8`                                       |
| 2    | `logo-rcube.jpg`          | RCube — Fédération du Réemploi & Réparation                 | `https://rcube.org/`                                                                |
| 3    | `logo-gsm-master.png`     | GSM Master — L'école du Réemploi                            | `https://gsmmaster.fr/`                                                             |

- Visuel : conteneur de 140 px de haut, `display: flex; align-items: center; justify-content: center;`, image `object-fit: contain; max-height: 140px`.
- Hover : `translateY(-3px)`, image `opacity: 0.9`.

### 4.7 Footer

- Fond `--bg-footer` (`#F4F7F9`), bordure haute `--border`, padding `56px 0 32px`, texte centré.
- Empilement vertical :
  1. "Re-Watt" — weight 500, taille 1 rem, anthracite
  2. Lien `contact@re-watt.fr` (mailto:) — souligné, `--gris-texte`, hover vert
  3. © 2026 Re-Watt — taille `0.8125rem`, `--gris-sec`
  4. Pictos sociaux LinkedIn + YouTube — 44×44 px tap target, picto SVG 22 px, couleur `--gris-texte` → `--vert-rewatt` au hover
     - LinkedIn : `https://www.linkedin.com/company/re-watt-clinique-batteries/posts/?feedView=all`
     - YouTube : `https://www.youtube.com/channel/UCc0IIA03CBrAF3MuBHuDdsQ`
  5. Liens légaux : *Mentions légales* · *Politique de confidentialité* — taille `0.75rem`, `--gris-sec`

### 4.8 Bouton "Back to top" (flottant)

- `position: fixed; bottom: 24px; right: 24px;`
- 44×44 px, cercle, fond `--vert-rewatt`, chevron blanc.
- **Caché** par défaut (`opacity: 0; visibility: hidden`).
- **Visible** quand `scrollY > 400 px` (classe `.is-visible` ajoutée par JS).
- Hover : fond `--vert-rewatt-dark`.
- Clic : `window.scrollTo({ top: 0, behavior: 'smooth' })`.

### 4.9 Burger menu mobile

- Visible uniquement <768 px, bouton 44×44 px avec 3 barres horizontales.
- Animation barres → croix sur état ouvert (transform CSS).
- `aria-expanded` synchronisé.
- Menu plein écran : `position: fixed; inset: 0; top: var(--header-h);`, fond blanc.
- Lien de menu : padding 16 px 8 px, taille 1.25 rem, bordure basse `--border`.
- Fermeture : clic sur lien, clic burger, touche Échap, resize ≥768 px.
- `document.body.style.overflow = 'hidden'` pendant l'ouverture pour bloquer le scroll d'arrière-plan.

---

## 5. Comportements interactifs (JS minimal — aucun tracking)

| Comportement             | Déclencheur          | Action                                                                 |
|--------------------------|----------------------|------------------------------------------------------------------------|
| Scroll smooth ancres     | Clic lien `#xxx`     | `scroll-behavior: smooth` CSS + `scroll-padding-top` pour header sticky |
| Header au scroll         | `window.scroll`      | Ajoute/retire classe `.is-scrolled` (seuil 8 px)                       |
| Burger ouvrir/fermer     | Clic + Échap + Resize| Toggle classe `.is-open` + `aria-expanded`                             |
| Mailto enrichi           | Au load              | JS construit `mailto:` avec subject + body `encodeURIComponent`        |
| Back-to-top              | `window.scroll`      | Ajoute classe `.is-visible` au-delà de 400 px                          |

---

## 6. Accessibilité (WCAG 2.1 AA)

- `lang="fr"` sur le `<html>`.
- Balises sémantiques : `<header>`, `<main>`, `<section>`, `<nav>`, `<footer>`.
- Hiérarchie de titres respectée (un seul `<h1>` = le claim hero, `<h2>` pour les blocs).
- `aria-label` sur chaque `<nav>` et chaque lien icône-seule.
- Skip link "Aller au contenu" en début de page (visible au focus).
- `:focus-visible` avec outline 3 px `--vert-rewatt`, offset 3 px.
- Zones tactiles ≥ 44×44 px sur tous les liens icônes (sociaux, back-to-top, burger).
- Contraste vérifié sur paires couleur/fond.
- Préférence `prefers-reduced-motion` respectée (transitions désactivées).

---

## 7. SEO

| Tag                | Valeur                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------|
| `<title>`          | Re-Watt — Redonnez vie à vos batteries                                                                       |
| `meta description` | Re-Watt prolonge la durée de vie des batteries électriques amovibles, près de chez vous. 80 % des batteries envoyées au recyclage sont en réalité réparables. |
| `meta theme-color` | `#4CAF50`                                                                                                    |
| `og:type`          | `website`                                                                                                    |
| `og:title`         | identique à `<title>`                                                                                        |
| `og:description`   | identique à `meta description`                                                                               |
| `og:image`         | `assets/og-image.png` — **à générer** (1200×630, image de partage)                                           |
| `og:locale`        | `fr_FR`                                                                                                      |
| `twitter:card`     | `summary_large_image`                                                                                        |

Sur WordPress, Yoast SEO ou Rank Math gèrent ça nativement.

---

## 8. Performance & qualité

- **Police** : un seul appel Google Fonts (4 poids combinés). À auto-héberger si on veut zero call externe.
- **Images** : conserver les PNG/JPG du `/assets/`. Optimisation : passer par TinyPNG ou ShortPixel (plugin WP).
- **JS** : ~3 ko inlined dans la version statique. Sur WP, l'enqueue conditionnel suffit (pas besoin de bundler).
- **CSS** : ~15 ko inlined. À convertir en feuille de style enfant du thème WP, ou en custom-property CSS native du theme.json (FSE).

---

## 9. Suggestion d'architecture WordPress

Le client est libre, mais à titre indicatif :

- **Thème** : base légère type **Astra**, **Kadence**, **GeneratePress** ou Block Theme natif (FSE).
- **Builder** : Gutenberg (blocks natifs + ACF si besoin), **ou** Elementor / Bricks si l'équipe est plus à l'aise dessus.
- **Plugins essentiels** :
  - **Yoast SEO** ou **Rank Math** (SEO + sitemap)
  - **Wordfence** ou **Solid Security** (sécurité)
  - **WP Rocket** ou **LiteSpeed Cache** (perf)
  - **Contact Form 7** / **WPForms** / **Fluent Forms** (formulaire si on remplace mailto:)
  - **Complianz** ou **Cookiebot** (bandeau cookies CNIL-friendly, devient obligatoire dès qu'un plugin dépose un cookie non essentiel)
- **Pages WP à créer** :
  - `Accueil` (slug par défaut)
  - `Mentions légales` → `/mentions-legales`
  - `Politique de confidentialité` → `/politique-confidentialite`
- **Custom Post Types** : aucun a priori (one-pager). Si Re-Watt ajoute un blog/actualités plus tard → CPT `article` ou `actualite`.

---

## 10. Checklist de migration

- [ ] Récupérer les assets du `/assets/` du dépôt
- [ ] Récupérer la palette de couleurs et l'injecter dans le theme.json ou les variables CSS
- [ ] Charger Inter (4 poids)
- [ ] Reproduire les 7 blocs de la landing à l'identique (cf. § 4)
- [ ] Connecter le formulaire de contact (ou conserver mailto:)
- [ ] Mettre à jour la politique de confidentialité avec les cookies réels du setup WP
- [ ] Installer un bandeau cookies si nécessaire (cf. politique)
- [ ] Tester accessibilité (skip link, focus, ARIA) sur la version WP
- [ ] Tester responsive sur 320 / 375 / 768 / 1024 / 1440 px
- [ ] Tester ouverture des `mailto:` / soumission du formulaire
- [ ] Générer une image Open Graph 1200×630
- [ ] Configurer le SEO (title, description, OG, sitemap)
- [ ] Mettre en place une redirection 301 de l'ancienne URL GitHub Pages vers le nouveau domaine
- [ ] Désactiver l'indexation GitHub Pages (ajouter `<meta name="robots" content="noindex">`) le temps de la transition

---

## 11. Contact

Pour toute question sur l'implémentation actuelle ou les choix de design : `contact@re-watt.fr`.
