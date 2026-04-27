# Spring Vision Studio — Guide de déploiement

## Fichiers dans ce package
- `index.html` — Site complet (single-file, tout intégré)
- `DEPLOIEMENT.md` — Ce guide
- `HANDOFF_CLAUDE.md` — Contexte pour continuer le développement avec Claude

---

## Avant de déployer — 3 remplacements obligatoires

Ouvrir `index.html` dans un éditeur de texte (VS Code recommandé) et faire les remplacements suivants :

### 1. Clé LUMIA (IA Brief)
Chercher : `__LUMIA_KEY__`
Remplacer par : votre clé Anthropic `sk-ant-…`
Obtenir la clé sur : https://console.anthropic.com → API Keys

### 2. Formulaire Contact (Formspree)
Chercher : `__FORMSPREE_CONTACT__`
Remplacer par : votre ID Formspree pour le formulaire contact
Créer sur : https://formspree.io → New Form → copier l'ID (8 caractères)

### 3. Formulaire Prestataires (Formspree)
Chercher : `__FORMSPREE_PREST__`
Remplacer par : votre ID Formspree pour le formulaire prestataires
(Créer un second formulaire distinct sur Formspree)

### 4. Vidéos Vimeo (optionnel mais recommandé)
Chercher : `VOTRE_VIDEO_ID` → ID de la vidéo background hero
Chercher : `VOTRE_SHOWREEL_ID` → ID du showreel cliquable
Les IDs se trouvent dans l'URL Vimeo : vimeo.com/**123456789**

---

## Déploiement sur Netlify (recommandé — gratuit)

1. Aller sur https://netlify.com
2. "Add new site" → "Deploy manually"
3. Glisser-déposer le fichier `index.html` dans la zone de dépôt
4. Le site est en ligne en 30 secondes
5. Pour un domaine personnalisé : Site settings → Domain management → Add custom domain

**Domaine recommandé déjà configuré dans le code :** `springvision.studio`

---

## Déploiement sur Vercel (alternative)

```bash
npm i -g vercel
vercel --prod
```

---

## Contenu à remplacer avant lancement client

Dans la section "Références" (section id="projets"), remplacer :
- `data-k="pr1_title"` / `pr2_title` / `pr3_title` → vrais titres de projets
- `data-k="pr1_fmt"` / `pr2_fmt` / `pr3_fmt` → vrais formats
- Couleurs de fond des `.proj-thumb` → vraies images ou gradients

---

## Structure du site (sections dans l'ordre)

1. Hero — background Vimeo + titre animé
2. Showreel — player Vimeo au clic
3. Vision — manifeste fondateur + 6 piliers
4. Services — 6 cartes horizontal scroll
5. Engagements — 6 promesses
6. Manifeste — citation centrale
7. Références — 3 projets (placeholders)
8. Méthode — 4 étapes de production
9. Outils & Studio — 6 gadgets interactifs
10. LUMIA Brief IA — générateur de brief
11. Contact — formulaire Formspree
12. Footer + mentions légales + RGPD

---

## Notes techniques

- Single-file HTML — aucune dépendance externe sauf Google Fonts et Formspree
- Polices : Cormorant Garamond + Barlow Condensed + Space Mono (Google Fonts)
- Bilingue FR/EN — toggle dans la nav, langue mémorisée en localStorage
- Responsive — desktop / tablet / mobile
- Cursor custom désactivé automatiquement sur écran tactile
- SEO : meta og, twitter card, JSON-LD schema.org intégrés
- RGPD : bannière consent + modal mentions légales

---

## Contact technique
infos@springvision.studio
