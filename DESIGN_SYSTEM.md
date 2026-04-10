# goodforest — Design System Spec
> Document de référence pour déploiement automatisé par IA (technique BMAD).
> Lire ce fichier en entier avant d'écrire la moindre ligne de code.

---

## 1. Stack & setup

| Outil | Version | Note |
|-------|---------|------|
| Vue 3 + Vite | latest | Composition API |
| Tailwind CSS | v3 | Config étendue (voir §2) |
| Chart.js / vue-chartjs | 4.x | Tous les graphiques |
| Google Fonts | Poppins | 300/400/500/600/700/800 |

**Jamais de PNG pour les icônes.** Tout est SVG inline ou Tailwind. Pas de librairie d'icônes externe obligatoire — utiliser des SVG faits main (voir §8).

---

## 2. Tailwind config

```js
// tailwind.config.js
export default {
  darkMode: ['selector', '[data-theme="dark"]'],
  theme: {
    extend: {
      fontFamily: { sans: ['Poppins', 'sans-serif'] },
      colors: {
        gf: {
          400: '#34d399', // emerald-400 · forest accent
          500: '#10B981', // emerald-500 · light accent
          600: '#32D583', // cyan · dark accent
          950: '#0f1f12', // forest bg
        },
      },
    },
  },
}
```

**Règle absolue :** ne jamais hardcoder une couleur. Toujours utiliser `var(--xxx)` ou `bg-[var(--xxx)]`.

---

## 3. Système de thèmes

Le thème est contrôlé par `data-theme` sur `<html>`. Trois valeurs : `light` | `dark` | `forest`.

```html
<html lang="fr" data-theme="light">
```

### 3.1 CSS Variables — Light

```css
:root, [data-theme="light"] {
  --bg: #f5f7fa;
  --surface: #ffffff;
  --card: #ffffff;
  --cb: rgba(0,0,0,0.08);
  --nav: rgba(255,255,255,0.92);
  --t1: #1a1a1a;
  --t2: #525252;
  --t3: #a3a3a3;
  --primary: #10b981;
  --primary-txt: #ffffff;
  --accent: #10b981;
  --acs: rgba(16,185,129,0.1);
  /* Sévérité */
  --alertes: #ef4444;
  --alertes-s: rgba(239,68,68,0.1);
  --alertes-b: rgba(239,68,68,0.25);
  --anomalie: #f97316;
  --anomalie-s: rgba(249,115,22,0.1);
  --anomalie-b: rgba(249,115,22,0.25);
  --stress: #eab308;
  --stress-s: rgba(234,179,8,0.1);
  --stress-b: rgba(234,179,8,0.28);
  --normal: #10b981;
  /* Charts */
  --chart-forte: #ef4444;
  --chart-moy: #eab308;
  --chart-surf: #ff9500;
  --chart-bar: #10b981;
  /* UI */
  --sh: 0 2px 8px rgba(0,0,0,0.08);
  --shm: 0 4px 6px -1px rgba(0,0,0,0.2);
  --ibg: #f5f7fa;
  --grid-y: rgba(0,0,0,0.05);
  --tooltip-bg: #ffffff;
  --tooltip-border: #e5e7eb;
}
```

### 3.2 CSS Variables — Dark

```css
[data-theme="dark"] {
  --bg: #1a1a1a;
  --surface: #262626;
  --card: #262626;
  --cb: rgba(255,255,255,0.08);
  --nav: rgba(26,26,26,0.95);
  --t1: #ffffff;
  --t2: #a3a3a3;
  --t3: #525252;
  --primary: #e1fb15;
  --primary-txt: #1a1a1a;
  --accent: #32d583;
  --acs: rgba(50,213,131,0.12);
  /* Sévérité */
  --alertes: #f87171;
  --alertes-s: rgba(248,113,113,0.12);
  --alertes-b: rgba(248,113,113,0.3);
  --anomalie: #ff9500;
  --anomalie-s: rgba(255,149,0,0.12);
  --anomalie-b: rgba(255,149,0,0.3);
  --stress: #e1fb15;
  --stress-s: rgba(225,251,21,0.12);
  --stress-b: rgba(225,251,21,0.28);
  --normal: #32d583;
  /* Charts */
  --chart-forte: #f87171;
  --chart-moy: #eab308;
  --chart-surf: #ff9500;
  --chart-bar: #32d583;
  /* UI */
  --sh: 0 2px 8px rgba(0,0,0,0.4);
  --shm: 0 4px 6px -1px rgba(0,0,0,0.4);
  --ibg: #262626;
  --grid-y: rgba(255,255,255,0.05);
  --tooltip-bg: #262626;
  --tooltip-border: #404040;
}
```

### 3.3 CSS Variables — Forest

```css
[data-theme="forest"] {
  --bg: #0f1f12;
  --surface: #162119;
  --card: #1e2f21;
  --cb: rgba(50,213,131,0.15);
  --nav: rgba(22,33,25,0.96);
  --t1: #e8f5ec;
  --t2: #a7f3d0;
  --t3: rgba(167,243,208,0.45);
  --primary: #34d399;
  --primary-txt: #0f1f12;
  --accent: #34d399;
  --acs: rgba(52,211,153,0.15);
  /* Sévérité */
  --alertes: #f87171;
  --alertes-s: rgba(248,113,113,0.14);
  --alertes-b: rgba(248,113,113,0.32);
  --anomalie: #fb923c;
  --anomalie-s: rgba(251,146,60,0.14);
  --anomalie-b: rgba(251,146,60,0.32);
  --stress: #fbbf24;
  --stress-s: rgba(251,191,36,0.13);
  --stress-b: rgba(251,191,36,0.3);
  --normal: #34d399;
  /* Charts */
  --chart-forte: #f87171;
  --chart-moy: #fbbf24;
  --chart-surf: #fb923c;
  --chart-bar: #34d399;
  /* UI */
  --sh: 0 2px 8px rgba(0,0,0,0.4), 0 0 0 1px rgba(52,211,153,0.08);
  --shm: 0 4px 20px rgba(0,0,0,0.5);
  --ibg: #162119;
  --grid-y: rgba(52,211,153,0.1);
  --tooltip-bg: #1e2f21;
  --tooltip-border: rgba(52,211,153,0.25);
}
```

---

## 4. Typographie

Police unique : **Poppins** (Google Fonts).

| Token | Desktop | Tablette | Mobile | Weight | Usage |
|-------|---------|----------|--------|--------|-------|
| `display-hero` | 2.5rem | 2rem | 1.8rem | 800 | Logo brand header |
| `display-xl` | 2.5rem | 2rem | 1.8rem | 700 | H1 page title |
| `heading-lg` | 1.5rem | 1.25rem | 1.1rem | 600 | H2 section |
| `heading-md` | 1.1rem | 1rem | 1rem | 600 | H3 card title |
| `kpi-value` | 3rem | 2.5rem | 2rem | 700 | Chiffre KPI |
| `label-kpi` | .85rem | .85rem | .75rem | 600 | Label KPI uppercase |
| `body-md` | 14px | 14px | 14px | 400 | Corps texte |
| `body-sm` | 13px | 13px | 13px | 400 | Sous-titre chart |
| `caption` | .85rem | .85rem | .8rem | 500 | Légendes, unités |
| `mono` | 12px | 12px | 12px | 400 | Courier New — tokens, hex |

```css
* { font-family: 'Poppins', sans-serif; -webkit-font-smoothing: antialiased; }
```

Utiliser `clamp()` pour les niveaux display :
```css
font-size: clamp(1.8rem, 4vw, 2.5rem); /* display-hero */
font-size: clamp(1.5rem, 3vw, 2.5rem); /* display-xl */
```

---

## 5. Système de sévérité

4 niveaux, toujours dans l'ordre **vert → jaune → orange → rouge** :

| Niveau | Token CSS | FR | EN | Clé DB |
|--------|-----------|----|----|--------|
| 1 | `--normal` | Normal | Normal | Normal |
| 2 | `--stress` | À surveiller | Watch | Stress |
| 3 | `--anomalie` | À risque | Caution | Anomalie |
| 4 | `--alertes` | Critique | Critical | Alertes |

### Badges

```html
<!-- Normal -->
<span class="badge" style="background:var(--acs);color:var(--accent);border:1px solid rgba(16,185,129,.2);">
  <span class="dot"></span>Normal
</span>
<!-- À surveiller / Watch / Stress -->
<span class="badge" style="background:var(--stress-s);color:var(--stress);border:1px solid var(--stress-b);">
  <span class="dot"></span>À surveiller
</span>
<!-- À risque / Caution / Anomalie -->
<span class="badge" style="background:var(--anomalie-s);color:var(--anomalie);border:1px solid var(--anomalie-b);">
  <span class="dot"></span>À risque
</span>
<!-- Critique / Critical / Alertes -->
<span class="badge" style="background:var(--alertes-s);color:var(--alertes);border:1px solid var(--alertes-b);">
  <span class="dot"></span>Critique
</span>
```

CSS badge :
```css
.badge {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 3px 10px; border-radius: 999px;
  font-size: 11px; font-weight: 600;
  letter-spacing: .04em; text-transform: uppercase;
}
.dot { width: 5px; height: 5px; border-radius: 50%; background: currentColor; }
```

---

## 6. Composants

### Card
```css
.card {
  background: var(--card);
  border: 1px solid var(--cb);
  border-radius: 12px;
  box-shadow: var(--sh);
}
```

### KPI Card
Structure obligatoire :
```html
<div class="card" style="padding:20px 22px;">
  <!-- Icône + label -->
  <div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;">
    <div style="width:36px;height:36px;border-radius:10px;
                background:var(--alertes-s);border:1px solid var(--alertes-b);
                display:flex;align-items:center;justify-content:center;">
      <!-- SVG inline 18×18, stroke="var(--alertes)" -->
    </div>
    <span style="font-size:10px;font-weight:600;letter-spacing:.05em;
                 text-transform:uppercase;color:var(--t2);">LABEL KPI</span>
  </div>
  <!-- Valeur -->
  <div style="font-size:clamp(2rem,4vw,3rem);font-weight:700;
              letter-spacing:-.02em;line-height:1;color:var(--t1);">42</div>
  <!-- Trend -->
  <span style="font-size:12px;font-weight:500;color:var(--alertes);
               background:var(--alertes-s);padding:3px 8px;border-radius:8px;">
    ↑ +12 vs p.p.
  </span>
</div>
```

KPIs standards de l'app :
- **Alertes détectées** — icône triangle warning (`--alertes`)
- **Surface impactée** — icône grille polygone (`--accent`)
- **Forte sévérité** — icône flamme (`--alertes`)
- **Parcelles touchées** — icône arbre/feuille (`--anomalie`)

### Boutons

```css
.btn {
  display: inline-flex; align-items: center; gap: 7px;
  font-weight: 600; font-size: 14px; cursor: pointer;
  border: none; border-radius: 8px; padding: 9px 20px;
  font-family: 'Poppins', sans-serif;
}
/* Variantes */
.btn-primary { background: var(--primary); color: var(--primary-txt); }
.btn-outline  { background: transparent; color: var(--t1); border: 1.5px solid var(--cb); }
.btn-ghost    { background: transparent; color: var(--t2); }
.btn-danger   { background: var(--alertes-s); color: var(--alertes); border: 1.5px solid var(--alertes-b); }
/* Tailles */
.btn-sm { padding: 6px 14px; font-size: 12px; }
.btn-lg { padding: 12px 28px; font-size: 15px; }
```

Couleur `--primary` par thème :
- Light → `#10b981` / texte blanc
- Dark → `#e1fb15` / texte `#1a1a1a`
- Forest → `#34d399` / texte `#0f1f12`

### Inputs

```css
.inp, .sel {
  background: var(--ibg); border: 1px solid var(--cb);
  border-radius: 8px; padding: 9px 14px; font-size: 14px;
  color: var(--t1); outline: none; width: 100%;
}
.inp:focus, .sel:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--acs);
}
```

### Navigation (3 patterns)

**Pill** — `nav` horizontal avec pills actives, fond `--bg`, border `--cb`.
**Sidebar** — `nav` vertical gauche, 240px, items avec icône + texte.
**Icon-only** — sidebar compacte 60px, icônes seules + tooltip.

Item actif : `background: var(--acs); color: var(--accent);`

---

## 7. Charts (Chart.js / vue-chartjs)

### Config commune (à injecter dans chaque chart)

```js
const baseOptions = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: { display: false },
    tooltip: {
      backgroundColor: 'var(--tooltip-bg)',
      borderColor: 'var(--tooltip-border)',
      borderWidth: 1,
      titleColor: 'var(--t1)',
      bodyColor: 'var(--t2)',
      titleFont: { family: 'Poppins', size: 12, weight: '600' },
      bodyFont:  { family: 'Poppins', size: 11 },
      padding: 10, cornerRadius: 8,
    },
  },
  scales: {
    x: {
      grid: { display: false },
      ticks: { color: 'var(--t3)', font: { family: 'Poppins', size: 10 } },
      border: { display: false },
    },
    y: {
      grid: { color: 'var(--grid-y)', drawBorder: false },
      ticks: { color: 'var(--t3)', font: { family: 'Poppins', size: 10 } },
      border: { display: false },
    },
  },
}
```

### Couleurs des datasets par chart

| Chart | Type | Dataset principal | Dataset secondaire |
|-------|------|------------------|--------------------|
| `SeverityDoughnut` | Double-Ring Doughnut | `--chart-forte`, `--chart-moy`, `--chart-surf` | anneau intérieur décalé |
| `MonthlyEventsChart` | Stacked Bar | `--alertes` | `--anomalie`, `--stress` |
| `MonthlySurfaceChart` | Dual Area Line | `--alertes` | `--anomalie` |
| `MonthlyHectaresChart` | Single Area Line | `--chart-surf` | — |
| `TopForestsChart` | Horizontal Bar (indexAxis:'y') | `--alertes` → `--anomalie` → `--stress` | — |
| `TopParcelsChart` | Horizontal Bar (indexAxis:'y') | `--alertes` → `--anomalie` → `--stress` | — |
| `SpeciesChart` | Polar Area | `--chart-bar`, `--chart-surf`, `--accent` | — |

### Réactivité thème

Les couleurs Chart.js ne lisent pas les CSS vars directement. Résoudre via :
```js
const getCssVar = (v) => getComputedStyle(document.documentElement).getPropertyValue(v).trim()
// Appeler au mount ET sur chaque changement de thème
```

---

## 8. Map Pins (SVG inline — jamais PNG)

ViewBox `0 0 32 40`. Anchor point : bas centre. 3 tailles : sm 22×28, md 32×40, lg 44×54.

### Template de base

```svg
<svg width="32" height="40" viewBox="0 0 32 40" fill="none">
  <!-- Corps du pin (teardrop) -->
  <path d="M16 0C7.163 0 0 7.163 0 16c0 10.627 14.4 23.2 15.04 23.76a1.28 1.28 0 0 0 1.92 0C17.6 39.2 32 26.627 32 16 32 7.163 24.837 0 16 0z"
        fill="[COULEUR_SEVERITE]"/>
  <!-- Cercle intérieur ombré -->
  <path d="M16 4C9.373 4 4 9.373 4 16s5.373 12 12 12 12-5.373 12-12S22.627 4 16 4z"
        fill="rgba(0,0,0,0.15)"/>
  <!-- Arbre goodforest — 3 tiers géométriques -->
  <path d="M16 7.5 L13 13 H19 Z"           fill="white" opacity="0.9"/>
  <path d="M16 11.5 L10.5 18.5 H21.5 Z"   fill="white" opacity="0.9"/>
  <path d="M16 15.5 L8.5 23.5 H23.5 Z"    fill="white" opacity="0.9"/>
  <rect x="14.5" y="23" width="3" height="3" rx="0.5" fill="white" opacity="0.9"/>
</svg>
```

> Pour le pin **Stress** (fond amber clair) : remplacer `fill="white"` par `fill="rgba(0,0,0,0.65)"`.

### Couleurs par niveau

| Niveau | `fill` teardrop |
|--------|----------------|
| Normal | `var(--normal)` |
| Stress / À surveiller | `var(--stress)` |
| Anomalie / À risque | `var(--anomalie)` |
| Alertes / Critique | `var(--alertes)` |

### Badge compteur (optionnel)

```html
<div style="position:relative;width:32px;height:40px;">
  <!-- SVG pin ici -->
  <div style="position:absolute;top:-6px;right:-8px;
              background:var(--alertes);color:white;
              border-radius:99px;min-width:18px;height:18px;
              display:flex;align-items:center;justify-content:center;
              font-size:9px;font-weight:700;
              border:2px solid var(--card);">5</div>
</div>
```

### Clusters

```svg
<svg width="44" height="44" viewBox="0 0 48 48" fill="none">
  <circle cx="24" cy="24" r="22" fill="[COULEUR]" opacity="0.15"/>
  <circle cx="24" cy="24" r="16" fill="[COULEUR]" opacity="0.3"/>
  <circle cx="24" cy="24" r="11" fill="[COULEUR]"/>
  <text x="24" y="28" text-anchor="middle" fill="white"
        font-size="11" font-weight="700" font-family="Poppins,sans-serif">42</text>
</svg>
```

Taille cluster : `< 10` alertes → 40px / `10–49` → 44px / `50+` → 52px. Couleur = sévérité dominante.

---

## 9. Glassmorphism

Réservé **uniquement** aux cards posées sur une image (hero banner, carte satellite). Jamais sur fond app uni.

```css
.glass-panel {
  background: rgba(15, 31, 18, 0.55);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(52, 211, 153, 0.2);
  border-radius: 16px;
}
```

---

## 10. Layout & Espacement

```
Conteneur max-width : 1320px, margin: 0 auto, padding: 0 24px
Grille principale   : CSS Grid repeat(auto-fill, minmax(280px, 1fr)), gap: 16px
Sections            : margin-bottom: 88px
Cards               : border-radius: 12px, padding: 20–24px
Nav sticky          : height: 58px, backdrop-filter: blur(16px)
```

Échelle d'espacement (Tailwind) : `4 / 8 / 12 / 16 / 20 / 24 / 32 / 40 / 48 / 64 / 88px`

---

## 11. Transitions & animations

```css
/* Classe utilitaire à appliquer sur tous les éléments thémés */
.theme-tr {
  transition: background-color .2s ease, color .2s ease,
              border-color .2s ease, box-shadow .2s ease;
}
/* Jamais de transition sur width/height/layout → évite les flickering */
```

---

## 12. Checklist d'implémentation (ordre recommandé)

1. **CSS variables** → coller les 3 blocs `:root` / `[data-theme="dark"]` / `[data-theme="forest"]` dans `src/assets/variables.css`
2. **Tailwind config** → ajouter colors.gf + fontFamily dans `tailwind.config.js`
3. **Switcher de thème** → `document.documentElement.setAttribute('data-theme', theme)` + persistance `localStorage`
4. **Composants de base** → Card, Badge, Button, Input (utiliser les classes CSS ci-dessus)
5. **KPI cards** → 4 cartes avec SVG icônes inline
6. **Navigation** → implémenter au moins le pattern Pill pour mobile + Sidebar pour desktop
7. **Charts** → monter les 7 composants Chart.js avec `getCssVar()` et re-render au changement de thème
8. **Map pins** → SVG templates + logique de cluster dans la couche cartographique
9. **Glassmorphism** → uniquement pour les overlays sur images

---

## 13. Palette de marque — référence rapide

| Nom | Hex | Usage |
|-----|-----|-------|
| Yellow Neon | `#e1fb15` | `--primary` dark |
| Cyan Accent | `#32d583` | `--accent` dark |
| Emerald 400 | `#34d399` | `--primary/accent` forest |
| Emerald 500 | `#10b981` | `--primary/accent` light |
| Forest Deep | `#0f1f12` | `--bg` forest |
| Red Vivid | `#ef4444` | `--alertes` light |
| Red Light | `#f87171` | `--alertes` dark+forest |
| Orange Light | `#f97316` | `--anomalie` light |
| Orange iOS | `#ff9500` | `--anomalie` dark |
| Orange 400 | `#fb923c` | `--anomalie` forest |
| Amber 600 | `#eab308` | `--stress` light |
| Amber 400 | `#fbbf24` | `--stress` forest |
| Background Light | `#f5f7fa` | `--bg` light |
| Background Dark | `#1a1a1a` | `--bg` dark |
| Neutral Surface | `#262626` | `--card` dark |
