# Meridian

> Application de gestion de projet complète — un seul fichier HTML, zéro dépendance.

[![Landing page](https://img.shields.io/badge/Landing-mal0004.github.io%2Fmeridian-5B6EF5?style=flat-square&logo=github)](https://mal0004.github.io/meridian/)
![Version](https://img.shields.io/badge/version-0.5.0-5B6EF5?style=flat-square)
![Taille](https://img.shields.io/badge/taille-~160%20KB-22C55E?style=flat-square)
![Dépendances](https://img.shields.io/badge/dépendances-0-F59E0B?style=flat-square)
[![Licence](https://img.shields.io/badge/licence-MIT-9898AA?style=flat-square)](https://github.com/mal0004/meridian/blob/master/LICENSE)

**[→ Présentation](https://mal0004.github.io/meridian/)** · **[→ Ouvrir l'application](https://mal0004.github.io/meridian/app.html)** · **[Code source](https://github.com/mal0004/meridian)**

**Meridian** est un gestionnaire de projet inspiré de Linear et Craft, livré en deux fichiers HTML autonomes. Aucun serveur, aucun bundler, aucun framework — ouvrez un fichier dans un navigateur et commencez à travailler.

| Fichier | Rôle |
|---------|------|
| `index.html` | Landing page — présentation du projet |
| `app.html` | Application Kanban complète |

---

## Fonctionnalités

### Vue Kanban
- **4 colonnes** : Backlog · En cours · Review · Terminé
- **Drag & drop natif** (HTML5) entre colonnes avec feedback visuel (colonne surlignée, placeholder en pointillés)
- **Cartes** avec icône de priorité, tags colorés, avatar d'assigné, identifiant et compteur de commentaires
- **Filtres croisés** par priorité, tag et assigné — combinaison ET, compteurs dynamiques
- **Colonne Terminé** visuellement atténuée

### Panneau de focus
- **Clic sur une carte** ouvre un panneau latéral persistant (420 px), sans quitter la vue
- **Description rich-text** avec bascule Aperçu / Éditer — Markdown simplifié : `# Titres`, `**gras**`, `*italique*`, `` `code` ``, `- listes`, `> citations`, `[liens](url)`, `---`
- **Auto-save** à 600 ms après la frappe, `Ctrl+S` pour forcer la sauvegarde immédiate
- **Fil de discussion** intégré : commentaires avec avatar, auteur, timestamp relatif, `Ctrl+Entrée` pour envoyer
- **Métadonnées** de la tâche : statut, priorité, assigné, tags, date de création
- **Supprimer** la tâche depuis le panneau, avec confirmation via toast + undo

### Vue Timeline / Gantt
- **SVG natif** — aucune bibliothèque de chart
- Grille sur **4 semaines (28 jours)** avec numéros de semaine ISO
- Bandes de week-end grisées, lignes de grille hiérarchiques
- **Barres colorées** par priorité avec titre tronqué (`<clipPath>`) et avatar assigné
- **Marqueur "aujourd'hui"** : losange + ligne pointillée verticale
- Scroll horizontal avec panel de labels synchronisé
- Bouton **Aujourd'hui** pour recentrer la vue

### Dashboard
- **4 KPI cards** : Total · Terminées · En cours · Taux de complétion
- **Burndown chart** sur Canvas 2D — courbe réelle + ligne idéale en pointillés, gradient de remplissage, point du jour, responsive via `ResizeObserver`
- **Heatmap d'activité** 7 × 4 (jours × semaines) avec 5 niveaux d'intensité
- **Répartition par priorité** — barres horizontales colorées
- **Répartition par assigné** — avatar + barre de progression
- **Temps réel** : toute modification Kanban met à jour le dashboard instantanément

### Notifications toast
- **Confirmation** après chaque action : tâche créée, déplacée, supprimée
- **Undo instantané** — bouton Annuler disponible pendant 4 secondes, barre de progression en temps réel
- Pause au survol, fermeture au clic, file jusqu'à 5 toasts simultanés
- Annonces `aria-live` pour les lecteurs d'écran

### Palette de commandes `⌘K`
- Fuzzy search avec **scoring** (bonus départ précoce + caractères consécutifs)
- **Caractères matchés surlignés** dans les résultats
- Recherche dans les **actions statiques** et les **tâches**
- Navigation clavier `↑` `↓` `↵`, fermeture `Esc`
- Sections : Vues · Actions · Tâches

### Accessibilité
- **Skip link** "Passer au contenu principal" visible au focus clavier
- **ARIA roles** : `region` sur chaque colonne, `article` sur chaque carte, `toolbar` sur les filtres, `complementary` sur le panneau de focus, `dialog` sur tous les modals
- **Focus trap** dans chaque modal (Nouvelle tâche, Palette, Aide, Détail) — Tab / Shift+Tab reste dans la fenêtre ouverte
- **Restauration du focus** à l'élément déclencheur à la fermeture de chaque modal
- **Navigation clavier des cartes** : `Tab` pour parcourir, `Entrée` / `Espace` pour ouvrir le panneau de focus
- **`aria-pressed`** sur les filtres et le bouton de thème, **`aria-current="page"`** sur la nav active
- **`aria-hidden`** sur les icônes SVG décoratives, **`aria-label`** complet sur chaque carte (titre, priorité, colonne, assigné)
- Région `aria-live="polite"` pour les annonces dynamiques (drag, toasts, ouverture du panneau)

### Raccourcis clavier
| Touche | Action |
|--------|--------|
| `⌘K` / `Ctrl+K` | Palette de commandes |
| `1` `2` `3` | Basculer entre Kanban / Timeline / Dashboard |
| `N` | Nouvelle tâche (Backlog) |
| `T` | Basculer thème clair / sombre |
| `F` | Effacer tous les filtres |
| `?` | Aide — liste des raccourcis |
| `Esc` | Fermer tout modal ou panneau ouvert |
| `Entrée` / `Espace` | Ouvrir le panneau de focus sur une carte sélectionnée |
| `Ctrl+S` | Sauvegarder la description (panneau de focus en mode Éditer) |
| `Ctrl+Entrée` | Envoyer un commentaire |

### Thème
- Détection automatique via `prefers-color-scheme`
- Bascule manuelle persistée en `localStorage`
- Canvas burndown adaptatif au changement de thème (via `MutationObserver`)

### Persistance
- Toutes les données en `localStorage` — tâches, vue active, préférence de thème
- Données de seed pré-chargées au premier lancement (10 tâches, 9 commentaires)
- Migration automatique des données existantes lors d'une mise à jour (ajout de `comments`, `description`, `createdAt` si absents)

---

## Architecture du code

L'application tient dans **un seul fichier** `app.html` (~5 000 lignes), organisé en sections clairement délimitées.

```
app.html
├── <head>
│   └── <style>
│       ├── Design system (tokens CSS, variables sémantiques)
│       ├── Thème clair / sombre / auto
│       ├── Reset & base, utilitaires accessibilité (.sr-only, .skip-link)
│       ├── App shell (sidebar, topbar, layout)
│       ├── Kanban (colonnes, cartes, filtres, modal)
│       ├── Timeline / Gantt (labels panel, SVG grid)
│       ├── Dashboard (KPI cards, canvas, heatmap)
│       ├── Palette de commandes & modal d'aide
│       ├── Détail tâche & commentaires (modal)
│       ├── Panneau de focus (side panel, Markdown preview)
│       └── Toast notifications
│
├── <body>
│   ├── .skip-link
│   ├── #app
│   │   ├── #sidebar (logo, nav[aria-label], theme toggle)
│   │   └── #main
│   │       ├── #topbar (breadcrumb, actions)
│   │       └── #content[tabindex=-1]
│   │           ├── #view-kanban   (toolbar[role=toolbar] + board)
│   │           ├── #view-timeline (toolbar + SVG gantt)
│   │           └── #view-dashboard (grid : KPIs, canvas, heatmap)
│   │   └── #focusPanel[role=complementary]
│   │       ├── .fp-header (id, priorité, titre, méta-badges)
│   │       └── .fp-body
│   │           ├── .fp-section — description Markdown
│   │           └── .fp-section — commentaires + saisie
│   ├── #detailModal[role=dialog]
│   ├── #cmdPalette[role=dialog]
│   └── #helpModal[role=dialog]
│
└── <script>
    ├── Accessibilité    focusTrap(), announce(), live region
    ├── Theme            loadTheme(), applyThemeUI()
    ├── Navigation       switchView(), aria-current, raccourcis clavier
    │
    ├── ── KANBAN ──────────────────────────────────────────
    ├── Constants        COLUMNS, ASSIGNEES, TAGS, PRIORITIES, PRIORITY_SVG
    ├── Store            loadTasks(), saveTasks(), tasks[]
    ├── Filters          initFilters(), updateFilterUI(), aria-pressed
    ├── Render           renderCard(), renderColumn(), renderBoard()
    ├── Drag & drop      dragstart / dragover / drop + toast undo
    ├── Modal            buildModal(), openModal(), closeModal(), submitModal()
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
    ├── Palette          openPalette(), closePalette(), focusTrap
    └── Help             openHelp(), closeHelp(), focusTrap
    │
    ├── ── TOASTS ──────────────────────────────────────────
    └── IIFE             showToast(msg, {type, undo, duration})
    │
    ├── ── PANNEAU DE FOCUS ────────────────────────────────
    ├── Markdown         parseMarkdown()
    ├── Render           renderFocusMeta(), renderFocusComments()
    ├── Description      setFpDescMode(), auto-save (debounce 600ms)
    ├── Commentaires     addFocusComment(), formatRelTime()
    └── Panel            openFocus(), closeFocus(), aria-hidden
    │
    └── ── DÉTAIL MODAL (commentaires) ─────────────────────
        ├── Render       renderDetailMeta(), renderComments()
        ├── Commentaires addComment()
        └── Dialog       openDetail(), closeDetail(), focusTrap
```

### Design system

Les tokens CSS sont définis en variables sur `:root` et remplacés par les overrides dark-mode sur `[data-theme="dark"]` et `@media (prefers-color-scheme: dark) [data-theme="auto"]`.

| Catégorie | Variables |
|-----------|-----------|
| Couleurs brand | `--accent`, `--accent-hover`, `--accent-subtle` |
| Sémantiques | `--bg`, `--bg-subtle`, `--bg-elevated`, `--border`, `--text`, `--text-muted` |
| Feedback | `--success`, `--warning`, `--danger` |
| Typographie | `--font`, `--font-mono`, `--text-xs` → `--text-3xl`, `--weight-*` |
| Espacement | `--sp-1` (4px) → `--sp-12` (48px) |
| Arrondis | `--radius-sm`, `--radius`, `--radius-lg` |
| Ombres | `--shadow-xs` → `--shadow-lg` |

---

## Démarrage

```bash
# Cloner le dépôt
git clone https://github.com/mal0004/meridian.git
cd meridian

# Ouvrir la landing page
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux

# Ouvrir directement l'application
open app.html            # macOS
start app.html           # Windows
xdg-open app.html        # Linux
```

Aucune installation, aucun `npm install`, aucun serveur local requis.

> **Note** : la Google Font `Inter` est chargée depuis `fonts.googleapis.com`. En environnement hors ligne, le système retombe sur `system-ui` / `-apple-system`.

---

## Données & persistance

Toutes les données sont stockées dans `localStorage` sous les clés suivantes :

| Clé | Contenu |
|-----|---------|
| `meridian:tasks` | Tableau JSON des tâches |
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

# 3. Modifier app.html (application) ou index.html (landing page)
# 4. Tester dans Chrome, Firefox et Safari (desktop)
# 5. Pousser et ouvrir une Pull Request
git push origin feat/nom-de-la-fonctionnalite
```

### Conventions de code

- **Pas de framework, pas de bundler** — vanilla JS ES2020+ uniquement
- **Tout dans `app.html`** — pas de fichiers séparés CSS/JS
- **Variables CSS** pour toute valeur visuelle — pas de couleur hardcodée hors du design system
- **`escHtml()`** obligatoire sur tout contenu utilisateur injecté dans le DOM
- **Event delegation** préféré à l'attachement de listeners en boucle
- **`function` declarations** pour les fonctions hoistables (logique principale), **`const`** pour les expressions de flèches et callbacks
- **`aria-*`** et `role` obligatoires sur tout nouvel élément interactif ou région

### Structure d'une tâche

```js
{
  id:          "t-011",          // auto-généré, format "t-NNN"
  title:       "Titre de tâche", // string, obligatoire
  column:      "backlog",        // "backlog" | "inprogress" | "review" | "done"
  priority:    "medium",         // "urgent" | "high" | "medium" | "low"
  tags:        ["frontend"],     // tableau d'ids (voir TAGS[])
  assignee:    "al",             // id (voir ASSIGNEES[]) ou null
  startDay:    0,                // offset depuis le lundi de la semaine courante (0–27)
  duration:    3,                // durée en jours (1–28)
  createdAt:   1742000000000,    // timestamp Unix ms
  description: "",               // Markdown brut (éditable dans le panneau de focus)
  comments: [
    {
      id:     "c-010",           // auto-généré, format "c-NNN"
      author: "al",              // id d'un ASSIGNEE
      text:   "Texte du commentaire",
      ts:     1742000000000      // timestamp Unix ms
    }
  ]
}
```

### Ajouter un assigné

Dans le tableau `ASSIGNEES` (section *KANBAN — data model*) :

```js
{ id: 'em', name: 'Emma', initials: 'EM', color: '#F472B6' },
```

### Ajouter une colonne

Dans `COLUMNS`, puis mettre à jour les options du modal de création si nécessaire.

### Roadmap potentielle

- [ ] Édition inline du titre des cartes (double-clic)
- [ ] Drag horizontal sur le Gantt pour modifier `startDay` / `duration`
- [ ] Export JSON / import de données
- [ ] Palette de commandes : historique des actions récentes
- [ ] Vue Liste (alternative au Kanban)
- [ ] Mode hors-ligne garanti via `Service Worker`
- [ ] Tests d'accessibilité automatisés (axe-core)

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
- CSS Custom Properties · Grid · Flexbox
- HTML5 Drag and Drop API
- Canvas 2D API · SVG inline
- `localStorage` · `ResizeObserver` · `MutationObserver`
- `requestAnimationFrame`
- ARIA (WAI-ARIA 1.2)

---

## Licence

Distribué sous licence MIT. Voir [`LICENSE`](LICENSE) pour le texte complet.

---

<div align="center">
  <sub>
    Construit avec ♥ en HTML / CSS / JS vanilla · Aucune dépendance · Fonctionne partout<br>
    <a href="https://mal0004.github.io/meridian/">Landing page</a> ·
    <a href="https://mal0004.github.io/meridian/app.html">Application</a> ·
    <a href="https://github.com/mal0004/meridian">GitHub</a> ·
    <a href="https://github.com/mal0004/meridian/issues">Signaler un bug</a>
  </sub>
</div>
