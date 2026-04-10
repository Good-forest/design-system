# goodforest — Design System

Référence visuelle et technique de la charte graphique goodforest. Document vivant, mis à jour à chaque évolution du produit.

## Ce que contient ce repo

| Fichier | Rôle |
|---------|------|
| `index.html` | Design system interactif — prévisualisation live dans le navigateur |
| `DESIGN_SYSTEM.md` | Spec technique pour implémentation IA (BMAD) |
| `img/` | Assets images utilisés dans les démos |

## Ouvrir le design system

Ouvrir `index.html` directement dans un navigateur. Aucun build, aucune dépendance à installer.

## Contenu

- **3 thèmes** — Light · Dark · Forest, switchables en live
- **Palette de marque** — 14 couleurs sources avec leur usage par thème
- **Tokens de thème** — CSS variables sémantiques (`--alertes`, `--accent`, `--t1`…)
- **Typographie** — Échelle Poppins complète avec responsive tokens
- **Composants** — Badges, boutons, inputs, KPI cards, tableaux, progress bars, toggles
- **Sévérité** — 4 niveaux Normal / À surveiller / À risque / Critique (FR · EN · DB)
- **Charts** — Référence Chart.js des 7 graphiques avec configs et rendus par thème
- **Map Pins** — Marqueurs SVG personnalisés (teardrop + arbre goodforest) avec clusters
- **Layout** — Grilles, espacements, patterns de navigation (Pill · Sidebar · Icon)
- **Glassmorphism** — Règles d'usage et exemples sur fond photo
- **CSS Variables** — Blocs `:root` prêts à copier

## Stack

Tailwind CSS · Poppins · Chart.js · HTML/CSS/JS vanilla — pas de framework, pas de build.

## Implémentation dans un projet

Lire `DESIGN_SYSTEM.md` — ce fichier contient tous les tokens, composants et configurations nécessaires pour déployer la charte dans une app Vue 3 / React / autre.
