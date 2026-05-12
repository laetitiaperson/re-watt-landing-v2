# Re-Watt — Migration vers WordPress

Guide pratique pour faire passer la landing actuelle (statique sur GitHub Pages) à un site WordPress, sans casser ce qui marche.

> **Documents liés** :
> - [`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md) — specs visuelles et fonctionnelles de la landing, à fournir à toute personne qui intègre.
> - [`index.html`](./index.html) — source de vérité visuelle (la version WP doit reproduire ça au pixel).
> - [`BRIEF-PRESTATAIRE.md`](./BRIEF-PRESTATAIRE.md) — cahier des charges prêt à envoyer si tu prends un freelance.

---

## 1. Décisions à prendre (en 10 min)

Avant tout achat, ces 4 choix conditionnent la suite.

### 1.1 WordPress.com ou WordPress.org (auto-hébergé) ?

| Critère                | WordPress.com (plan Business)       | WordPress.org (auto-hébergé)              |
|------------------------|--------------------------------------|--------------------------------------------|
| Prix annuel            | ~290 €/an (plan Business)            | ~80–150 €/an (hébergement) + domaine       |
| Installation           | Zéro effort                          | 1-click chez la plupart des hébergeurs     |
| Plugins                | Limité au plan Business+             | Tous, sans restriction                     |
| Thèmes                 | Limité au plan Business+             | Tous, sans restriction                     |
| Liberté CSS / HTML     | Limité                               | Totale                                     |
| Sauvegardes            | Incluses                             | À configurer (gratuit avec plugin)         |
| RGPD / serveurs UE     | Aux US (Automattic), CCT en place    | Au choix selon hébergeur                   |

**Recommandation pour Re-Watt** : **WordPress.org auto-hébergé** chez un hébergeur français/européen, pour souveraineté + budget + liberté. Cohérent avec le positionnement "souveraineté industrielle" de la marque.

### 1.2 Quel hébergeur ?

Pour une landing one-pager + croissance progressive, n'importe quel hébergeur mutualisé "WordPress" suffit. Top 3 français/EU :

| Hébergeur    | Plan d'entrée WP | Datacenter | Notes                                                                  |
|--------------|------------------|------------|------------------------------------------------------------------------|
| **Infomaniak** | ~9 €/mois HT     | Suisse     | RGPD, énergie renouvelable, support FR de qualité. Cohérent éco-Re-Watt. |
| **OVHcloud** | ~6 €/mois HT     | France     | Hébergeur historique français, plans WordPress dédiés                  |
| **o2switch**  | ~7 €/mois TTC    | France     | Offre unique illimitée, support FR                                     |

**Recommandation** : **Infomaniak** (label énergie renouvelable, RGPD béton, support FR rapide). OVH si tu préfères 100 % français.

### 1.3 Toi-même ou prestataire ?

| Profil                                              | Voie recommandée                          | Temps      | Budget                |
|-----------------------------------------------------|-------------------------------------------|------------|-----------------------|
| Non-tech, veux que ça soit fait vite et bien        | **Freelance WordPress**                   | 1–2 semaines | 700–1500 € HT         |
| Tech-curieuse, OK pour passer 2 weekends dessus      | **DIY avec un builder no-code** (Elementor / Kadence) | 8–15 h     | Coût hébergement seul |
| Veux un design 100 % sur mesure + futur catalogue   | **Agence ou freelance senior**            | 3–5 semaines | 2000–5000 € HT       |

**Pour Re-Watt** : la landing actuelle est simple, le contenu est déjà rédigé et les specs sont dans [`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md). Un **freelance WordPress confirmé** te livre ça en **1 semaine pour ~800–1000 € HT** sans surprise.

### 1.4 Constructeur de pages (page builder)

Si DIY ou si tu donnes une consigne au freelance :

| Outil               | Recommandé pour                           | Notes                                                       |
|---------------------|-------------------------------------------|-------------------------------------------------------------|
| **Gutenberg natif** | Stack moderne, perf max, longévité        | Block patterns, theme.json — courbe d'apprentissage légère  |
| **Elementor**        | Non-tech, glisser-déposer, plein d'options | Très populaire, plugins payants (~50 €/an Pro pour les forms) |
| **Bricks**          | Tech, perf, devs front                    | Licence one-shot ~80 €, moins populaire                     |

**Recommandation** : **Gutenberg natif + un thème block-ready** (Astra ou Kadence). Pas de plugin builder externe, plus rapide, plus pérenne, gratuit.

---

## 2. Préparatifs (avant d'installer WordPress)

À faire **avant** de toucher à WordPress, pour éviter les blocages plus tard.

### 2.1 Nom de domaine

- Vérifier si **`re-watt.fr`** est déjà acheté. Sinon, le réserver chez **Gandi** (~12 €/an) ou directement chez l'hébergeur choisi (souvent offert la 1re année).
- Si déjà acheté ailleurs : tu n'auras qu'à modifier les enregistrements DNS au moment de la bascule (cf. § 6).

### 2.2 Adresse e-mail `contact@re-watt.fr`

Aujourd'hui, les liens "Nous écrire" pointent tous vers `contact@re-watt.fr`. **Cette adresse doit fonctionner avant la mise en ligne WP** — sinon les visiteurs envoient dans le vide.

Trois options :

1. **Boîte e-mail incluse chez l'hébergeur** (Infomaniak, OVH, o2switch en proposent toutes). Le plus simple.
2. **Google Workspace** (~6 €/mois/utilisateur) si tu veux Gmail + Drive + Meet pro.
3. **Microsoft 365 Business Basic** (~6 €/mois) si plus à l'aise avec Outlook.

**Pour démarrer** : option 1 (gratuite, incluse dans l'hébergement).

### 2.3 Assets prêts

Tout est déjà rassemblé dans [`/assets/`](./assets/) du dépôt actuel. À uploader tel quel dans la Media Library de WordPress :
- `logo-rewatt.png`, `favicon.png`, `apple-touch-icon.png`, `picto-laureat.png`, `logo-rcube.jpg`, `logo-gsm-master.png`

À générer **avant la mise en ligne** : une image **Open Graph 1200×630 px** (`og-image.png`) pour le partage sur réseaux sociaux. Canva fait ça en 5 min.

### 2.4 Contenu (déjà prêt)

Tous les textes de la landing sont dans [`index.html`](./index.html) et le détail dans [`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md). Rien à rédiger.

À rédiger en parallèle de la migration :
- **Mentions légales** complètes (raison sociale, RCS, hébergeur final, etc.) — le placeholder actuel ne suffira pas.
- **Politique de confidentialité** au sens RGPD — version WordPress, avec liste réelle des cookies déposés par les plugins choisis.

---

## 3. Calendrier-type (semaine de migration)

| Jour    | Étapes                                                            | Temps   |
|---------|--------------------------------------------------------------------|---------|
| **J-7** | Choix hébergeur + achat hébergement + DNS du domaine               | 30 min  |
| **J-7** | Création de l'e-mail `contact@re-watt.fr`                          | 15 min  |
| **J-6** | Installation WordPress (1-click chez l'hébergeur)                  | 10 min  |
| **J-5** | Installation thème (Astra ou Kadence) + plugins essentiels (§ 5)   | 1 h     |
| **J-4** | Reproduction de la home page (cf. § 4)                             | 3–6 h   |
| **J-3** | Pages mentions légales + politique de confidentialité              | 1–2 h   |
| **J-3** | Formulaire de contact (Fluent Forms / WPForms)                     | 1 h     |
| **J-2** | Tests responsive, accessibilité, formulaire, mailto                | 1 h     |
| **J-1** | Configuration SEO (Yoast/Rank Math), sitemap, robots.txt           | 30 min  |
| **J-1** | Bandeau cookies CNIL (Complianz ou Tarteaucitron) configuré        | 1 h     |
| **J0**  | Bascule DNS du domaine vers WP, `noindex` sur GitHub Pages         | 15 min  |
| **J+1** | Vérifications post-bascule, soumission Google Search Console       | 30 min  |

**Total temps de travail réel** : ~12–18 h, sur ~1 semaine en élapsé.

---

## 4. Reproduire la landing dans WordPress

L'objectif : reproduire à l'identique la version statique. Toutes les specs sont dans [`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md) (palette, typo, breakpoints, comportements). Voici le mode opératoire pratique.

### 4.1 Configurer les couleurs et la typo

Quel que soit le thème choisi, configurer ces variables une fois pour toutes via l'interface du thème (Personnaliser → Couleurs / Typographie) :

```
Couleur primaire   : #4CAF50  (vert Re-Watt)
Couleur secondaire : #2B82C9  (bleu Re-Watt)
Couleur texte      : #2B2B2B  (anthracite)
Couleur texte muted: #5C5C5C  (gris)
Couleur fond       : #FAFAF7  (off-white)
Police             : Inter (Google Fonts)
Poids              : 400 / 500 / 700 / 800
```

Avec un thème block-ready (Astra/Kadence), ces valeurs se retrouvent ensuite dans tous les blocs Gutenberg en un clic.

### 4.2 Construire la page d'accueil

7 blocs dans l'ordre, exactement comme dans [`index.html`](./index.html) :

| # | Bloc                          | Type Gutenberg suggéré                                      |
|---|-------------------------------|-------------------------------------------------------------|
| 1 | Hero "Le saviez-vous ? 80 %"  | Bloc *Cover* ou *Group* avec 4 paragraphes empilés          |
| 2 | Mission (aplat bleu)          | Bloc *Group* avec couleur de fond `--bleu-rewatt`           |
| 3 | Promesse (4 verbes)           | Bloc *Paragraph* centré, couleur vert                       |
| 4 | "Vous êtes…" (4 cartes)       | Bloc *Columns* × 4 ou bloc *Cover* × 4 en grid              |
| 5 | Partenaires (3 colonnes)      | Bloc *Columns* × 3, chaque colonne contient image + texte   |
| 6 | Footer                        | Footer du thème, à configurer dans le Personnaliser         |
| 7 | Header sticky                 | Header du thème, à configurer dans le Personnaliser         |

Pour les **détails de chaque bloc** (textes, tailles de police exactes, comportements, mailto), suivre § 4 du `DESIGN-HANDOFF.md`.

### 4.3 Formulaire de contact (remplacer les mailto:)

Plugin recommandé : **Fluent Forms** (gratuit, RGPD-friendly) ou **WPForms Lite**.

Champ par champ :

| Champ       | Type        | Obligatoire | Notes                                                              |
|-------------|-------------|-------------|--------------------------------------------------------------------|
| Vous êtes   | Liste déroulante | Oui    | Options : Particulier / Professionnel / Partenaire / Écosystème     |
| Prénom Nom  | Texte simple | Oui        |                                                                    |
| E-mail      | E-mail       | Oui        |                                                                    |
| Téléphone   | Téléphone    | Non        |                                                                    |
| Sujet       | Texte simple | Non        | Pré-rempli selon "Vous êtes…" (cf. tableau dans DESIGN-HANDOFF § 4.5) |
| Message     | Textarea     | Oui        |                                                                    |
| Consentement RGPD | Case à cocher | Oui    | "J'accepte que mes données soient utilisées pour traiter ma demande." |

**Notification e-mail** : à envoyer vers `contact@re-watt.fr` à chaque soumission, avec dans le sujet `[Re-Watt] Demande {profil} — {prénom}`.

---

## 5. Plugins WordPress essentiels

À installer **dans cet ordre**, après l'installation de WordPress et du thème.

| Plugin                | Rôle                                  | Gratuit ?         | Note                                          |
|-----------------------|---------------------------------------|-------------------|-----------------------------------------------|
| **Rank Math**         | SEO (titres, sitemap, OG)             | Oui (free version) | Plus moderne que Yoast                        |
| **Solid Security** ou **Wordfence** | Sécurité de base       | Oui               | Choisir un seul                               |
| **WP Super Cache** ou cache de l'hébergeur | Cache et perfs   | Oui               | LiteSpeed Cache si l'hébergeur est LS         |
| **Fluent Forms**      | Formulaire de contact                 | Oui               | Alternative : WPForms Lite                    |
| **Complianz**          | Bandeau cookies CNIL                  | Oui (free)        | Génère automatiquement la cookie policy       |
| **UpdraftPlus**       | Sauvegardes automatiques              | Oui (free)        | Backup hebdo vers Dropbox/Google Drive        |
| **OMGF**              | Auto-héberger Google Fonts            | Oui               | Évite le call externe → mieux RGPD            |

**Total : ~7 plugins, tous gratuits**.

À NE PAS installer (sinon site lent ou conflits) :
- Plus d'un plugin de cache à la fois
- Plus d'un plugin de sécurité à la fois
- Jetpack (sauf besoin spécifique, c'est lourd)
- Plugins de "stats" type WP Statistics si déjà Rank Math + GA — choisir un seul outil d'audience

---

## 6. Bascule DNS / mise en ligne (J0)

Le jour J de la mise en ligne, l'ordre des opérations compte.

### 6.1 Préparer le site WordPress

- Le site est complet en pré-prod (URL temporaire de l'hébergeur, ex. `re-watt.infomaniakwp.com`).
- Toutes les pages sont rédigées.
- Le formulaire fonctionne (envoyer un test à `contact@re-watt.fr`).
- Lighthouse : Performance > 80, Accessibilité > 90, SEO > 95.

### 6.2 Mettre l'ancien GitHub Pages en `noindex`

Avant la bascule, modifier `index.html` du dépôt actuel pour ajouter dans le `<head>` :

```html
<meta name="robots" content="noindex, follow">
```

Push + GitHub Pages rebuild. Ainsi quand Google viendra réindexer après la bascule, il ne risque pas d'indexer en double.

### 6.3 Changer les DNS du domaine

Chez le registrar du domaine `re-watt.fr` (Gandi / OVH / etc.) :

- Modifier les enregistrements DNS pour pointer vers l'hébergeur WordPress.
- Typiquement :
  - Enregistrement A `@` → IP du serveur WP
  - Enregistrement A `www` → IP du serveur WP (ou CNAME `@`)
- **Propagation** : 1–48 h selon FAI. Pendant ce temps, certaines personnes verront encore l'ancien site GitHub Pages.

### 6.4 Activer HTTPS

L'hébergeur fournit un certificat **Let's Encrypt gratuit** activable en 1 clic. **Indispensable** pour le SEO et la confiance.

### 6.5 Désactiver GitHub Pages (optionnel)

Une fois le DNS propagé, tu peux désactiver GitHub Pages dans les settings du dépôt `re-watt-landing-v2`. Garde le dépôt comme archive du code source.

---

## 7. Checks post-mise en ligne

### J0 (jour de la bascule)

- [ ] La home s'affiche correctement sur Chrome / Firefox / Safari
- [ ] Le formulaire envoie bien un e-mail à `contact@re-watt.fr`
- [ ] Les 4 mailto / dropdowns du formulaire fonctionnent pour les 4 profils
- [ ] Le bandeau cookies apparaît sur 1re visite et persiste après choix
- [ ] HTTPS est actif (cadenas vert dans la barre d'adresse)
- [ ] Les liens externes (LinkedIn, YouTube, RCube, GSM Master, pitch Lauréat) ouvrent dans un nouvel onglet
- [ ] Le bouton "Back to top" apparaît après 400 px de scroll

### J+1

- [ ] Test sur mobile réel (iPhone + Android)
- [ ] Test du burger menu mobile
- [ ] Test responsive 320 / 375 / 768 / 1024 / 1440 px
- [ ] Soumission du **sitemap.xml** à Google Search Console
- [ ] Vérifier que **`re-watt.fr/sitemap_index.xml`** est généré par Rank Math
- [ ] Vérifier qu'il n'y a pas d'erreurs JS dans la console
- [ ] Audit Lighthouse complet (Performance, Accessibilité, SEO, Best Practices)

### J+7

- [ ] Vérifier que Google a commencé à indexer la nouvelle URL (`site:re-watt.fr` dans Google)
- [ ] Vérifier qu'il n'y a pas d'erreurs dans Search Console
- [ ] Premier compteur de visites (Rank Math Analytics ou Plausible)
- [ ] Sauvegarde automatique fonctionne (UpdraftPlus → check de l'historique)

---

## 8. Coûts mensuels / annuels prévisionnels

| Poste                         | Coût annuel    | Note                                        |
|-------------------------------|----------------|---------------------------------------------|
| Nom de domaine `re-watt.fr`    | ~12 € / an     | Gandi ou inclus 1re année chez l'hébergeur  |
| Hébergement WordPress         | ~100 € / an    | Infomaniak plan WordPress de base           |
| Boîte mail `contact@re-watt.fr` | 0 €            | Incluse dans l'hébergement                  |
| Plugins (tous gratuits)       | 0 €            | Cf. § 5                                     |
| Sauvegardes (UpdraftPlus free)| 0 €            | Vers Dropbox / Google Drive perso           |
| **TOTAL**                     | **~110 € / an** | Soit ~9 €/mois                              |

Si tu prends un **freelance** pour la migration : **+ 800–1500 € one-shot**.

Si tu prends ensuite un **contrat de maintenance** WordPress avec un freelance ou agence : **~30–80 €/mois** (mises à jour, sauvegardes vérifiées, support).

---

## 9. Si tu as besoin d'aide

- Pour aller plus loin sur les specs visuelles : ouvrir [`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md).
- Pour briefer un freelance : ouvrir [`BRIEF-PRESTATAIRE.md`](./BRIEF-PRESTATAIRE.md).
- Pour reproduire un détail visuel précis : ouvrir [`index.html`](./index.html) en local et inspecter avec les outils de dev du navigateur.
