# Layout & Hierarchy Rules — DashLint Rulebook

> Information hierarchy — what goes where, how the eye should travel,
> and the structural patterns from production dashboard projects.

---

## Page-Level Hierarchy

Every dashboard follows an inverted-pyramid reading order. The most
summarized information is at the top; detail increases as the user
scrolls or drills down.

```
┌─────────────────────────────────────────────────────────────────┐
│  Sidebar / Nav Rail       │  Header (Title + Data Source)       │
│  (240–280px, persistent,  ├─────────────────────────────────────┤
│   visually distinct from  │  Filter Strip (date range, scope,   │
│   content area)           │  category selects, export action)   │
│                           ├─────────────────────────────────────┤
│  • Dataset snapshot       │  Tab Navigation (segmented track)   │
│  • Key metric stack       ├─────────────────────────────────────┤
│  • Navigation links       │  KPI Row (hero numbers, 4–6 cards)  │
│  • Settings / config      ├──────────────────┬──────────────────┤
│                           │  Primary chart   │  Secondary chart │
│                           │  (wider panel)   │  or table        │
│                           ├──────────────────┴──────────────────┤
│                           │  Detail / drill-down area           │
│                           │  (tables, ranked lists, expanded)   │
└───────────────────────────┴─────────────────────────────────────┘
```

---

## Rules

### Visual Weight & Reading Order

- **R-LAYOUT-01**: **KPI summary cards are always positioned above charts.** This is standard inverted-pyramid information hierarchy — the most aggregated data appears first. Hard rule.
- **R-LAYOUT-02**: Filter strip sits **above** the tab navigation — filters apply globally across tabs and should be visible before any tab content.
- **R-LAYOUT-03**: The most critical metric occupies the **first (leftmost) KPI card** position. Reading order is left-to-right, top-to-bottom.

### Sidebar / Nav Rail

- **R-LAYOUT-04**: A **persistent nav rail, visually distinct from the content area**, is the structural rule. It houses navigation, dataset indicators, and summary metrics. Width range: **240–280px**.
- **R-LAYOUT-05**: The sidebar uses a **visually distinct treatment** (dark background is the default convention; light with strong border is also acceptable) to create clear separation from the data workspace.

### Grid System

- **R-LAYOUT-06**: Dashboard workspace uses an **asymmetric two-column grid** — the primary panel is wider than the supporting panel. The principle is that the main analytical view gets more space; the exact ratio is flexible.
- **R-LAYOUT-07**: Grid gap between dashboard cards is `12px`. App canvas padding is `12px`.
- **R-LAYOUT-08**: **Minimum chart height is 180–200px.** Charts compressed below this threshold become unreadable — axis labels overlap, data points collide, and patterns vanish. This is a common AI-generated-layout failure.

### Responsive Behavior

- **R-LAYOUT-09**: At approximately **900–960px viewport width**, the grid collapses to a single column. Don't hard-code a single breakpoint — test with your actual content.
- **R-LAYOUT-10**: When the sidebar can't fit alongside content, it collapses to a top nav bar or a hamburger-triggered overlay — never hidden entirely.
- **R-LAYOUT-11**: Charts below minimum readable width should switch to a simplified view (fewer tick marks, hidden axis labels) rather than simply scaling down.

### Drawers & Overlays

- **R-LAYOUT-12**: Drill-down drawers slide from the **right**. Default width: `min(520px, 92vw)`.
- **R-LAYOUT-13**: **Full-screen overlays** are for spatial or sustained-focus tasks with their own toolbar — geographic maps, multi-view analysis studios, flow network visualizations. Use them for work that needs its own dedicated context.
- **R-LAYOUT-14**: **Slide drawers** are for quick drill-downs that shouldn't lose the surrounding dashboard context — clicking a data point to see its details, inspecting a specific incident or agent.
- **R-LAYOUT-15**: Overlay backdrop uses the dark theme palette (`--surface: #151515`). Drawers use the main theme palette.

### Tab Navigation

- **R-LAYOUT-16**: Tabs use a **segmented track** pattern (height: `34px`, inner gap: `4px`). Active tab is visually elevated (white surface card with subtle drop shadow).
- **R-LAYOUT-17**: All tab panels are rendered simultaneously and toggled via `display: none` — this preserves scroll positions, chart dimensions, and component state across tab switches. Never unmount tab content.

---

## Interaction Patterns

- **R-INTERACT-01**: **Cross-filtering** (clicking a chart element filters other charts) is strongly recommended for multi-chart analytical dashboards. Not mandatory for single-purpose status views.
- **R-INTERACT-02**: Charts should be **interactive entry points** — clicking data points opens a drawer or navigates to a filtered view. But don't make decorative elements clickable with no real destination behind them.
- **R-INTERACT-03**: **Keyboard shortcuts** for overlay access and tab switching are a power-user accessibility nicety worth implementing, but not a core requirement. Document them when present (e.g., `1`–`7` for tabs, `Escape` to dismiss).

---

## Viewport & Scroll Policy

- **R-LAYOUT-18**: The viewport shell is **100vh × 100vw with `overflow: hidden`** on the outer container. Outer page-level scrolling is forbidden in a dashboard — all scroll activity is confined to individual panels, tables, or drawer bodies with custom scrollbars (`5px` width, `4px` thumb radius).

---

## Empty, Loading & Error States

- **R-STATE-01 (Loading UI)**: Use skeleton screens shaped like the actual chart (e.g., bar-shaped bars, flat line for a line chart), not a generic spinner. Spinners cause jarring pop-ins; shape-matching skeletons keep the layout stable and look more engineered. For KPI cards, use a pulsing/blurred placeholder for the number, then use the AnimatedNumber count-up firing once real data lands, bridging the loading and loaded states into one animation system.
- **R-STATE-02 (Empty States)**: Keep the chart shell (axes, grid, card frame) visible and centered, and overlay a short, specific message (e.g., "No incidents in this range") instead of a decorative illustration or collapsing the card. Layout stability across states is critical; big illustrations visually compete with surrounding data. Always hint at active filters in the copy if applicable.
- **R-STATE-03 (Error States)**: Errors must be per-card isolated, not a page-level crash. One failed fetch out of six should show only that card in a "Failed to load — Retry" state (inline, matching the loaded footprint) while the rest of the dashboard remains interactive. This enforces an architecture where charts fetch independently rather than using a single shared page-level query.
- **R-LAYOUT-11 (Sidebar Necessity)**: A full sidebar may be more chrome than this dashboard needs. If the layout has a sidebar but 2 or fewer views and no persistent filters, it usually fits a header/top-bar just as well. This is a recommendation, not a hard error.
