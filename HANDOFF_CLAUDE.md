# Spring Vision Studio — Handoff Claude

Ce document permet à une nouvelle instance de Claude de reprendre le développement
du site Spring Vision Studio sans perte de contexte.

---

## Contexte client

**Client :** Fakri
**Projet :** Site web de Spring Vision Studio
**Type :** Maison de production cinématographique, Paris 8ème
**Email :** infos@springvision.studio
**Domaine :** springvision.studio
**Instagram :** https://www.instagram.com/spring.vision.studio
**LinkedIn :** https://www.linkedin.com/company/spring-vision-studio/

---

## Identité de marque

- **Positionnement :** "Maison de production" — jamais "agence" ni "prestataire"
- **Ton :** prestige, littéraire, architectural — sans emojis, sans amateurisme
- **Palette :** `--ink:#020202` / `--paper:#ECE7DE` / `--spring:#B5FF35` (vert spring = seul accent)
- **Polices :** Cormorant Garamond (titres) + Barlow Condensed (labels) + Space Mono (corps)
- **Langue par défaut :** Français (avec toggle FR|EN dans la nav)
- **L'anglais est business haut de gamme** — ex: "Schedules held. Deadlines met." / "Bespoke teams"

---

## Architecture technique

- **Single-file HTML** — tout intégré (CSS + JS + traductions dans index.html)
- **Pas de framework** — vanilla JS uniquement
- **Bilingue** via objet `T = { fr: {...}, en: {...} }` et fonction `applyLang(l)`
- **Éléments data-k** → texte traduit / **data-k-ph** → placeholder traduit
- **Sections dynamiques** rebuildées par fonctions : `buildServices()`, `buildPromesse()`, `buildProcess()`, `buildOtTabs()`, `buildMoods()`, `buildAR()`, `buildFooter()`, `buildPrestTags()`

---

## Fonctionnalités en place

### Navigation
- Menu fullscreen burger avec animation clip-path
- Toggle FR|EN dans la nav (visible tous formats)
- Cursor custom (anneau lag + point vert) désactivé sur tactile
- Smooth scroll

### Sections
- Hero avec background Vimeo (placeholder `VOTRE_VIDEO_ID`)
- Showreel Vimeo lazy-load au clic (placeholder `VOTRE_SHOWREEL_ID`)
- Section Vision / Services (6 cartes scroll horizontal) / Engagements (6 cartes)
- Manifeste central
- **Section Références** (id="projets") — 3 cartes avec placeholders pr1/pr2/pr3
- Méthode (4 étapes)

### Outils & Studio (6 gadgets dans tabs)
1. **Estimateur de budget** — calcul auto au chargement, select + sliders + radio groups, tarifs CCNPF
2. **Calendrier de production** — timeline inversée à partir date de livraison
3. **Formats cinéma** — 8 formats, clic = description + visualisation
4. **Sélecteur d'ambiance** — 9 palettes, direction photographique prédéfinie + enrichissement LUMIA
5. **Heure dorée · Monde** — 90+ capitales, calcul solaire temps réel, filtres continent + recherche
6. **Rejoindre le studio** — formulaire prestataires → Formspree

### LUMIA (Brief IA)
- Nom propriétaire pour l'IA — aucune mention de Claude/Anthropic côté utilisateur
- Clé intégrée en dur dans `var LUMIA_KEY = '__LUMIA_KEY__'`
- Modèle utilisé : `claude-opus-4-5`
- Prompt en FR et EN selon langue active

### Formulaires (Formspree)
- Contact → endpoint `https://formspree.io/f/__FORMSPREE_CONTACT__`
- Prestataires → endpoint `https://formspree.io/f/__FORMSPREE_PREST__`
- États : sending / sent / error avec fallback email

### RGPD & Légal
- Bannière consent (localStorage `svs-consent`) apparaît après 1,8s
- Modal mentions légales complet (éditeur, PI, données, cookies)
- Liens légaux dans footer avec `href="legal"` interceptés en JS

### SEO
- meta og:title, og:description, og:image, og:locale
- twitter:card
- canonical href
- JSON-LD schema.org Organization

---

## Placeholders à remplacer avant déploiement

| Placeholder | Valeur à mettre | Où obtenir |
|---|---|---|
| `__LUMIA_KEY__` | Clé API Anthropic `sk-ant-…` | console.anthropic.com |
| `__FORMSPREE_CONTACT__` | ID formulaire contact | formspree.io |
| `__FORMSPREE_PREST__` | ID formulaire prestataires | formspree.io |
| `VOTRE_VIDEO_ID` | ID vidéo Vimeo (hero bg) | URL Vimeo |
| `VOTRE_SHOWREEL_ID` | ID showreel Vimeo | URL Vimeo |

---

## Ce qui reste à faire (priorisé)

### Priorité haute
- [ ] Remplacer les 3 projets placeholder par de vrais projets (section Références)
- [ ] Intégrer vidéos Vimeo (hero + showreel)
- [ ] Configurer Formspree (2 formulaires) et tester la réception email
- [ ] Remplacer `__LUMIA_KEY__` par la vraie clé Anthropic

### Priorité moyenne
- [ ] Ajouter une image `og-image.jpg` (1200×630px) pour le SEO social
- [ ] Ajouter `logo.png` pour le JSON-LD
- [ ] Vérifier mentions légales (numéro SIRET si société enregistrée)

### Priorité basse
- [ ] Ajouter canal Vimeo dans footer (icône déjà retirée faute de lien)
- [ ] Ajouter Google Analytics ou Plausible si tracking souhaité
- [ ] Proxy serveur pour sécuriser la clé LUMIA (Netlify Functions ou Cloudflare Worker)

---

## Préférences de travail de Fakri

- Exige la qualité **Maison** — jamais commercial/générique
- L'anglais doit être **business haut de gamme** — pas d'anglais banal
- Préfère les sections dynamiques pour faciliter les mises à jour
- Sensible à la terminologie : "Maison" pas "agence", "partenaires créatifs" pas "prestataires"
- La clé API LUMIA appartient à Fakri — les clients ne doivent jamais savoir que c'est Claude

---

## Historique des sessions précédentes

**Session 1 :** Construction du site Spring Vision Studio complet (Spring Green, Cormorant, dark luxury)
**Session 2 :** Ajout des 6 gadgets (budget, planning, aspect ratios, mood, golden hour, prestataires)
**Session 3 :** Gadget Heure Dorée étendu à 90+ capitales mondiales avec filtres et recherche
**Session 4 :** Système bilingue FR/EN complet avec toggle nav
**Session 5 :** Branding LUMIA (suppression mentions Claude/Anthropic), clé hardcodée, formulaires Formspree, SEO, RGPD, section Références, fix mobile lang toggle, estimation budget auto

---

## Comment reprendre le travail

1. Charger `index.html` dans la conversation
2. Lire ce document HANDOFF_CLAUDE.md
3. Demander la modification souhaitée
4. Claude modifie le fichier et le restitue

Pour les modifications complexes (refonte section, ajout fonctionnalité), utiliser
Python pour les remplacements de chaînes — éviter les éditions inline sur un fichier >150KB.
