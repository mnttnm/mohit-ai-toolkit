# Visualization

> **When**: the Propose/Build phase — choosing a chart, writing its insight text, or
> reaching past basic bar/line. Single source for the **insight-text taxonomy**
> (headline / callout / actionable / comparative) and the chart catalog.

Rich charts and composed widgets are the **default** — they're what separate these
dashboards from traditional ones. This file is **not** a cull list. The right-medium
check below is a *guard* against gratuitous visuals, not a reason to start axing charts.

---

## 1. The right-medium check (a guard, not a cull)

Before reaching for a chart, confirm a chart is the right *medium* — but the bar is low.
A chart stays whenever it does real work (shows a trend, a flow, a pattern, a comparison
the eye reads faster than digits). Demote **only** decoration: a visual with no decision
behind it. **Default to keeping the rich visual.**

```
number / delta  →  sentence  →  table  →  chart  →  headline + link
   (1 figure)     (1 relation)  (lookup)  (pattern)   (just a pointer)
```

Walk left only when the heavier medium earns nothing. Most real widgets land at
**chart** — that's expected, not a failure.

### First lens: the data-fit check

The sharpest way gratuitous visuals sneak in: the chart *type* is conceptually right but
the *actual values* render visually identical.

> **Core question:** *Will users see a meaningful visual difference with this data?*

A visual adds value only when its differences are perceptible. Values like **91 / 91 / 95
/ 102** against a 120 target all render as near-identical bars — the chart hides the story
the numbers tell. Pivot to **numbers + delta chips**.

| Visual | Works when | Pivot away when |
|--------|-----------|-----------------|
| Progress bars | Values span a meaningful range | Values cluster — bars look identical |
| Bar / column | Differences visible at the chosen scale | Small differences get lost |
| Pie | Segments distinct and countable | Many small slices, or one dominates |
| Line | Trend is visible and meaningful | Line is essentially flat |
| Heatmap | Color gradations distinguishable | Values compress to one color band |

**Conceptual choice:** "value vs target → progress bar." **Data-driven choice:** "values
are 91/91/95/102 of 120 — near-identical bars; delta chips communicate better."

When the data defeats the visual, pivot to: numbers + comparison text · delta chips
(`+2.3%`) · gap framing (distance from target) · rankings (`#1 #2 #3`).

> The data-fit check **demotes a handful of widgets to numbers**. It does not license
> stripping the chart layer wholesale. Everything that survives the check stays rich.

---

## 2. Charts + insights

Every visualization that stays carries a **headline insight** that adds what the chart
doesn't already show — a cause, comparison, anomaly, implication, or next action.

```
VISUALIZATION = CHART + INSIGHT TEXT + CONTEXT
  Chart alone:        "Here's the data"
  Chart + insight:    "Revenue up 23%, driven by APAC"
```

The test: *would a sharp analyst bother saying this out loud?* If the best you can write
restates the axis ("Thursday was highest"), drop the band — let the chart speak. No
boilerplate ("steady growth, +2%").

### Insight-text taxonomy (canonical — other files reference this)

| Type | Answers | Example |
|------|---------|---------|
| **Headline** | What's the story? | "Revenue up 23% — strongest quarter since Q2 2022" |
| **Callout** | What's notable / anomalous? | "Unusual spike March 15 — investigate" · "3 of 5 targets exceeded" |
| **Actionable** | What do I do next? | "Activation drop is the bottleneck → review onboarding" |
| **Comparative** | How does it compare? | "23% above industry average" · "Down 5% vs. last year" |

A widget usually carries **one** of these, not all four. Pick the type the data most
strongly supports. Annotations (events marked directly on the chart — "Product launch",
"Price change") are the in-chart form of a callout.

---

## 3. Selecting the chart

### By data question (canonical)

| Question | Default | Upgrade to |
|----------|---------|-----------|
| How much? | KPI card / big number | **Bullet** for target context |
| How has it changed? | Line, Area | **Slope** (before/after) · **Bump** (rank changes) |
| How do these compare? | Bar, Column | **Radar** (5–8 attributes) · **Bullet** (vs target) |
| What's the composition? | Stacked bar, Treemap | Sunburst (deep hierarchy) · **Waterfall** (sums to total) |
| What's the flow / conversion? | **Funnel**, **Sankey** | — (always, for sequential / multi-path flow) |
| What's the pattern? | **Heatmap** | Calendar heatmap (daily over months) |
| What's the relationship? | Scatter | Bubble (3rd dimension) · Connected scatter (over time) |
| How is it distributed? | Histogram, Box plot | Violin (shape comparison) |
| What's the rank change? | **Bump** | — |
| What drives the total? | **Waterfall** | — |
| Where is it? | Choropleth, Point map | Cartogram (emphasis by value) |

### Upgrade guide — escape the default

| Instead of | Consider | When |
|-----------|----------|------|
| Bar | Radar | Comparing 5–8 attributes |
| Stacked bar | Funnel | Conversion / drop-off |
| Multiple bars | Waterfall | Component contributions to a total |
| Line | Bump | Rankings matter, not absolute values |
| Grouped bars | Slope | Only two time points |
| Table | Heatmap | Pattern recognition is the goal |
| Flow diagram | Sankey | Multiple paths to show |
| Gauge | Bullet | Target comparison needed |

---

## 4. Advanced chart catalog (don't avoid these — they earn their keep)

Each entry: **best for** / **avoid when** / what it's actually built from (§6).

| Chart | Best for | Avoid when |
|-------|----------|-----------|
| **Radar / Spider** | Multi-dimensional comparison, 5–8 attributes (product vs product, skills, competitor factors) | More than 8 attributes; precise reading required |
| **Heatmap** | Patterns across two categorical dims (day × hour, region × product, cohort, correlation) | Precise values needed |
| **Funnel** | Sequential drop-off (pipeline, onboarding, checkout, recruitment) | Non-sequential data |
| **Sankey** | Flow between categories, budget/traffic allocation, journey mapping | Simple A→B flow |
| **Waterfall** | How components sum to a total (revenue bridge, profit breakdown, variance) | Non-additive data |
| **Bump** | Ranking changes over time (market share, leaderboards, adoption) | Absolute values matter more than rank |
| **Bullet** | KPI with target + performance bands (vs quota, vs benchmark) | No target exists |
| **Slope** | Two-point before/after (YoY, pre/post intervention) | More than 2 time points |
| **Treemap / Sunburst** | Hierarchical part-to-whole | Deeper than ~3 levels (treemap) |

**Funnel for attrition** stays — it tells the "trimmed at each stage" story a bar can't
(`10,000 → 5,200 → 2,800 → 1,400 → 700`, biggest drop flagged). But it **must render
cleanly** (see §5).

### Chart by data shape (cross-cut)

- **Time** — single metric → Line; multi-metric → multi-line / small multiples;
  part-to-whole → stacked area; discrete periods → Column; before/after → Slope; rank →
  Bump; cyclical (day/week) → Heatmap.
- **Categorical** — <7 → Bar/Column; 7+ → horizontal bar, sorted; multi-attribute →
  Radar; hierarchical → Treemap/Sunburst; two dims → Heatmap.
- **Flow/process** — drop-off → Funnel; multiple paths → Sankey; breakdown → Waterfall;
  steps → Timeline/Gantt.
- **Distribution/relationship** — two vars → Scatter; three → Bubble; shape → Histogram /
  Violin; compare → Box plot; correlation → Heatmap.

---

## 5. Selection ≠ execution

Picking the right chart is half the job. A correctly-chosen chart, rendered badly, fails.
Run this checklist on every chart before it ships:

- **Funnel** — render a **clean horizontal stepped funnel** (rectangular stages,
  decreasing width). **Not** Recharts' default `FunnelChart`, which draws a pointy
  trapezoid/triangle that distorts the proportions.
- **Figures** — `tabular-nums` (or `font-variant-numeric: tabular-nums`) on every numeric
  column, axis tick, and KPI so digits align and don't jitter on update.
- **Axis & legend hygiene** — labels present and formatted (currency, %, K/M); no clipped
  or overlapping ticks; legend only for multi-series, else direct labels; consistent
  decimal places.
- **No clipped content** — long category labels truncate with tooltip or rotate
  deliberately; nothing runs off the plot area; adequate margins.
- **Colorblind-safe encoding** — never encode meaning by hue alone. Pair color with
  position, label, pattern, or icon. Verify the palette survives deuteranopia.
- **Meaningful color** — color carries data (category / sequence / divergence / status),
  never decoration. Max 5–6 categorical colors.

### When NOT to use

- **Pie** — avoid >5 slices, similar-sized slices, precise comparison, or multiple pies
  side by side. Only when one slice is dramatically >50%.
- **3D** — never. It distorts perception.
- **Dual axis** — avoid; it manufactures false correlations. If unavoidable, label and
  differentiate both axes explicitly.
- **Gauge / dial** — almost always worse than a **bullet** chart. Only when literally
  mimicking a real-world gauge.

### Perceptual accuracy (Cleveland–McGill)

For **precision** tasks, encodings rank by how accurately the eye decodes them:

1. Position on a common scale (most accurate)
2. Length
3. Angle / slope
4. Area
5. Color saturation (least accurate)

**But precision isn't always the goal.** A radar comparing products is more memorable
than a grouped bar, even if slightly less precise. **Rule:** high-accuracy encodings for
critical comparisons; engaging encodings for storytelling and pattern-spotting.

---

## 6. Chart type → library primitive (conventions, not code)

Greenfield default stack: **Recharts** for base charts, **Tremor** for complex/composed
widgets (chart + insight combos, KPI cards with deltas, bullets). If the project already
has a chart lib, **inherit it** — translate these conventions to that lib.

- **KPI card / big number** — Tremor `Card` + `Metric` + `BadgeDelta`, or a plain
  styled div. `tabular-nums` on the figure.
- **Line / area / bar / column** — Recharts `LineChart` / `AreaChart` / `BarChart`, or
  Tremor's `LineChart` / `BarChart` wrappers when you want built-in legends and value
  formatting.
- **Bullet** — compose, don't import a "gauge": a thin horizontal `BarChart` (the measure)
  over banded background `ReferenceArea`s (qualitative ranges) with a `ReferenceLine` for
  the target. Tremor's tracker/progress primitives can stand in.
- **Funnel** — **do not** use Recharts `FunnelChart`. Build a clean stepped funnel from a
  horizontal `BarChart` with one decreasing bar per stage (each row labeled with count +
  % retained), or a CSS/flex stack of width-scaled rows. Horizontal, rectangular,
  proportional.
- **Radar** — Recharts `RadarChart` (`PolarGrid` / `PolarAngleAxis` / `Radar`). Cap at
  8 axes.
- **Heatmap** — neither lib ships one; build a CSS grid of cells with a sequential color
  scale (e.g. d3-scale or a token ramp from design-system.md), or `@nivo/heatmap` if a
  heavier dep is acceptable.
- **Sankey** — Recharts `Sankey`, or `@nivo/sankey` for richer link styling.
- **Waterfall** — Recharts stacked `BarChart` with a transparent "base" series offsetting
  each bar to its running total; color rising vs falling segments distinctly.
- **Bump** — Recharts `LineChart` plotting *rank* (invert the Y axis) with one line per
  series and direct end labels; or `@nivo/bump`.
- **Slope** — Recharts `LineChart` with exactly two X points and direct labels at each
  end; no gridlines.
- **Treemap / Sunburst** — Recharts `Treemap`; sunburst via `@nivo/sunburst`.

Pull only the heavier deps (`@nivo/*`) when the base stack genuinely can't express the
chart — don't add a second general-purpose chart lib.

---

## 7. Build against CURRENT docs

Chart-library APIs drift (prop renames, new composition patterns, Tremor's shadcn
migration). **Do not rely on memorized APIs.** At build time, pull the current docs for
the stack in play — **Recharts, Tremor, and shadcn charts** — via context7
(`resolve-library-id` → `query-docs`) or web. Verify component names, required props, and
the current recommended composition before writing chart code.

---

## 8. Complete widget specification

Define these for any non-trivial widget (most are conditional — earn each one):

- **Type & purpose** — chart type + the question it answers + data fields/aggregations.
- **Insight text** — one taxonomy type (§2): headline / callout / actionable / comparative.
- **Visual config** — palette (with meaning), axis labels/format/range, legend or direct
  labels, annotations.
- **Interactivity** — hover tooltip content, click drill-down destination, filterable
  fields.
- **Context line** — comparison baseline ("vs. last quarter · Target $12M, 90% met").
- **CTA** — earned and specific ("View full funnel analysis →"), never generic "View
  details". See information-architecture.md.
- **States** — loading / empty / error (always required — see edge-states.md).

---

## Anti-patterns

- **Default-to-bar reflex** — "it's a comparison → bar" when it's a 6-factor comparison
  (radar) or sequential drop-off (funnel) or multi-path flow (Sankey).
- **Chart with only a title** — no earned insight.
- **Values that render identical** — failed the data-fit check; use numbers + deltas.
- **≥3 widgets all collapsing to horizontal bars** — differentiate at least one.
- **The pointy default funnel** — use a clean horizontal stepped funnel.
- **Decorative color** — hue without data meaning; or meaning by hue alone (colorblind-unsafe).
- **Dead-end chart** — no drill-down, no next action.

> Tokens (hex, palette ramps, semantic colors) live in **design-system.md** — reference,
> never re-list here.
