# Strategy Reference

> **When to use this file**: At the Strategy gate — classify the dashboard type, infer
> the **audience archetype**, set the **visualization density budget**, and prioritize
> metrics. Run after requirements; feeds layout (information-architecture.md) and the
> right-medium check (visualization.md).

Strategy is where you decide **what the dashboard is for** and **how much to visualize**.
The density budget is a *tuning knob, not a cull*: it sets how rich each region should be
for this audience — every chart still earns its place via the right-medium check. Glanceable
≠ stripped; it means *fewer, bigger, calmer* widgets with depth pushed to drill-down.

---

## Strategy Process

```
1. Read requirements → infer dashboard type + audience archetype
2. PROPOSE type + archetype + density budget (with reasoning) → confirm
3. PROPOSE metric priority, scaled to the budget → confirm
4. Confirm comparisons + refresh cadence
5. Emit the Strategy brief
```

Propose with reasoning, offer the alternative, confirm, then move. Don't interrogate — ask
only what changes the design.

---

## 1. Dashboard type

Classify, but lead with reasoning and name the alternative so the user can redirect.

| Type | Signals in requirements | Behavior it buys |
|------|------------------------|------------------|
| **Operational** | "real-time", "alerts", "immediate action", monitoring | Live/near-live updates; clear alert states; glanceable status; exceptions over exploration |
| **Analytical** | "trends", "compare", "investigate", "drill down"; daily/weekly cadence | Interactive filtering; drill-down paths; comparative views; period-over-period |
| **Strategic** | executive/board audience; KPIs, OKRs; monthly/quarterly horizon | High-level KPIs tied to goals; trend over granularity; presentation-ready |

**Proposal shape:**
```
"I'm recommending an **Analytical** dashboard — you review data daily, need drill-down to
investigate, and comparisons/trends are central.

Alternative: if you need threshold alerts for immediate response → Operational; if this is
board review → Strategic.

Does Analytical fit?"
```

Type is not exclusive of archetype — an Operational dashboard can still be glanceable; a
Strategic one almost always is. Classify type first, then tune density via the archetype.

---

## 2. Audience archetype → visualization density budget

Infer *who reads this and in what posture*, then set how much to visualize per region. This
tunes **how much**, never **whether** — charts still pass the right-medium check
(visualization.md); the budget just sets how many earn space and how big they run.

| Archetype | Reader & posture | Density budget | Depth strategy |
|-----------|------------------|----------------|----------------|
| **Glanceable / monitoring** | Exec or operator, at-a-glance, seconds of attention | **Fewer, bigger, lighter** widgets. 1–3 hero metrics; calm whitespace; one focal chart, not a wall | **Heavy drill-down** — granularity lives on dedicated views, reached by click |
| **Analytical / exploratory** | Analyst or power user, sustained attention, here to dig | **Denser charts justified** — multiple coordinated views, comparisons, small multiples, finer-grained series | **In-place depth** — filters, brushing, expandable detail on the same surface |

**Read the posture from requirements:** time-on-screen, "quick check" vs. "investigate",
device (wall display / mobile → glanceable; multi-monitor desktop → analytical), and the
decision cadence. When ambiguous, ask one question — it materially changes the layout.

**What the budget changes — and what it doesn't:**
- Changes: widget *count* per region, hero-metric count, chart *size*, how much detail is
  inline vs. behind a drill-down.
- Does **not** change: whether a chart that does real work survives. A glanceable budget
  doesn't delete the trend chart — it makes it the single focal element and moves the
  breakdown table to a drill-down. Stripping rich widgets "for simplicity" is the
  anti-pattern, not the goal.

```
"Read of your audience: **glanceable / monitoring** — execs checking status in seconds on a
shared display. So I'd budget for 2 hero metrics up top, one focal trend chart, and push the
per-segment breakdown to a drill-down rather than crowding the home view.

If your readers are analysts who'll sit and dig, I'd flip to a denser layout with the
breakdowns inline. Which sounds closer?"
```

---

## 3. Metric prioritization — scaled to the budget

Tier every metric, then **let the budget set how many reach the top tier.** Same data,
different real-estate split per archetype.

| Tier | Role | Placement |
|------|------|-----------|
| **Critical** | Answers the primary decision | Most prominent (top-left / hero) |
| **Important** | Leading indicators, process health | Clearly visible |
| **Supporting** | Context & diagnostics | Lower / available, not dominant |

**Budget ties to tier count:**
- **Glanceable** → **1–2 hero metrics**, ruthlessly few. Everything else demotes to
  Important/Supporting or to a drill-down. A glanceable home with 8 KPIs has no hero.
- **Analytical** → **more metrics can share the top band**; supporting metrics can stay
  inline because the analyst wants them within reach.

**Proposal shape (glanceable example):**
```
"Glanceable budget, so I'm keeping the top tier tight:

CRITICAL (hero): the primary decision metric — the one number this dashboard exists for.
IMPORTANT: 1–2 leading indicators.
SUPPORTING: context metrics → reachable via drill-down, not on the home view.

Does the hero metric match what you'd check first?"
```

**The "so what?" test** — each metric earns space only if both answers are real:
```
"If this number is bad, what do you do? If it's good, what does it mean?"
```
If neither answer drives action, it's not a metric — it's decoration. Demote or drop.

---

## 4. Comparisons & cadence

A metric without a comparison is a number without meaning. Confirm the baseline per metric;
keep comparison *types* aligned with the insight taxonomy in visualization.md (trend,
comparison, anomaly, target) rather than redefining them here.

```
| Metric            | Compare against        | Why                        |
|-------------------|------------------------|----------------------------|
| Primary metric    | vs. target + vs. prior | Goal progress and trend    |
| Leading indicator | vs. target             | Goal-focused               |
| Process-health    | vs. prior period       | Trend-focused              |
```

Confirm refresh cadence against the type: Operational → live/near-live; Analytical →
daily/weekly; Strategic → monthly/quarterly.

---

## Domain-agnostic framing

State strategy in **transferable terms**, not one domain's nouns, so the reasoning ports:

- "the primary decision metric" — not "Revenue"
- "ranked entities" — leaderboards, top-N tables (reps, products, regions…)
- "a conversion process" — funnel stages, onboarding steps, checkout flow
- "a time series" — any metric over time
- "leading indicator" — the upstream signal that moves before the outcome

Inherit the *project's* vocabulary when you write the actual brief — but reason in these
archetypal shapes so the choice is justified, not domain-lucky.

---

## Handling disagreement

**Wrong type** → re-test against signals: "Do you need live data and alert states, or is the
primary job investigation?" Adjust to the answer.

**Wrong priority** → reorder immediately and restate the consequence: "Got it — that metric
becomes the hero and dominates the visual hierarchy. Right?"

**Budget feels off** → the user is the ground truth on posture. If they say "my execs do
sit and dig," shift glanceable → analytical and re-tier.

---

## Output: Strategy brief

```markdown
## Dashboard Strategy Brief

**Type**: [Operational / Analytical / Strategic] — confirmed
**Audience archetype**: [Glanceable-monitoring / Analytical-exploratory] — confirmed
**Density budget**: [Fewer-bigger-lighter, heavy drill-down  /  Denser, in-place depth]
**Primary decision this supports**: [decision]
**Refresh cadence**: [live / daily / weekly / monthly] — confirmed

### Metric priority (scaled to budget)
| Tier       | Metric (transferable term)      | Comparison        | Placement       |
|------------|---------------------------------|-------------------|-----------------|
| Critical   | [primary decision metric]       | [vs. what]        | Hero / top-left |
| Important  | [leading indicator]             | [vs. what]        | Visible         |
| Supporting | [context / diagnostic]          | [vs. what]        | Lower / drill-down |

### Key decisions
- Type: [type] because [signals]
- Archetype + budget: [archetype] because [posture read] → [what it tunes]
- Hero metric: [metric] because [user reasoning]
- Depth strategy: [drill-down vs. in-place]

### Confirmations
- [ ] Type  - [ ] Archetype/budget  - [ ] Priority  - [ ] Comparisons  - [ ] Ready for layout
```

---

## Anti-patterns

- Classifying type or budget **without reasoning** the user can redirect.
- Treating the density budget as a **cull** — stripping rich widgets "for simplicity"
  instead of resizing/relocating them. Glanceable means *fewer and bigger*, not *gutted*.
- A glanceable home with **no clear hero** (8 equal KPIs = no priority).
- Forcing an analyst's exploratory needs into a sparse exec layout (or vice-versa) because
  the archetype was never inferred.
- Metrics with **no comparison** and no "so what?" answer earning prime real estate.
- Domain-locked reasoning that only works for one dataset's nouns.
```