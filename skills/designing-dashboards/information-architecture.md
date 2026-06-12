# Information Architecture Reference

> **When to use this file**: When planning dashboard layout structure, choosing between layout patterns (hero, magazine, bento, hub & spoke, etc.), establishing visual hierarchy, designing the dashboard-level interaction model (filters, date range, drill-down, URL state), or breaking away from the default "4 KPIs + 2 charts + table" layout.

---

## Philosophy: The Dashboard Is a Launchpad

```
┌─────────────────────────────────────────────────────────────┐
│  ❌ DEFAULT THINKING:                                       │
│     "4 KPIs on top, 2 charts below, table at bottom"       │
│                                                             │
│  ❌ EVERYTHING-PAGE THINKING:                              │
│     "Cram every metric, every breakdown, every table       │
│      onto one screen so nothing needs a second click"      │
│                                                             │
│  ✓  LAUNCHPAD THINKING:                                     │
│     "Headline + entry points. What's the story, what's     │
│      the focal point, and where does each widget LAUNCH     │
│      the user when they want to go deeper?"                 │
└─────────────────────────────────────────────────────────────┘
```

A dashboard is a **launchpad, not an everything-page**: a headline layer (the
focal metric and its story) plus a set of **entry points** (widgets that each
open onto a dedicated drill-down view). This is about the **placement of depth**,
not the removal of it. The richness stays — composed widgets, insight bands, and
comparative views all earn their place. What changes is *where the deepest layer
lives*: a row-level table, a full cohort breakdown, a per-entity history belongs
on a drill-down page that the dashboard *links to*, not stacked onto the home
screen until it scrolls forever.

The test for the home screen: **does this widget help the user decide where to go
next?** If yes, it's an entry point — keep it. If it's exhaustive reference detail
that only matters once you've already decided to investigate, it's drill-down
content — link to it.

> Rich by intent, not by reflex. Pushing depth to drill-down views is a
> *placement* decision, never a license to strip widgets in the name of
> "simplicity." See SKILL.md, Principle 5.

## Layout Pattern Library

### 1. Hero Focal Layout
**Use for**: Dashboards with one dominant metric or visualization

A large central visual commands attention, with supporting metrics arranged around it.

```
┌─────────────────────────────────────────────────────────────┐
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐        │
│  │ KPI 1   │  │ KPI 2   │  │ KPI 3   │  │ KPI 4   │        │
│  │ $1.2M   │  │ 4.8%    │  │ 2,847   │  │ 94%     │        │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘        │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                                                     │   │
│  │                                                     │   │
│  │              HERO VISUALIZATION                     │   │
│  │           (Large, commanding attention)             │   │
│  │                                                     │   │
│  │                                                     │   │
│  │                                                     │   │
│  └─────────────────────────────────────────────────────┘   │
│  💡 Key insight text spanning full width                   │
│                                      [Explore Details →]   │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Executive dashboards, single-focus monitoring, storytelling

### 2. Magazine / Editorial Layout
**Use for**: Data stories with narrative flow

Asymmetric layout that guides the eye through a sequence.

```
┌─────────────────────────────────────────────────────────────┐
│  THE STORY                                                  │
│  ═══════════════════════════════════════════════════════    │
│                                                             │
│  ┌───────────────────────────────┐  ┌───────────────────┐  │
│  │                               │  │ Q4 Performance    │  │
│  │   LARGE FEATURE CHART         │  │                   │  │
│  │                               │  │ Revenue  $4.2M    │  │
│  │   Revenue trend with          │  │          ↑ 23%    │  │
│  │   annotated story points      │  │                   │  │
│  │                               │  │ Users    1.2M     │  │
│  │                               │  │          ↑ 15%    │  │
│  └───────────────────────────────┘  │                   │  │
│                                     │ Margin   34%      │  │
│  💡 "Revenue surged after the      │          ↑ 2pp    │  │
│     October product launch..."      └───────────────────┘  │
│                                                             │
│  ┌─────────────────┐  ┌─────────────────┐  ┌────────────┐  │
│  │  By Region      │  │  By Product     │  │  Outlook   │  │
│  │  [breakdown]    │  │  [breakdown]    │  │  [forecast]│  │
│  └─────────────────┘  └─────────────────┘  └────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Weekly reports, board presentations, investor updates

### 3. Hub and Spoke Layout
**Use for**: Central metric with related dimensions

One central element with radiating related information.

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│             ┌─────────────────┐                             │
│             │   By Channel    │                             │
│             │   [breakdown]   │                             │
│             └────────┬────────┘                             │
│                      │                                      │
│  ┌──────────┐   ┌────┴────┐   ┌──────────┐                 │
│  │By Region │───│  CORE   │───│By Product│                 │
│  │[breakdown│   │  KPI    │   │[breakdown│                 │
│  └──────────┘   │ $4.2M   │   └──────────┘                 │
│                 │ Revenue │                                 │
│                 └────┬────┘                                 │
│                      │                                      │
│             ┌────────┴────────┐                             │
│             │   By Segment    │                             │
│             │   [breakdown]   │                             │
│             └─────────────────┘                             │
│                                                             │
│  Click any dimension to drill down                          │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Exploratory dashboards, dimensional analysis, interactive reporting

### 4. Bento Box Layout
**Use for**: Dense information with visual variety

Mixed-size containers creating visual interest while maximizing information.

```
┌─────────────────────────────────────────────────────────────┐
│  ┌───────────────────────┐  ┌─────────┐  ┌─────────┐       │
│  │                       │  │         │  │  KPI 3  │       │
│  │   LARGE CHART         │  │  KPI 1  │  │  2,847  │       │
│  │   (2x2 cells)         │  │  $1.2M  │  └─────────┘       │
│  │                       │  │         │  ┌─────────┐       │
│  │                       │  └─────────┘  │  KPI 4  │       │
│  │                       │  ┌─────────┐  │  94%    │       │
│  └───────────────────────┘  │  KPI 2  │  └─────────┘       │
│  ┌───────────┐  ┌───────────┤  4.8%   │  ┌─────────────┐   │
│  │  MINI     │  │  MINI     │         │  │             │   │
│  │  CHART 1  │  │  CHART 2  └─────────┘  │  MEDIUM     │   │
│  │           │  │           │            │  CHART      │   │
│  └───────────┘  └───────────┘            │             │   │
│                                          └─────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Operations dashboards, monitoring, data-rich displays

### 5. Comparison / Split Layout
**Use for**: Before/after, this vs that, A/B analysis

Side-by-side structure for direct comparison.

```
┌─────────────────────────────────────────────────────────────┐
│            THIS PERIOD          │       LAST PERIOD         │
│  ════════════════════════════   │  ════════════════════════ │
│                                 │                           │
│  ┌─────────────────────────┐   │   ┌─────────────────────┐ │
│  │  Revenue: $4.2M         │   │   │  Revenue: $3.4M     │ │
│  │  ████████████████       │   │   │  █████████████      │ │
│  │  ↑ 23.5%                │   │   │                     │ │
│  └─────────────────────────┘   │   └─────────────────────┘ │
│                                 │                           │
│  ┌─────────────────────────┐   │   ┌─────────────────────┐ │
│  │  [Trend Chart]          │   │   │  [Trend Chart]      │ │
│  │                         │   │   │                     │ │
│  └─────────────────────────┘   │   └─────────────────────┘ │
│                                 │                           │
│  💡 Key driver: APAC growth    │   Reference period        │
│                                 │                           │
│           [View Full Comparison Analysis →]                 │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Period comparisons, A/B test results, competitive analysis

### 6. Funnel / Flow Layout
**Use for**: A conversion process or any staged flow with drop-off

Vertical or horizontal flow showing stages. *Domain-agnostic*: any sequential
process where entities advance and attrit between stages — onboarding, checkout,
hiring, support escalation — maps to this pattern, not just a sales funnel.

```
┌─────────────────────────────────────────────────────────────┐
│  Stage Flow                                                 │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              STAGE 1 (entry)                        │   │
│  │  Entered: 100,000        Input cost: $50K           │   │
│  └─────────────────────────────────────────────────────┘   │
│                        │ 52% advance                        │
│                        ▼                                    │
│       ┌────────────────────────────────────────┐           │
│       │           STAGE 2                      │           │
│       │  Advanced: 52,000    Cost/unit: $0.96  │           │
│       └────────────────────────────────────────┘           │
│                        │ 35% advance                        │
│                        ▼                                    │
│            ┌──────────────────────────────┐                │
│            │       STAGE 3               │                │
│            │  Converted: 18,200  AOV: $85 │                │
│            └──────────────────────────────┘                │
│                        │ 42% return                         │
│                        ▼                                    │
│                 ┌──────────────────┐                       │
│                 │   STAGE 4        │                       │
│                 │  Retained: 7,644 │                       │
│                 └──────────────────┘                       │
│                                                             │
│  💡 Biggest opportunity: Stage 2 → Stage 3 (35% advance)  │
│                                  [Optimize Flow →]         │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Conversion processes, multi-stage journeys, process efficiency

### 7. Timeline / Narrative Layout
**Use for**: Chronological data stories

Horizontal timeline with events and metrics.

```
┌─────────────────────────────────────────────────────────────┐
│  Performance Story (time series with event markers)         │
│                                                             │
│  ══════════════════════════════════════════════════════════ │
│     P1          P2          P3          P4                  │
│      │           │           │           │                  │
│      │           │           │           │                  │
│  ────●───────────●───────────●───────────●────────────────  │
│      │           │           │           │                  │
│   Event A     Event B     Event C     Event D              │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                                                     │   │
│  │             PRIMARY TIME SERIES                     │   │
│  │           (with event annotations)                  │   │
│  │                                                     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  [← Prior Period]                       [Next Period →]    │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Annual reviews, project timelines, historical analysis

### 8. Contextual Sidebar Layout
**Use for**: Main content with persistent context

Primary area with supporting information always visible. The sidebar is also the
natural home for the **global filter bar** and active-filter context (see
*Dashboard-Level Interaction Model* below).

```
┌─────────────────────────────────────────────────────────────┐
│  ┌───────────────────────────────────────┬────────────────┐ │
│  │                                       │  CONTEXT       │ │
│  │                                       │                │ │
│  │                                       │  Period: Q4    │ │
│  │                                       │  Region: All   │ │
│  │        MAIN CONTENT AREA              │  Segment: B2B  │ │
│  │                                       │                │ │
│  │        (Charts, tables, etc.)         │  ──────────    │ │
│  │                                       │                │ │
│  │                                       │  Key Metrics:  │ │
│  │                                       │  • Rev: $4.2M  │ │
│  │                                       │  • Users: 1.2M │ │
│  │                                       │  • NPS: 72     │ │
│  │                                       │                │ │
│  │                                       │  ──────────    │ │
│  │                                       │                │ │
│  │                                       │  Quick Actions │ │
│  │                                       │  [Export]      │ │
│  │                                       │  [Share]       │ │
│  │                                       │  [Schedule]    │ │
│  └───────────────────────────────────────┴────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Analysis tools, exploration interfaces, filtered views

### 9. Quadrant Layout
**Use for**: Balanced four-perspective view

Four equal sections for comprehensive coverage.

```
┌─────────────────────────────────────────────────────────────┐
│  Business Overview                                          │
│  ┌──────────────────────────┬──────────────────────────┐   │
│  │                          │                          │   │
│  │    📈 REVENUE            │    👥 CUSTOMERS          │   │
│  │                          │                          │   │
│  │    $4.2M  ↑ 23%          │    12,450  ↑ 15%         │   │
│  │    [trend chart]         │    [trend chart]         │   │
│  │                          │                          │   │
│  │    [Revenue Details →]   │    [Customer Details →]  │   │
│  ├──────────────────────────┼──────────────────────────┤   │
│  │                          │                          │   │
│  │    📦 OPERATIONS         │    💰 PROFITABILITY      │   │
│  │                          │                          │   │
│  │    2,847 orders  ↑ 8%    │    34% margin  ↑ 2pp     │   │
│  │    [trend chart]         │    [trend chart]         │   │
│  │                          │                          │   │
│  │    [Operations →]        │    [Financials →]        │   │
│  └──────────────────────────┴──────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

**Best for**: Balanced scorecards, multi-department views, startup metrics

## Layout Selection Guide

| Dashboard Purpose | Recommended Layouts |
|-------------------|---------------------|
| Executive summary | Hero Focal, Magazine |
| Operations monitoring | Bento Box, Quadrant |
| Conversion / staged process | Funnel Flow, Comparison |
| Exploration/analysis | Hub & Spoke, Contextual Sidebar |
| Reporting/presentation | Magazine, Timeline |
| Single-focus monitoring | Hero Focal |
| Multi-dimensional | Hub & Spoke, Quadrant |

---

## Dashboard-Level Interaction Model

Individual widgets get their own CTAs and click behavior (SKILL.md Principle 4;
per-widget destinations live in visualization.md's spec). This section is the
layer *above* that: the controls and state that bind the whole board together.
Principle-level — decide the model, not the code.

### Global filter bar

A single control region (top of board, or the sidebar in the Contextual Sidebar
layout) holds the filters that apply across widgets — dimension selectors
(region, segment, channel), search, and the date-range control.

**Cascade rule**: a global filter cascades to **every widget bound to that
dimension** simultaneously. Changing "Region: APAC" re-scopes the headline KPI,
the breakdowns, and the time series in one action — the board stays internally
consistent. Widgets that are intentionally global (e.g. an all-up benchmark) opt
*out*, and should visibly signal that they ignore the filter so the user never
mistakes a global number for a filtered one.

```
┌─────────────────────────────────────────────────────────────┐
│ [Region: APAC ▾] [Segment: All ▾] [Channel: All ▾]  🔍       │ ← cascades to bound widgets
│ [ Last 30 days ▾ ]                  [Saved: "APAC weekly" ▾]  │ ← date range + saved view
├─────────────────────────────────────────────────────────────┤
│  Headline KPI (APAC)     Breakdown (APAC)     Trend (APAC)    │ ← all re-scoped together
└─────────────────────────────────────────────────────────────┘
```

### Date-range control

The time window is a first-class, board-wide control, not a per-widget setting.
Offer relative presets (last 7 / 30 / 90 days, QTD, YTD) plus a custom range, and
**echo the active range** wherever comparisons appear ("vs. prior 30 days") so
deltas are never ambiguous. If one widget must pin a different window (e.g. an
always-trailing-12-month trend), label that exception on the widget.

### URL / saved-view state

Filter selections, date range, and the active drill-down should serialize into the
**URL** (or an equivalent shareable state token). This makes any board view
linkable, bookmarkable, and reproducible — paste the link, land on the same
filtered state. Layer **saved views** on top for recurring scopes a user returns to
("APAC · weekly · B2B"). State that survives a refresh and a paste is a correctness
property, not a nicety: a screenshotted "down 12%" must be reconstructable from its
link.

### Drill-down destinations (the launchpad payoff)

Entry-point widgets must launch onto a **real destination**, not a hand-wavy
"View details." State the concrete target as part of the layout spec:

| Widget (entry point) | Concrete drill-down destination |
|---|---|
| Ranked-entities widget (e.g. top performers) | Per-entity detail view, pre-filtered to the clicked entity |
| Time-series widget | Expanded time-series explorer with granularity toggle + annotations |
| Breakdown-by-dimension widget | That dimension's full table view, inheriting the current global filters |
| Conversion-process widget | Stage-level diagnostic for the clicked stage (cohort, reasons, segment) |
| Alert / exception widget | The underlying record(s) that triggered the exception |

Two placement rules:

- **Inherit context.** A drill-down opens with the board's current global filters
  and date range already applied — the user shouldn't re-specify what they just
  set. (This is the WHERE of actionability; for CTA *wording* and per-widget click
  behavior, see SKILL.md Principle 4 and visualization.md.)
- **Depth goes to the destination, not the tile.** If a widget is tempted to grow a
  full table or a long history inline, that's the signal to push it to the
  drill-down view and keep the home tile a headline + entry point.

---

## Reconciling "Single Screen" with Richer Narrative Layouts

There's a real tension here, and it shouldn't be settled by decree.

- **The single-screen / minimal-scroll instinct** suits glanceable, monitoring
  use: an operator needs the whole state in one view, no scrolling, exceptions
  surfaced fast.
- **Richer narrative layouts** (Magazine, Timeline, a tall scrollytelling story)
  deliberately use vertical space to walk the reader through a sequence — and for
  reporting/presentation audiences that *is* the value.

Neither is universally right. **Let the audience archetype and the visualization
density budget decide** — both established upstream in strategy.md
(the audience-archetype → density-budget mapping). The flow:

```
Audience archetype + density budget (strategy.md)
        │
        ├─ Glanceable / operational, lean budget
        │     → favor single-screen; push depth to drill-down; minimal scroll
        │
        └─ Narrative / analytical / presentation, richer budget
              → a guided scroll is legitimate; sequence beats compression
```

The launchpad principle holds either way: **scroll length is never an excuse to
become an everything-page.** A narrative board scrolls because the *story* needs
the room, not because exhaustive reference detail was dumped onto the home screen
instead of a drill-down view. When in doubt, ask: is this length serving a sequence
the reader follows, or is it just deferred drill-down content?

---

## Variety Check (Board-Level Composition)

Beyond choosing each chart well, step back and read the **whole board as one
composition**. A common failure: every widget independently resolves to a
horizontal bar, and the page becomes a wall of near-identical bars — visually
monotonous even when each individual choice was defensible.

**The check**: if **3+ widgets** on the board resolve to horizontal bars,
differentiate at least one. This is an IA / composition concern — about the gestalt
of the screen, not any single widget's correctness.

The *fix* is a chart-type decision, and that lives in visualization.md — a cluster
of ranked-entity bars might become a slope view, a bump chart, a heatmap, or numbers
+ deltas depending on the data. **Don't re-decide chart selection here**; just flag
the monotony at the board level and route the remedy to visualization.md.

(This pairs with the data-fit check in visualization.md, which catches the
*opposite* problem — a single chart whose values render visually identical.)

---

## Visual Hierarchy Principles

### The Gutenberg Principle (Still Applies)
```
┌─────────────────────────────────────┐
│  1. PRIMARY          2. STRONG      │  ← Eyes start here
│     (Critical KPI)      (Important) │
│                                     │
├─────────────────────────────────────┤
│  3. WEAK             4. TERMINAL    │  ← Eyes end here
│     (Supporting)        (Actions)   │
└─────────────────────────────────────┘
```

But modern layouts can guide the eye with:
- **Size contrast** — Larger elements attract first
- **Color accent** — Pop of color draws attention
- **Isolation** — Whitespace around important elements
- **Visual flow** — Lines, arrows, connected elements

### Cognitive Load Management

**The 7±2 Rule**: Maximum information chunks visible at once.

**Chunking strategies**:
```
✓ Group related KPIs into one "Financial Health" section
✓ Collapse detail into expandable sections
✓ Use progressive disclosure (summary → detail on click)
✓ Visual containers create natural groups
```

The 7±2 ceiling is the launchpad's discipline in disguise: when chunk count climbs
past it, the answer is usually to **route a chunk to a drill-down view**, not to
shrink everything until it's illegible.

## Grid System Flexibility

### Standard 12-Column (For Card Layouts)
```
│ 1│ 2│ 3│ 4│ 5│ 6│ 7│ 8│ 9│10│11│12│
├──┴──┴──┼──┴──┴──┼──┴──┴──┼──┴──┴──┤
│  3 col │  3 col │  3 col │  3 col │  ← 4 equal columns
├────────┴────────┼────────┴────────┤
│     6 col       │     6 col       │  ← 2 halves
├─────────────────┴─────────────────┤
│           12 col (full)           │  ← Full width
```

### Breaking the Grid (For Creative Layouts)
```
Hero Layout:
│ 2│ 2│ 2│ 2│ 2│ 2│     ← 6 mini KPIs
├──┴──┴──┴──┴──┴──┴──┴──┴──┴──┴──┴──┤
│            12 col HERO            │     ← Full-width focal
└───────────────────────────────────┘

Magazine Layout:
├────────────────┬─────────┤
│    8 col       │  4 col  │     ← Asymmetric split
│   Feature      │  Stats  │
├────────────────┴─────────┤
│          12 col          │
└──────────────────────────┘
```

## Layout Specification Template

```markdown
## Layout: [Name]

### Pattern
- Type: [Hero / Magazine / Bento / etc.]
- Rationale: [Why this pattern fits the use case]

### Visual Hierarchy
1. Primary focus: [What draws attention first]
2. Secondary elements: [What comes next]
3. Supporting content: [Background information]
4. Actions: [Where CTAs live]

### Grid Structure
- Columns: [12-column breakdown]
- Breakpoints: [Desktop / Tablet / Mobile adaptations]

### Section Breakdown
| Section | Content | Span | Purpose |
|---------|---------|------|---------|
| [Name] | [What's in it] | [Cols] | [Why] |

### Interaction Model
- Global filters: [Which dimensions cascade across widgets]
- Date range: [Presets + default window; any per-widget exceptions]
- URL / saved-view state: [What serializes; named saved views]

### Navigation & Flow
- Eye flow: [Describe how eye travels]
- Drill-down paths: [Each entry point → its CONCRETE destination, with inherited filters]
- Exit points: [CTAs and their destinations]

### Single-screen vs. scroll
- Decision: [Single-screen / guided scroll] — driven by [archetype + density budget]
```

## Architecture Checklist

### Layout Choice
- [ ] Selected layout pattern matches dashboard purpose
- [ ] Considered creative options (not default card grid)
- [ ] Focal point identified if applicable
- [ ] Visual flow guides the narrative

### Launchpad Discipline
- [ ] Home screen is headline + entry points, not an everything-page
- [ ] Exhaustive reference detail pushed to drill-down views, not stacked inline
- [ ] Single-screen vs. scroll decided by archetype + density budget (strategy.md), not by reflex

### Interaction Model
- [ ] Global filter bar defined; cascade behavior across widgets is explicit
- [ ] Date-range control is board-level; comparisons echo the active range
- [ ] Filter + range + drill-down state serialize to URL; saved views considered
- [ ] Every entry-point widget names a CONCRETE drill-down destination (not "View details")
- [ ] Drill-down views inherit the board's current filters and date range

### Information Priority
- [ ] Most critical info in highest-attention position
- [ ] Related items visually grouped
- [ ] Clear visual hierarchy (size, color, position)
- [ ] Cognitive load managed (7±2 chunks)

### Composition Variety
- [ ] Board doesn't collapse to a wall of bars (3+ horizontal bars → differentiate one; remedy in visualization.md)

### Responsiveness
- [ ] Desktop layout defined
- [ ] Tablet adaptation planned
- [ ] Mobile prioritization decided
