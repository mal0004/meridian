# Meridian

> Application de gestion de projet complète — un seul fichier HTML, zéro dépendance.

[![Démo live](https://img.shields.io/badge/Démo-mal0004.github.io%2Fmeridian-5B6EF5?style=flat-square&logo=github)](https://mal0004.github.io/meridian/)
![Version](https://img.shields.io/badge/version-0.1.0-5B6EF5?style=flat-square)
![Taille](https://img.shields.io/badge/taille-~90%20KB-22C55E?style=flat-square)
![Dépendances](https://img.shields.io/badge/dépendances-0-F59E0B?style=flat-square)
[![Licence](https://img.shields.io/badge/licence-MIT-9898AA?style=flat-square)](https://github.com/mal0004/meridian/blob/master/LICENSE)

**[→ Ouvrir la démo](https://mal0004.github.io/meridian/)** · **[Code source](https://github.com/mal0004/meridian)**

```
┌─────────────────────────────────────────────────────────────────┐
│  ⌘  Meridian                                           v0.1  │
├──────────────┬──────────────────────────────────────────────────┤
│              │                                                  │
│  Vues        │   Backlog       En cours    Review    Terminé   │
│  ─────────   │   ─────────     ─────────   ──────    ────────  │
│  ▣ Kanban  ◀ │   ┌────────┐   ┌────────┐                       │
│  ≡ Timeline  │   │ 🔴 Fix │   │ 🟡 API │   ┌──────┐           │
│  ⊞ Dashboard │   │ mobile │   │ N+1    │   │ 🔵 UI│           │
│              │   └────────┘   └────────┘   └──────┘           │
│              │   ┌────────┐                                     │
│              │   │ 🔵 CI  │                                     │
│              │   │ /CD    │                                     │
│              │   └────────┘                                     │
│  ◑ Thème     │                                                  │
└──────────────┴──────────────────────────────────────────────────┘
```

**Meridian** est un gestionnaire de projet inspiré de Linear et Craft, livré en un seul fichier `index.html` autonome. Aucun serveur, aucun bundler, aucun framework — ouvrez le fichier dans un navigateur et commencez à travailler.

---

## Fonctionnalités

### Vue Kanban
- **4 colonnes** : Backlog · En cours · Review · Terminé
- **Drag & drop natif** (HTML5) entre colonnes avec feedback visuel (colonne surlignée, placeholder en pointillés)
- **Cartes** avec icône de priorité, tags colorés, avatar d'assigné et identifiant de tâche
- **Filtres croisés** par priorité, tag et assigné — combinaison ET, compteurs dynamiques
- **Colonne Terminé** visuellement atténuée

### Vue Timeline / Gantt
- **SVG natif** — aucune bibliothèque de chart
- Grille sur **4 semaines (28 jours)** avec numéros de semaine ISO
- Bandes de week-end grisées, lignes de grille hiérarchiques
- **Barres colorées** par priorité avec titre tronqué (`<clipPath>`) et avatar assigné
- **Marqueur "aujourd'hui"** : losange + ligne pointillée verticale
- Scroll horizontal avec panel de labels synchronisé (scroll invisible)
- Bouton **Aujourd'hui** pour recentrer la vue

### Dashboard
- **4 KPI cards** : Total · Terminées · En cours · Taux de complétion
- **Burndown chart** sur Canvas 2D — courbe réelle + ligne idéale en pointillés, gradient de remplissage, point du jour, responsive via `ResizeObserver`
- **Heatmap d'activité** 7 × 4 (jours × semaines) avec 5 niveaux d'intensité
- **Répartition par priorité** — barres horizontales colorées
- **Répartition par assigné** — avatar + barre de progression
- **Temps réel** : toute modification Kanban met à jour le dashboard instantanément

### Palette de commandes `⌘K`
- Fuzzy search avec **scoring** (bonus départ précoce + caractères consécutifs)
- **Caractères matchés surlignés** dans les résultats
- Recherche dans les **actions statiques** et les **tâches**
- Navigation clavier `↑` `↓` `↵`, fermeture `Esc`
- Sections : Vues · Actions · Tâches

### Raccourcis clavier
| Touche | Action |
|--------|--------|
| `⌘K` / `Ctrl+K` | Palette de commandes |
| `1` `2` `3` | Basculer entre Kanban / Timeline / Dashboard |
| `N` | Nouvelle tâche (Backlog) |
| `T` | Basculer thème clair / sombre |
| `F` | Effacer tous les filtres |
| `?` | Aide — liste des raccourcis |
| `Esc` | Fermer tout modal ou palette ouvert |

### Thème
- Détection automatique via `prefers-color-scheme`
- Bascule manuelle persistée en `localStorage`
- Canvas burndown adaptatif au changement de thème (via `MutationObserver`)

### Persistance
- Toutes les données en `localStorage` — tâches, vue active, préférence de thème
- Données de seed pré-chargées au premier lancement

---

## Aperçu ASCII

```
KANBAN ─────────────────────────────────────────────────────────
  Priorité [Urgent][Haute][Moyenne][Basse]  Tag [Frontend][Bug]…

  BACKLOG            EN COURS           REVIEW         TERMINÉ
  ─────────────      ─────────────      ───────────    ───────────
  ┌───────────┐      ┌───────────┐      ┌─────────┐    ┌─────────┐
  │▲ Fix pagin│      │▲ N+1 API  │      │◼ DataTbl│    │◼ Sentry │
  │[Bug][Front│      │[Backend]  │      │[UI][Dev]│    │[Infra]  │
  │       AL ●│      │       BO ●│      │    CL ● │    │    DA ● │
  └───────────┘      └───────────┘      └─────────┘    └─────────┘
  ┌───────────┐
  │◼ CI/CD    │
  │[Infra]    │
  │       DA ●│
  └───────────┘

TIMELINE ───────────────────────────────────────────────────────
  16 mar 2026 → 12 avr 2026                        [Aujourd'hui]

  Tâches │ S12·16mar    S13·23mar    S14·30mar    S15·6avr
  ───────┼─────────────────────────────────────────────────────
  Fix pag│ ████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ AL
  N+1 API│ ░░░░░░░░░████████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░ BO
  Redesig│ ░░░░░░░░░░░░░░░░░░░░████████████████░░░░░░░░░░░░░ CL
         │                          ↑ aujourd'hui

DASHBOARD ──────────────────────────────────────────────────────
  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
  │  Total   │ │ Terminées│ │ En cours │ │Complétion│
  │    10    │ │    2     │ │    2     │ │   20%    │
  │          │ │██░░░░░░░░│ │███░░░░░░░│ │██░░░░░░░░│
  └──────────┘ └──────────┘ └──────────┘ └──────────┘

  Burndown 4 semaines        │  Par priorité
  10│╲  ╌╌╌╌╌ idéal         │  Urgent ████░░░░  2
    │ ╲    ───── réel        │  Haute  ████████  4
   5│  ╲____                 │  Moyen  ████░░░░  2
    │       ‾‾‾──            │  Basse  ██░░░░░░  1
   0└─────────────────       │
    S12  S13  S14  S15       │
```

---

## Architecture du code

Tout le projet tient dans **un seul fichier** `index.html` (~3 300 lignes), organisé en sections clairement délimitées.

```
index.html
├── <head>
│   └── <style>
│       ├── Design system (tokens CSS, variables sémantiques)
│       ├── Thème clair / sombre / auto
│       ├── Reset & base
│       ├── App shell (sidebar, topbar, layout)
│       ├── Kanban (colonnes, cartes, filtres, modal)
│       ├── Timeline / Gantt (labels panel, SVG grid)
│       ├── Dashboard (KPI cards, canvas, heatmap)
│       ├── Palette de commandes
│       └── Modal d'aide
│
├── <body>
│   ├── #app
│   │   ├── #sidebar (logo, nav, theme toggle)
│   │   └── #main
│   │       ├── #topbar (breadcrumb, actions)
│   │       └── #content
│   │           ├── #view-kanban   (toolbar + board)
│   │           ├── #view-timeline (toolbar + SVG gantt)
│   │           └── #view-dashboard (grid : KPIs, canvas, heatmap)
│   ├── #cmdPalette  (palette de commandes)
│   └── #helpModal   (modal d'aide raccourcis)
│
└── <script>
    ├── Globals          _appInitDone, thème
    ├── Theme            loadTheme(), applyThemeUI()
    ├── Navigation       switchView(), raccourcis clavier
    │
    ├── ── KANBAN ──────────────────────────────────────────
    ├── Constants        COLUMNS, ASSIGNEES, TAGS, PRIORITIES
    ├── Store            loadTasks(), saveTasks(), tasks[]
    ├── Filters          initFilters(), updateFilterUI(),
    │                    toggleFilter(), clearAllFilters()
    ├── Render           renderCard(), renderColumn(), renderBoard()
    ├── Drag & drop      dragstart / dragover / drop
    ├── Modal            buildModal(), openModal(), submitModal()
    ├── Utility          escHtml(), makeId()
    │
    ├── ── TIMELINE ────────────────────────────────────────
    ├── Constants        DAY_W, ROW_H, HEADER_H, TOTAL_DAYS
    ├── Helpers          getMonday(), isoWeek(), ensureTimelineData()
    ├── SVG builder      svgEl(), renderTimeline()
    └── Sync             scroll listener, scrollToToday()
    │
    ├── ── DASHBOARD ───────────────────────────────────────
    ├── Data             simulateBurndown(), getDayActivity()
    ├── Canvas           getCanvasColors(), drawBurndown()
    ├── Render           renderDashboard()
    ├── Observers        ResizeObserver, MutationObserver (thème)
    │
    ├── ── PALETTE & AIDE ──────────────────────────────────
    ├── Commands         PALETTE_COMMANDS, CMD_ICONS
    ├── Fuzzy            fuzzyMatch(), hlText()
    ├── Palette          openPalette(), _renderPaletteResults()
    └── Help             openHelp(), closeHelp()
```

### Design system

Les tokens CSS sont définis en variables sur `:root` et remplacés par les overrides dark-mode sur `[data-theme="dark"]` et `@media (prefers-color-scheme: dark) [data-theme="auto"]`.

| Catégorie | Variables |
|-----------|-----------|
| Couleurs brand | `--accent`, `--accent-hover`, `--accent-subtle` |
| Échelle neutre | `--gray-50` → `--gray-900` |
| Sémantiques | `--bg`, `--bg-subtle`, `--bg-elevated`, `--border`, `--text`, `--text-muted` |
| Typographie | `--font`, `--font-mono`, `--text-xs` → `--text-3xl`, `--weight-*` |
| Espacement | `--sp-1` (4px) → `--sp-12` (48px) |
| Arrondis | `--r-sm` → `--r-full` |
| Ombres | `--shadow-xs` → `--shadow-lg` |
| Transitions | `--ease`, `--ease-snap`, `--dur-fast` → `--dur-slow` |

---

## Démarrage

```bash
# Cloner le dépôt
git clone https://github.com/mal0004/meridian.git
cd meridian

# Ouvrir directement dans le navigateur
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

Aucune installation, aucun `npm install`, aucun serveur local requis.

> **Note** : la Google Font `Inter` est chargée depuis `fonts.googleapis.com`. En environnement hors ligne, le système retombe sur `system-ui` / `-apple-system`.

---

## Données & persistance

Toutes les données sont stockées dans `localStorage` sous les clés suivantes :

| Clé | Contenu |
|-----|---------|
| `meridian:tasks` | Tableau JSON des tâches (titre, colonne, priorité, tags, assigné, startDay, duration, createdAt) |
| `meridian:view` | Dernière vue active (`kanban` / `timeline` / `dashboard`) |
| `meridian:theme` | Préférence de thème (`light` / `dark` — absent = `auto`) |

Pour réinitialiser l'application :

```js
// Dans la console du navigateur
localStorage.removeItem('meridian:tasks');
location.reload();
```

---

## Contribuer

Les contributions sont les bienvenues. Ce projet étant un fichier unique, les conventions sont simples.

### Processus

```bash
# 1. Forker le dépôt sur https://github.com/mal0004/meridian
#    puis cloner votre fork
git clone https://github.com/VOTRE-USERNAME/meridian.git

# 2. Créer une branche descriptive
git checkout -b feat/nom-de-la-fonctionnalite

# 3. Modifier index.html
# 4. Tester dans Chrome, Firefox et Safari (desktop)
# 5. Pousser et ouvrir une Pull Request
git push origin feat/nom-de-la-fonctionnalite
```

### Conventions de code

- **Pas de framework, pas de bundler** — vanilla JS ES2020+ uniquement
- **Tout dans `index.html`** — pas de fichiers séparés CSS/JS
- **Variables CSS** pour toute valeur visuelle — pas de couleur hardcodée hors du design system
- **`escHtml()`** obligatoire sur tout contenu utilisateur injecté dans le DOM
- **Event delegation** préféré à l'attachement de listeners en boucle
- **`function` declarations** pour les fonctions hoistables (logique principale), **`const`** pour les expressions de flèches et callbacks

### Structure d'une tâche

```js
{
  id:        "t-011",          // auto-généré, format "t-NNN"
  title:     "Titre de tâche", // string, obligatoire
  column:    "backlog",        // "backlog" | "inprogress" | "review" | "done"
  priority:  "medium",         // "urgent" | "high" | "medium" | "low"
  tags:      ["frontend"],     // tableau d'ids (voir TAGS[])
  assignee:  "al",             // id (voir ASSIGNEES[]) ou null
  startDay:  0,                // offset depuis le lundi de la semaine courante (0–27)
  duration:  3,                // durée en jours (1–28)
  createdAt: 1742000000000     // timestamp Unix ms
}
```

### Ajouter un assigné fictif

Dans le tableau `ASSIGNEES` (section *KANBAN — data model*) :

```js
{ id: 'em', name: 'Emma', initials: 'EM', color: '#F472B6' },
```

### Ajouter une colonne

Dans `COLUMNS`, puis mettre à jour les sélecteurs du modal (`colOptions`) et la logique de filtrage si nécessaire.

### Roadmap potentielle

- [ ] Édition inline des cartes (double-clic)
- [ ] Drag horizontal sur le Gantt pour modifier `startDay` / `duration`
- [ ] Export JSON / import de données
- [ ] Palette de commandes : historique des actions récentes
- [ ] Vue Liste (alternative au Kanban)
- [ ] Notifications / rappels via `Notification API`
- [ ] Mode hors-ligne garanti via `Service Worker`

---

## Compatibilité navigateurs

| Navigateur | Support |
|------------|---------|
| Chrome / Edge ≥ 90 | ✅ Complet |
| Firefox ≥ 88 | ✅ Complet |
| Safari ≥ 15 | ✅ Complet |
| Mobile Chrome / Safari | ⚠️ Fonctionnel, drag & drop limité |
| IE 11 | ✗ Non supporté |

Technologies utilisées :
- CSS Custom Properties
- CSS Grid & Flexbox
- HTML5 Drag and Drop API
- Canvas 2D API
- SVG inline
- `localStorage`
- `ResizeObserver`
- `MutationObserver`
- `requestAnimationFrame`

---

## Licence

```
MIT License

Copyright (c) 2026 Meridian Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

<div align="center">
  <sub>
    Construit avec ♥ en HTML / CSS / JS vanilla · Aucune dépendance · Fonctionne partout<br>
    <a href="https://mal0004.github.io/meridian/">Démo live</a> ·
    <a href="https://github.com/mal0004/meridian">GitHub</a> ·
    <a href="https://github.com/mal0004/meridian/issues">Signaler un bug</a>
  </sub>
</div>
