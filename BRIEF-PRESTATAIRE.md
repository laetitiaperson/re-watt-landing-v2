# Re-Watt — Brief intégration WordPress

> Document à transmettre à un·e prestataire freelance pour l'intégration de la landing Re-Watt sur WordPress. Remplace ou complète un cahier des charges.

---

## 1. Contexte

Re-Watt est une jeune société à mission dont l'objet est de **prolonger la durée de vie des batteries électriques amovibles** (vélos cargo, scooters, trottinettes, outils portatifs) par la réparation et le reconditionnement. Constat fondateur : 80 % des batteries envoyées au recyclage sont réparables.

Une landing one-pager statique a été développée en HTML/CSS/JS vanilla et déployée à titre transitoire sur GitHub Pages. Elle sert aujourd'hui de **maquette finalisée et de référence visuelle** pour la version WordPress à produire.

**Maquette de référence** : <https://laetitiaperson.github.io/re-watt-landing-v2/>
**Code source** : <https://github.com/laetitiaperson/re-watt-landing-v2>

---

## 2. Périmètre de la mission

Intégration d'une landing one-pager sur WordPress en reproduisant à l'identique la maquette de référence, avec :

- **7 sections** : header sticky, hero "80 %", mission, promesse, "Vous êtes…", partenaires, footer
- **Bouton flottant** "Back to top"
- **Bandeau de consentement cookies** + modal de personnalisation
- **2 pages secondaires** : mentions légales, politique de confidentialité (la trame est fournie)

Hors périmètre (sauf demande contraire à chiffrer) :
- Création d'un blog ou de catégories d'articles
- Espace membres / compte utilisateur
- Intégration e-commerce / WooCommerce
- Multilinguisme

---

## 3. Livrables attendus

1. Site WordPress fonctionnel sur l'hébergement Re-Watt (à choisir avec le client : Infomaniak ou OVH par défaut).
2. Pages : **Accueil**, **Mentions légales** (`/mentions-legales`), **Politique de confidentialité** (`/politique-confidentialite`).
3. **Formulaire de contact** unique remplaçant les 4 mailto actuels, avec dropdown "Vous êtes…" et notification vers `contact@re-watt.fr`.
4. **Bandeau cookies** conforme CNIL (Complianz ou équivalent).
5. **Plugins essentiels** configurés (SEO, sécurité, cache, sauvegardes — détail attendu à la livraison).
6. **Documentation de prise en main** : tutoriel court (3–5 pages PDF ou Notion) pour expliquer au client comment modifier les textes, l'e-mail destinataire, et ajouter une page.
7. Migration DNS et **mise en ligne** sur le domaine `re-watt.fr`.
8. **Tests** sur 4 navigateurs (Chrome / Firefox / Safari / Edge) et 3 viewports (mobile 375 px / tablette 768 px / desktop 1280 px).
9. **Audit Lighthouse** post-mise en ligne avec scores cibles : Perf > 80, A11y > 90, SEO > 95.

---

## 4. Spécifications visuelles et fonctionnelles

L'intégralité des spécifications (palette, typographie, tokens, structure des blocs, comportements interactifs, copy) figure dans :

📄 **[`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md)** — document de référence à lire en premier.

L'implémentation HTML/CSS/JS de référence est dans **[`index.html`](./index.html)** du dépôt. **La version WordPress doit reproduire ce rendu visuel au pixel près.**

### Quelques points critiques à respecter

- **Palette** : Bleu Re-Watt `#2B82C9`, Vert Re-Watt `#4CAF50` (extraits du PPTX de marque).
- **Police** : Inter (poids 400 / 500 / 700 / 800), idéalement auto-hébergée (plugin OMGF).
- **Hero** : le "80 %" doit s'afficher en très grand (clamp 6rem → 14rem), bleu Re-Watt, poids 800.
- **Mission** : aplat bleu pleine largeur avec texte blanc.
- **"Vous êtes…"** : 4 cartes cliquables (1 col mobile, 2 col tablette, 4 col desktop).
- **Partenaires** : 3 colonnes cliquables vers liens externes (Lauréat → pitch YouTube, RCube, GSM Master).
- **Footer** : LinkedIn + YouTube + mentions légales + lien "Politique de confidentialité" qui ouvre le modal cookies.
- **Bandeau cookies** : 3 boutons (Tout refuser / Personnaliser / Tout accepter), choix stocké 13 mois.

---

## 5. Spécifications techniques

| Exigence                  | Détail                                                                |
|---------------------------|-----------------------------------------------------------------------|
| CMS                        | WordPress (dernière version stable)                                   |
| Thème                      | Astra, Kadence, GeneratePress, ou block theme natif. Pas de Divi.     |
| Constructeur               | Gutenberg natif **ou** Elementor free. Pas de licence payante par défaut. |
| Hébergement                | Européen (Infomaniak / OVH / o2switch)                                |
| Base de données            | MySQL/MariaDB fournie par l'hébergeur                                 |
| HTTPS                      | Certificat Let's Encrypt activé                                       |
| Performances               | Lighthouse Performance > 80 sur mobile                                |
| Accessibilité              | WCAG 2.1 AA — outline focus visible, ARIA, contrastes, tap targets ≥ 44 px |
| Responsive                 | Fluide de 320 px à 1440 px+                                           |
| SEO                        | Yoast SEO **ou** Rank Math configuré, sitemap soumis à Search Console |
| RGPD                       | Bandeau cookies CNIL, formulaire avec case de consentement explicite  |
| Compatibilité              | Chrome / Firefox / Safari / Edge, 2 dernières versions                |

---

## 6. RGPD / accessibilité

Le client tient à un site éthique et conforme :

- **Bandeau cookies obligatoire** (la stack WP introduit nécessairement des cookies non essentiels selon les plugins).
- **Pas de tracking publicitaire**, pas de pixel Meta/LinkedIn.
- **Google Fonts** doit être auto-hébergée (plugin OMGF ou équivalent) pour éviter les appels US.
- **Politique de confidentialité réelle** à rédiger avec mention des plugins déposant des cookies (liste à fournir au client par le prestataire).
- **Mentions légales** à compléter avec les informations du prestataire (en tant qu'hébergeur logiciel) et celles de l'éditeur (le client fournit).
- **Accessibilité** : zones tactiles ≥ 44 px, focus visible au clavier, navigation au clavier sur l'ensemble du site, alt sur toutes les images, semantic HTML.

---

## 7. Calendrier

- **Devis attendu sous 5 jours ouvrés** après réception de ce brief.
- **Démarrage** : à convenir, idéalement dans les 2 semaines suivant la signature du devis.
- **Livraison** : entre 1 et 2 semaines après démarrage.
- **Mise en ligne et bascule DNS** : à convenir avec le client (créneau hors heures de bureau recommandé).

---

## 8. Modalités

### Demande de devis

Merci de fournir :

- **Tarif total HT** pour la mission complète, ou détail par lot.
- **Délai d'exécution** estimé.
- **Stack technique proposée** : thème, builder, plugins (avec versions et licences).
- **Référence(s) d'intégrations** comparables déjà réalisées (URLs).
- **Conditions de paiement** habituelles (acompte / solde).
- **Garantie post-livraison** (durée pendant laquelle les bugs sont corrigés gratuitement).
- **Maintenance optionnelle** (forfait mensuel / annuel).

### Sélection

Critères de choix par ordre d'importance :
1. **Compréhension du brief** et qualité du devis détaillé
2. **Références** comparables (one-pagers WordPress, plutôt que sites complexes)
3. **Localisation** : préférence pour un freelance français ou francophone
4. **Réactivité** sur la phase de devis
5. **Tarif** (à compétences équivalentes)

### Paiement

- **Acompte 30 %** à la signature du devis
- **Solde 70 %** à la livraison et validation du client (après tests)
- Facturation au choix : auto-entrepreneur, EURL, EI…

---

## 9. Contact

Pour toute question sur ce brief, ou pour transmettre votre devis :

**Re-Watt** — `contact@re-watt.fr`

---

## Annexes (fichiers fournis)

- [`DESIGN-HANDOFF.md`](./DESIGN-HANDOFF.md) — specs détaillées (palette, tokens, structure des 7 blocs, comportements, accessibilité, SEO)
- [`index.html`](./index.html) + [`/assets/`](./assets/) — version statique de référence avec tous les visuels exploitables
- [`mentions-legales.html`](./mentions-legales.html) — trame minimale, contenu à compléter
- [`MIGRATION-WORDPRESS.md`](./MIGRATION-WORDPRESS.md) — guide complet de migration côté client (à titre informatif, le prestataire n'a pas à le suivre, mais ça clarifie le contexte)
