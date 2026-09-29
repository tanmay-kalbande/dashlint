---
name: dashlint
description: >
  Dashboard and data-visualization design rulebook — chart selection
  (data shape → chart type mapping with rationale), color/spacing/typography
  design tokens, layout hierarchy, and information-density rules derived from
  production React analytics dashboards (incident management, contact-center
  SLA). Use when building, reviewing, or debugging any dashboard UI,
  analytics page, data-viz component, admin panel with charts, KPI display,
  or operational command-center view. Covers chart type decisions (when to
  avoid pie charts, horizontal vs vertical bars, stacked vs grouped, Sankey
  flow diagrams), semantic status colors, dark overlay themes, responsive
  grid collapse, drawer vs overlay patterns, monospace tabular-nums for
  numeric data, and animated KPI count-ups. Provides concrete pass/fail
  checks with rule IDs, not vague best-practices. Library-agnostic
  (Recharts, Nivo, D3, Victory, Chart.js, custom SVG).
---

# DashLint — Dashboard & Data-Viz Design Skill

## When to activate this skill

Activate DashLint when the user is:
- Building a new dashboard, analytics page, or data visualization
- Choosing chart types for a given dataset shape
- Reviewing or debugging an existing dashboard layout
- Defining color palettes, spacing, or typography for a data-heavy UI
- Creating KPI cards, filter strips, or drill-down panels
- Working with charting libraries (Recharts, Nivo, D3, Victory, Chart.js, etc.)
- Building operational command-center or SLA compliance views
- Deciding between drawers and overlays for drill-down patterns

## How to use

1. **Read [reference.md](./reference.md)** for the full rulebook — it
   contains every design rule with its ID (e.g., `R-CHART-01`).
2. **Profile your data** — identify field types, cardinalities, and roles.
3. **Choose the visual system** — Preserve the user's existing product system when working in an app. For a new dashboard, select a coherent reference or brand direction using judgment; ask only when the user's preference materially affects the result. This MCP does not expose design-system listing, planning, or validation tools.
4. **Build for the task** — treat chart, layout, color, and component patterns as reasoned defaults. The MCP's blueprint tool accepts field metadata only; it does not inspect rows, generate code, or validate a rendered dashboard.
5. **Review the result** — use `get_dashboard_completion_checklist()` when connected to the DashLint MCP. Otherwise review against the relevant rules in `reference.md`.
6. If a rule is violated, explain the issue and apply a context-appropriate fix. Rules are **data-driven defaults, not hard bans**; preserve readability, accessibility, and truthful data presentation when making an exception.

## Rule categories

| Prefix        | Category                        |
|---------------|---------------------------------|
| `R-COLOR-*`   | Color system & palette          |
| `R-SPACE-*`   | Spacing & sizing                 |
| `R-TYPE-*`    | Typography                       |
| `R-CHART-*`   | Chart selection & configuration  |
| `R-LAYOUT-*`  | Layout hierarchy & grid          |
| `R-INTERACT-*`| Interaction patterns             |
| `R-STATE-*`   | Empty / loading / error states   |
| `R-INSIGHT-*` | Insight presentation             |
| `R-DESIGN-*`  | Design system consistency        |

## Quick reference — check these first

1. **`R-CHART-01`**: Pie charts are a strong default-avoid. Use horizontal bars instead.
2. **`R-COLOR-01`**: Cap legend-dependent chart hues at 6–8 max.
3. **`R-LAYOUT-01`**: Put decision-relevant summaries before supporting detail where it serves the task.
4. **`R-TYPE-01`**: All numeric data uses monospace / tabular-nums font.
5. **`R-LAYOUT-08`**: Give charts enough room for their marks and labels; 180–200px is a useful starting point for many charts.
6. **`R-SPACE-03`**: Minimum 12px internal margin between card edge and chart.
7. **`R-CHART-05`**: Every chart needs a title. Axis labels when not self-evident.
8. **`R-COLOR-04`**: Same category → same color position across all charts.
9. **`R-CHART-07`**: Dual-axis charts are a default-avoid.
10. **`R-LAYOUT-12`**: Drill-down drawers slide from the right, width `min(520px, 92vw)`.
11. **`R-INSIGHT-01`**: Chart titles must state a finding, not describe an axis.
12. **`R-INSIGHT-03`**: Estimates/forecasts must show uncertainty ranges.
