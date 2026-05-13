# Re-Watt — Comment coller la landing dans WordPress

Guide pour quelqu'un qui n'a **jamais** utilisé WordPress. Objectif : avoir le site en ligne en **30 minutes**, par copier-coller, sans toucher au code PHP, FTP ou autre chose qui fait peur.

> 📦 Tous les fichiers à coller sont dans le dossier [`wordpress-paste/`](./wordpress-paste/) du dépôt.

---

## Vue d'ensemble

Tu vas faire ça :

1. Acheter un hébergement WordPress (10 min)
2. Installer WordPress (5 min — c'est en 1 clic)
3. Installer un thème léger (5 min)
4. Créer **2 pages** dans WordPress et coller du HTML dedans (10 min)
5. Régler ta page d'accueil et publier (2 min)

C'est tout. Pas de code à écrire. Pas de FTP.

---

## Étape 1 — Acheter l'hébergement

### 1.1 Aller chez un hébergeur français/européen

Je te recommande **Infomaniak** (Suisse, RGPD, énergie renouvelable, cohérent avec Re-Watt) ou **OVH** (français historique).

- **Infomaniak — Hébergement Web "Starter" WordPress** : ~9 €/mois HT, inclut domaine + e-mail. Lien direct : <https://www.infomaniak.com/fr/hebergement/hebergement-web>
- **OVH — Plan "Personal"** : ~3,59 €/mois HT, domaine inclus 1 an. Lien : <https://www.ovhcloud.com/fr/web-hosting/>

### 1.2 Choix de l'offre

Prends une formule qui propose **WordPress en 1 clic** (presque toutes le font). Demande à inclure :
- Le **domaine** `re-watt.fr` (vérifier qu'il est libre, ou utiliser celui que tu possèdes déjà)
- Au moins **1 boîte e-mail** (`contact@re-watt.fr`)
- **HTTPS gratuit** (Let's Encrypt — c'est inclus partout maintenant)

### 1.3 Paye, valide

Tu reçois un e-mail de confirmation avec :
- Une URL d'admin (du type `re-watt.fr/wp-admin` ou une URL temporaire si le DNS n'est pas encore propagé)
- Un identifiant et un mot de passe

---

## Étape 2 — Installer WordPress (1 clic)

Sur l'espace client de ton hébergeur :

- Onglet **"Sites Web"** ou **"Hébergements"**
- Bouton **"Installer WordPress"** ou **"Installation automatique"**
- Choisir le domaine : `re-watt.fr` (ou la sous-version temporaire)
- Suivre l'assistant — il te demande un nom de site (« Re-Watt »), un e-mail admin, un mot de passe admin

**Sur Infomaniak** : Manager → ton hébergement → Sites Web → Installer une application → WordPress. C'est balisé.

À la fin tu arrives sur **`tonsite/wp-admin`** avec ton login. Tu vois le **tableau de bord WordPress** — c'est l'écran d'administration.

---

## Étape 3 — Installer un thème simple

### 3.1 Aller dans Apparence > Thèmes

Sur le tableau de bord WordPress (à gauche) : **Apparence** → **Thèmes** → bouton **"Ajouter"**.

### 3.2 Chercher et installer Astra

Dans la barre de recherche en haut à droite, taper **"Astra"**. Le thème **Astra** (par Brainstorm Force) apparaît. Clique **Installer** puis **Activer**.

> ✅ Pourquoi Astra : c'est le thème WordPress gratuit le plus populaire au monde, ultra-léger, et il propose un **modèle de page vierge** dont on a besoin. Si tu préfères, **Kadence** ou **GeneratePress** marchent pareil.

---

## Étape 4 — Créer la page d'accueil

### 4.1 Aller dans Pages > Ajouter

Menu de gauche : **Pages** → **Ajouter** (bouton en haut).

### 4.2 Titre de la page

Tape **« Accueil »** comme titre. Ne tape rien d'autre dans la zone principale pour l'instant.

### 4.3 Choisir le modèle "Plein largeur / Vierge"

À droite du Block Editor, dans la barre latérale (colonne "Document") :

- Section **"Modèle"** ou **"Template"**
- Choisir **"Astra — Vide / Blank Container"** (ou équivalent : "Conteneur vide", "Full Width / Plain")

C'est crucial : ce modèle retire le titre de la page et toute la chrome du thème (en-tête, pied de page, sidebars). On veut une page vide pour y mettre TOUT notre HTML.

### 4.4 Ajouter un bloc "HTML personnalisé"

Clique le **+** au centre de la zone de contenu. Une fenêtre liste tous les types de blocs. Cherche **"HTML personnalisé"** (en anglais : *Custom HTML*). Clique-le.

### 4.5 Coller le contenu

Ouvre le fichier **[`wordpress-paste/page-accueil.html`](./wordpress-paste/page-accueil.html)** du dépôt. Sélectionne **tout** (Cmd+A / Ctrl+A) et copie. Reviens sur WordPress et colle dans la zone du bloc HTML.

> 💡 Tu peux ouvrir le fichier `.html` directement sur GitHub via cette URL : <https://github.com/laetitiaperson/re-watt-landing-v2/blob/main/wordpress-paste/page-accueil.html>
>
> Clique sur le bouton **"Raw"** en haut à droite du fichier, puis Cmd+A / Ctrl+A pour tout sélectionner et copier.

### 4.6 Publier

Bouton **"Publier"** en haut à droite. Confirme.

Tu peux maintenant cliquer **"Voir la page"** : tu vois ta landing 🎉

---

## Étape 5 — La déclarer comme page d'accueil

Par défaut, WordPress affiche la liste des derniers articles sur l'accueil. On veut afficher notre page "Accueil" à la place.

### Réglages > Lecture

Menu de gauche : **Réglages** → **Lecture**.

Section **"La page d'accueil affiche"** :
- Sélectionner **"Une page statique"**
- **Page d'accueil** : choisir **"Accueil"** dans le menu déroulant
- Laisser **"Page des articles"** vide

Bouton **"Enregistrer les modifications"** en bas.

✅ Maintenant `https://re-watt.fr` affiche la landing directement.

---

## Étape 6 — Créer la page Mentions légales

Même procédure que pour l'Accueil :

1. **Pages > Ajouter**
2. Titre : **"Mentions légales"**
3. Vérifier que l'URL (permalien) est bien `mentions-legales` — c'est important pour que le lien du footer fonctionne.
4. Modèle : **"Vide / Blank Container"** (comme pour l'Accueil)
5. Ajouter un bloc **"HTML personnalisé"**
6. Coller le contenu du fichier **[`wordpress-paste/page-mentions-legales.html`](./wordpress-paste/page-mentions-legales.html)**
7. **Publier**

---

## Étape 7 — Uploader les images (optionnel mais propre)

Pour l'instant, les images de la landing pointent vers **GitHub Pages** (`https://laetitiaperson.github.io/re-watt-landing-v2/assets/...`). Ça marche, mais c'est temporaire : le jour où tu désactives GitHub Pages, les images casseront.

### Pour rendre les images permanentes sur WP :

1. **Médias > Bibliothèque** > **Ajouter**.
2. Glisse-dépose ces 7 fichiers depuis ton ordinateur (présents dans le dossier `assets/` du dépôt si tu l'as cloné, ou téléchargeables depuis GitHub) :
   - `logo-rewatt.png`
   - `picto-laureat.png`
   - `logo-rcube.jpg`
   - `logo-gsm-master.png`
   - `favicon.ico`
   - `favicon-512.png`
   - `apple-touch-icon.png`
3. Une fois uploadés, clique sur chaque image et copie l'URL fournie par WP (du type `https://re-watt.fr/wp-content/uploads/2026/05/logo-rewatt.png`).
4. Retourne sur **Pages > Accueil > Modifier**, ouvre le bloc HTML personnalisé.
5. Fais un **Rechercher & Remplacer** (Cmd+F / Ctrl+F dans le bloc) :
   - Chercher : `https://laetitiaperson.github.io/re-watt-landing-v2/assets/`
   - Remplacer par : `https://re-watt.fr/wp-content/uploads/2026/05/` (adapter l'année/mois selon l'URL réelle)
6. **Mettre à jour** la page.

---

## Étape 8 — Plugins essentiels (15 minutes)

Sur le tableau de bord, menu **Extensions > Ajouter**. Pour chaque plugin ci-dessous : taper son nom, **Installer**, **Activer**.

| Plugin            | À quoi ça sert                                  |
|-------------------|-------------------------------------------------|
| **Rank Math**     | SEO (titres, sitemap, partage social)           |
| **Solid Security**| Sécurité de base, brute-force, scan             |
| **UpdraftPlus**   | Sauvegardes automatiques (vers Drive/Dropbox)   |
| **Complianz**     | Bandeau cookies CNIL (au cas où tu actives plus tard analytics ou embeds vidéo) |

Pour l'instant, **inutile d'installer un plugin formulaire** : la landing a déjà 4 cartes `mailto:` qui ouvrent le client mail des visiteurs. Plus tard, si tu veux un vrai formulaire, ajoute **Fluent Forms** ou **WPForms Lite**.

---

## Étape 9 — Configurer les favicons

WordPress veut son propre favicon dans les réglages :

1. **Apparence > Personnaliser**.
2. Section **"Identité du site"**.
3. **Icône du site** : uploader le fichier `favicon-512.png` (depuis ton ordi).
4. **Enregistrer**.

Le favicon dans le HTML pasté reste valide aussi — c'est redondant mais ça ne pose pas de problème.

---

## Étape 10 — Brancher le DNS si besoin

Si tu as acheté le domaine `re-watt.fr` **ailleurs** que chez ton hébergeur WP (par exemple chez Gandi), tu dois pointer les DNS :

- Aller chez ton registrar de domaine (Gandi, OVH…)
- Section **DNS**
- Modifier ou ajouter l'enregistrement **A** :
  - Type **A**, nom `@`, valeur = IP du serveur WP (fournie par ton hébergeur)
  - Type **A**, nom `www`, valeur = même IP
- Sauvegarder. **Propagation 1–48h.**

Si tu as acheté le domaine **chez l'hébergeur WP**, il branche tout automatiquement.

---

## Que faire après ?

- **Tester** sur mobile, tablette, ordinateur. Le `Custom HTML` rend le HTML/CSS/JS tel quel — tout doit fonctionner exactement comme la version GitHub Pages actuelle.
- **Compléter les Mentions légales** (le placeholder est très vide).
- **Pour aller plus loin** : remplacer les liens `mailto:` par un vrai formulaire (plugin Fluent Forms), activer un analytics respectueux (Plausible ou Matomo), basculer les images vers la Media Library WP.

---

## En cas de problème

### "Le HTML personnalisé ne s'affiche pas comme attendu"

- Vérifie que tu as bien collé le contenu **complet** du fichier `.html` (de la 1re ligne à la dernière).
- Vérifie le modèle de page : doit être **"Vide / Blank Container"** (sinon le thème ajoute son propre header par-dessus et ça fait doublon).
- Si le `<script>` est bloqué : certains hôtes managés strippent les scripts pour les comptes non-admin. **Assure-toi que tu es connectée en compte Administrateur**.

### "Les images ne s'affichent pas"

- Vérifie ta connexion internet — les images pointent par défaut vers GitHub Pages.
- Si tu as fait l'étape 7 (upload vers Media Library), vérifie que tu n'as pas oublié de mettre à jour les URLs dans le bloc HTML.

### "Le bandeau cookies réapparaît à chaque visite"

- Normal : `localStorage` est par origine. Tant que tu testais sur GitHub Pages et que tu visites désormais sur `re-watt.fr`, c'est un nouveau domaine donc bandeau remis à zéro. Une fois sur `re-watt.fr`, le choix est mémorisé 13 mois.

### "J'ai besoin d'aide"

- Documentation officielle WordPress en français : <https://fr.wordpress.org/support/>
- Documentation Astra : <https://wpastra.com/docs/>
- Si tu décides de prendre un freelance malgré tout : reviens me voir, je te fais un brief.
