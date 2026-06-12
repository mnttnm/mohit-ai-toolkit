# Widgets

> **When to use this file**: While building individual widgets (Layout → build phase).
> The anatomies, density limits, and squint test live here. Chart→primitive mapping and
> insight-text taxonomy live in [visualization.md](visualization.md); color tokens live in
> [design-system.md](design-system.md). This file does not repeat them.

---

## Widget anatomy is a MENU, not a mandate

A widget is a composed unit — visual + the interpretation around it. The composition is the
value; a bare chart with a title is not a dashboard widget. But "composed" is not "kitchen
sink." Each element below is on the **menu**, and earns its place by the gate beside it.
Include it when it pulls weight; skip it when it doesn't.

This is **not** a license to strip. Rich, interpretive widgets are the default and the
reason a real dashboard beats a generic one. The gate kills *gratuitous* elements
(boilerplate insight, "View details" CTA), not *valuable* ones. When in doubt on a rich
widget, keep it.

```
┌─────────────────────────────────────────────────────────────┐
│ [Icon] Title                              [Filter▼] [⋮] [⤢] │ ← HEADER
├─────────────────────────────────────────────────────────────┤
│ 💡 Insight: "APAC drove 60% of growth, up 34% YoY"         │ ← INSIGHT (contained banner — see below)
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                    VISUALIZATION                            │ ← VISUAL
│                                                             │
├─────────────────────────────────────────────────────────────┤
│ ● Series A  ● Series B  ● Series C    vs. Last Quarter     │ ← LEGEND / CONTEXT
├─────────────────────────────────────────────────────────────┤
│                                    [View Full Analysis →]   │ ← CTA
└─────────────────────────────────────────────────────────────┘
```

### Earns-its-place gate

| Element | Include when… | Skip / drop when… |
|---------|---------------|-------------------|
| **Title** | Always — name the metric, not the chart type. | (never skipped) |
| **Insight** | The data has a story the visual doesn't already show — a cause, comparison, anomaly, or implication. | The best you can write restates an axis ("Thursday was highest") or is boilerplate ("steady growth, +2%"). Let the chart speak. |
| **Visual** | Always — but only if the medium check (visualization.md §1) says a chart beats a number/sentence/table. | The value is a single number or delta — use a KPI tile, not a chart with one bar. |
| **Legend** | Multiple series that aren't directly labeled. | Single series, or series labeled at the line ends — direct labels beat a legend. |
| **Context line** | A comparison gives the number meaning — vs. target, vs. last period, vs. benchmark. | There's no honest baseline to compare against. |
| **CTA** | There's a real, specific next step or drill-down destination ("See 23 pending orders →"). | Only a generic "View details" / "More" fits — that's a dead end; drop it. |
| **Tooltip** | The chart has per-point detail worth surfacing on hover. | A KPI tile with nothing more to reveal. |
| **Loading / Empty / Error states** | **ALWAYS — the one true mandate.** Every widget that fetches data needs all three. See [edge-states.md](edge-states.md). | Never. |

The insight type (headline / callout / actionable / comparative) is the **canonical
taxonomy in [visualization.md §2](visualization.md)** — pick one type per widget; don't
stack all four. Don't restate it here.

### Where the insight goes — surfaced vs revealed

An insight is **contained** (a banner, never a loose colored line) and placed by how hard it
is to read off the data — the full rule, tones, and craft live in
[design-system.md → Surfacing insights](design-system.md). In short: **non-obvious →
surfaced** as an always-on banner at the *top* of the card (takeaway → data); **deducible →
hidden** behind a "Show insights" toggle at the top-right that reveals it at the top and
closes again. Either way the insight sits up top, so the card bottom is just metadata + the
CTA (CTA always right).

---

## KPI cards

The workhorse. The "full" anatomy below is the *menu* — a dense grid may want only the
minimal variant; a hero KPI may want all of it. Match the variant to the widget's job.

### Full KPI card
```
┌─────────────────────────────────────────┐
│ ◉ Monthly Revenue                    ⋮  │ ← Icon + label + actions menu
├─────────────────────────────────────────┤
│           $1.24M                        │ ← Primary value (32–40px bold, tabular-nums)
│     ↑ 15.3% vs last month               │ ← Trend (semantic color + context)
│ ▁▂▃▄▅▆▇█▇▆  Last 12 weeks               │ ← Sparkline + timeframe
│ Target: $1.5M                           │ ← Goal context
│ ████████████████░░░░  82.7%             │ ← Progress toward target
├─────────────────────────────────────────┤
│ 💡 On track to exceed Q4 target         │ ← Insight (earned)
├─────────────────────────────────────────┤
│                      [Forecast Q4 →]    │ ← CTA (earned, specific)
└─────────────────────────────────────────┘
```

### Variants — pick by density and job

**Minimal** (dense grids — value + label + trend only):
```
┌────────────────────────┐
│ Revenue      $1.24M    │
│              ↑ 15.3%   │
└────────────────────────┘
```

**Comparison** (this period vs last, side by side):
```
┌────────────────────────────────────────┐
│ Conversion Rate                        │
│   This Month        Last Month         │
│     4.8%              4.2%             │
│   ████████          ███████            │
│ 💡 +0.6pp from checkout redesign       │
│                        [Analyze →]     │
└────────────────────────────────────────┘
```

**Breakdown** (one metric, split by dimension):
```
┌────────────────────────────────────────┐
│ Total Users                    1.2M    │
│   Desktop    720K  ████████████  60%   │
│   Mobile     420K  ███████       35%   │
│   Tablet      60K  █              5%   │
│ 💡 Mobile growing fastest (+23% MoM)   │
│                    [View by Device →]  │
└────────────────────────────────────────┘
```

**Alert state** (threshold breached — value in error color, urgent CTA at top):
```
┌────────────────────────────────────────┐
│ ⚠️ Error Rate                 ALERT    │ ← Alert badge
├────────────────────────────────────────┤
│           2.4%                         │ ← Value in error color
│     ↑ 0.8% in last hour                │
│ Threshold: 1.5%  █████████████████░░   │
│ 💡 Spike correlates with deploy 14:32  │
│ [View Logs →]  [Acknowledge]           │ ← Action CTAs
└────────────────────────────────────────┘
```

Semantic colors (success / warning / error / info) and the trend up/down/flat colors are
**tokens — do not hardcode hex here**. Use the `--color-*` tokens from
[design-system.md](design-system.md). Never signal by color alone: pair with an icon,
arrow, or label (accessibility, design-system.md).

---

## Chart widgets

### Line / area chart
```
┌─────────────────────────────────────────────────────────────┐
│ Revenue Trend                                    [⤢] [⋮]   │
│ [Daily ▼] [Last 30 Days ▼]                                  │ ← Filters (earned)
├─────────────────────────────────────────────────────────────┤
│ 💡 Revenue peaked on Black Friday ($2.4M), 3x normal       │ ← Insight
├─────────────────────────────────────────────────────────────┤
│     $2.5M ┤                         ╱╲                      │
│     $2.0M ┤              ╱╲        ╱  ╲   ← "Black Friday"  │
│     $1.5M ┤    ╱╲       ╱  ╲    ╱      ╲     annotation     │
│     $1.0M ┤  ╱    ╲   ╱      ╲╱          ╲────             │
│     $0.5M ┤╱        ╲                                       │
│           └──────────────────────────────────────────────   │
│            Nov 1    Nov 8    Nov 15   Nov 22   Nov 29       │
├─────────────────────────────────────────────────────────────┤
│ ● Revenue ── Avg ($1.2M)  vs Last Year (gray)               │ ← Legend (multi-series)
├─────────────────────────────────────────────────────────────┤
│ Total: $38.4M  |  Avg: $1.28M  |  Peak: $2.4M               │ ← Summary stats
│                                    [View Daily Breakdown →] │ ← CTA
└─────────────────────────────────────────────────────────────┘
```

### Funnel
```
┌─────────────────────────────────────────────────────────────┐
│ Signup Funnel                             [This Week ▼] [⋮] │
├─────────────────────────────────────────────────────────────┤
│ 💡 Biggest drop-off at Email Verification (42% abandon)    │
│    Consider: reduce friction, add skip option               │ ← Actionable insight
├─────────────────────────────────────────────────────────────┤
│  Visited       ████████████████████████████  10,000  100%   │
│                          52% ▼                              │
│  Signed Up     ██████████████████             5,200   52%   │
│                          42% ▼                              │
│  Verified      ██████████████                 3,016   30%   │
│                          28% ▼                              │
│  Activated     ██████████                     2,171   22%   │
│                          35% ▼                              │
│  Purchased     ███████                        1,411   14%   │
├─────────────────────────────────────────────────────────────┤
│ Industry avg: 12%  │  Last month: 11%  │  Target: 18%       │ ← Context
│ [View by Source →]  [View by Cohort →]  [Export →]          │ ← Multiple CTAs
└─────────────────────────────────────────────────────────────┘
```

Horizontal, rectangular, proportional — **never** the pointy default `FunnelChart`. Build
details in [visualization.md §6](visualization.md).

### Heatmap
```
┌─────────────────────────────────────────────────────────────┐
│ User Activity by Day & Hour                          [⤢]   │
├─────────────────────────────────────────────────────────────┤
│ 💡 Peak: Tue-Thu 10am-12pm (3x avg). Dead: weekends <10am  │
├─────────────────────────────────────────────────────────────┤
│         Mon   Tue   Wed   Thu   Fri   Sat   Sun             │
│   8am   ▒▒    ▓▓    ▓▓    ▓▓    ▒▒    ░░    ░░              │
│  10am   ▓▓    ██    ██    ██    ▓▓    ▒▒    ░░              │
│  12pm   ▓▓    ██    ██    ██    ▓▓    ▒▒    ▒▒              │
│   2pm   ▒▒    ▓▓    ▓▓    ▓▓    ▒▒    ▒▒    ▒▒              │
│   6pm   ░░    ░░    ░░    ░░    ░░    ██    ██              │
│    ░ Low  ▒ Medium  ▓ High  █ Peak                         │ ← Legend
├─────────────────────────────────────────────────────────────┤
│ Click any cell for the detailed activity log               │
│                                   [Optimize Schedule →]     │ ← Action CTA
└─────────────────────────────────────────────────────────────┘
```

Use a sequential color ramp (the data-viz palette in [design-system.md](design-system.md)),
not arbitrary hues.

---

## Interactive data table

A table is a widget too — it earns an insight line and contextual, state-dependent row
actions, not one blanket "View" button.

```
┌─────────────────────────────────────────────────────────────────────┐
│ Customer Orders                                              [⤢]   │
│ 🔍 Search...   [Status ▼] [Date Range ▼] [+ Filter]   [Export ↓]   │
├─────────────────────────────────────────────────────────────────────┤
│ 💡 23 orders pending review (oldest: 3 days) — action needed       │
├───────────────┬──────────┬───────────┬────────────┬────────────────┤
│ Customer ▲    │ Status   │ Amount    │ Date       │ Actions        │
├───────────────┼──────────┼───────────┼────────────┼────────────────┤
│ Acme Corp     │ ● Paid   │   $12,450 │ 2 hrs ago  │ [View] [⋮]     │
│ TechStart Inc │ ◐ Pending│    $8,200 │ 1 day ago  │ [Review] [⋮]   │ ← CTA by state
│ GlobalCo      │ ● Paid   │   $24,100 │ 2 days ago │ [View] [⋮]     │
│ StartupXYZ    │ ○ Draft  │    $3,400 │ 3 days ago │ [Edit] [⋮]     │ ← CTA by state
├───────────────┴──────────┴───────────┴────────────┴────────────────┤
│ Showing 1-10 of 156  │  Total Value: $1.24M                        │
│                                            ◀ 1 2 3 ... 16 ▶        │
│ [+ New Order]                              [View All Orders →]      │
└─────────────────────────────────────────────────────────────────────┘
```

Amounts use `tabular-nums` and right-align (numeric craft, design-system.md). Status uses
icon **plus** color, never color alone.

---

## Implementation conventions

This file specifies *what* a widget contains. Translating that into code follows a few
standing conventions — the exact APIs you confirm at build time, not from memory.

**Detect, then match the project's chart library.** Run the project-context scan first
(`package.json`, a sample chart component). If the project already uses Recharts, Tremor,
visx, Chart.js, ECharts, Nivo, or a charting wrapper, **inherit it** — build every widget
in that library so the dashboard feels native. Don't introduce a second general-purpose
chart lib alongside an existing one.

**Greenfield default: Recharts + Tremor.** With no existing lib, reach for **Recharts** as
the base (line, area, bar, scatter, radar, the composable primitives) and **Tremor** for
complex or composed widgets — KPI cards with deltas, chart-plus-insight combos, bullets,
trackers — where its higher-level components save you from re-composing legends, value
formatting, and badges by hand. Pull a heavier dep (`@nivo/*`) only when the base stack
genuinely can't express a chart (e.g. sankey, sunburst), never as a casual second option.

**Use the library's vocabulary and its sane defaults.** Each chart maps to a small set of
primitives a practitioner reaches for — composable axis / grid / tooltip / legend
sub-components, a responsive container that owns sizing, accessor or `dataKey` props that
bind series to fields, and per-series color set from your tokens rather than the library's
stock palette. Lean on the defaults that are already good (responsive sizing, tooltips,
animation easing) and override only where this skill is opinionated: the funnel (never the
pointy built-in), `tabular-nums` on figures, axis formatting, and direct labels over a
legend where it reads cleaner.

**The chart→primitive mapping is canonical in
[visualization.md §6](visualization.md)** — which Recharts/Tremor component (or hand-built
CSS grid) backs each chart type, including how to compose a bullet, a clean funnel, a
waterfall, a bump. Don't repeat it; follow it.

**Build against CURRENT docs.** Chart-library APIs drift — prop renames, Tremor's shadcn
migration, new composition patterns. At build time, pull the live docs for the stack in
play (Recharts, Tremor, shadcn charts) via context7 or the web before writing chart code,
and verify component names, required props, and the current recommended composition. This
is non-optional; it's where memorized APIs silently break the build. (Detailed in
[visualization.md §7](visualization.md).)

**Tokens, not literals.** Series colors, semantic status colors, surfaces, text, and
spacing all come from the tokens in [design-system.md](design-system.md). Reference them;
don't paste hex into widget code.

---

## Density limits — don't cram

Rich does not mean crowded. A widget that tries to be six things reads as none. These are
the ceilings; respect them by promoting depth to a drill-down, not by shrinking type.

### Cramping anti-patterns

| Anti-pattern | Example | Fix |
|--------------|---------|-----|
| Multi-element cramping | Insight + funnel + CTA jammed into a KPI-sized card | Expand the card or split into two widgets |
| Information overload | >4 distinct facts in one KPI card | Prioritize; push the rest to drill-down |
| Missing whitespace | Sections touching with no padding | Consistent internal spacing (design-system.md) |
| Competing focal points | Several bold/large elements at once | One focal point per widget |

### Complexity ceiling by widget size

| Widget size | Max elements | Comfortable |
|-------------|--------------|-------------|
| Small KPI tile | 3 (value, label, trend) | 2–3 |
| Standard card | 5 (title, insight, visual, context, CTA) | 4–5 |
| Large card | 7 (add legend, filters) | 5–6 |
| Full-width panel | 10 | 7–8 |

### The squint test

Before finalizing any widget:

> **Squint at it. Can you identify 3 or fewer focal points?**

If no, it's too dense. In priority order: (1) move detail to hover or a drill-down, (2)
increase the card size, (3) drop the lowest-value element — never shrink type or kill
whitespace to make it fit.

Breathing room checklist: each section visibly separated · text not touching chart edges ·
CTA has a clear, padded tap target · insight not crammed under the title · legend items
spaced to read.
