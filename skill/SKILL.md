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
2. When generating dashboard code, **check each output** against the
   applicable rules before presenting to the user.
3. If a rule is violated, **cite the rule ID** and show the corrected version.
4. Rules are **data-driven defaults, not hard bans** — if the data context
   genuinely warrants an exception, state the exception and the reasoning.

## Rule categories

| Prefix        | Category                        | Count |
|---------------|---------------------------------|-------|
| `R-COLOR-*`   | Color system & palette          | 4     |
| `R-SPACE-*`   | Spacing & sizing                | 4     |
| `R-TYPE-*`    | Typography                      | 4     |
| `R-CHART-*`   | Chart selection & configuration | 10    |
| `R-LAYOUT-*`  | Layout hierarchy & grid         | 18    |
| `R-INTERACT-*`| Interaction patterns            | 3     |
| `R-STATE-*`   | Empty / loading / error states  | 3     |

## Quick reference — check these first

1. **`R-CHART-01`**: Pie charts are a strong default-avoid. Use horizontal bars instead.
2. **`R-COLOR-01`**: Cap legend-dependent chart hues at 6–8 max.
3. **`R-LAYOUT-01`**: KPI summary cards always above charts — inverted pyramid.
4. **`R-TYPE-01`**: All numeric data uses monospace / tabular-nums font.
5. **`R-LAYOUT-08`**: Minimum chart height is 180–200px — never compress below this.
6. **`R-SPACE-03`**: Minimum 12px internal margin between card edge and chart.
7. **`R-CHART-05`**: Every chart needs a title. Axis labels when not self-evident.
8. **`R-COLOR-04`**: Same category → same color position across all charts.
9. **`R-CHART-07`**: Dual-axis charts are a default-avoid.
10. **`R-LAYOUT-12`**: Drill-down drawers slide from the right, width `min(520px, 92vw)`.
