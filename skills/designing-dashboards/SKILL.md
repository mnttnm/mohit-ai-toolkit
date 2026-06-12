---
name: designing-dashboards
description: Design modern, actionable dashboards through a collaborative, taste-aware workflow. Use for any dashboard task—building new dashboards, revamping existing ones, choosing layouts, selecting charts, designing widgets, deriving a theme, or validating a design. Acts as a navigator: pitches options, adapts to the user's taste and codebase, keeps rich widgets that earn their place, and verifies the result by measurement—never assumes preferences.
---

# Dashboard Design Skill

A **navigator, not a prescriber.** This skill guides you toward a well-made dashboard
by pitching suggestions and adapting to the user's taste, their codebase, and their
audience. It keeps the rich, interpretive widgets that separate a real dashboard from a
generic one — and it earns every element rather than padding or stripping by reflex.

**Two operating beliefs:**
- **Rich by intent, not by reflex.** Charts, insights, and composed widgets are the
  value. Keep them whenever they do real work; cut only the *gratuitous*.
- **Verify, don't attest.** A dashboard isn't done because a checklist is ticked — it's
  done when the rendered output has been measured.

## How this skill works

Progressive disclosure: the workflow and principles live here; depth lives in reference
files, loaded when a phase needs them.

| Phase | Reference | Use when |
|-------|-----------|----------|
| Requirements | [requirements.md](requirements.md) | Starting out; scanning the project; gathering only what's ambiguous |
| Strategy | [strategy.md](strategy.md) | Classifying the dashboard, audience archetype → visualization density budget |
| Layout | [information-architecture.md](information-architecture.md) | Layout patterns, launchpad/drill-down, dashboard-level interaction (filters, date range, URL state) |
| Visualization | [visualization.md](visualization.md) | Right-medium check, chart selection, selection≠execution, chart→library mapping |
| Design system | [design-system.md](design-system.md) | Tokens (single source), theme sourcing (light/dark · derive · vibe), numeric craft, dark mode |
| Widgets | [components.md](components.md) | Widget anatomy as a menu; implementation conventions (Recharts + Tremor / project lib) |
| States | [edge-states.md](edge-states.md) | Empty / loading / error — always required |
| Validation | [validation.md](validation.md) | The measured loop: render → screenshot → contrast → breakpoints → scored rubric |

---

## First: New or Revamp?

**Revamp (improving an existing dashboard) → audit first, then diff.** Don't design from
blank. Audit the current dashboard widget-by-widget: *what does each one show, what
decision does it support, what's weak or missing?* Diff that against the target, then
improve. The existing layout is the **baseline to beat, not a template to copy.**

**New (greenfield) → go to Requirements.** Start from the audience and the questions the
dashboard must answer.

Either way, run the **project-context scan** early (see Principle 7).

---

## The three gates

Lightweight collaboration — ask only what genuinely changes the design, then move.

| Gate | When | What |
|------|------|------|
| **Clarify** | Before strategy | Resolve only *genuine* ambiguity (audience, theme source, must-show metrics). Don't interrogate. |
| **Propose** | Before building | Pitch strategy + layout + theme sourcing as options; confirm direction. |
| **Validate** | After building | Run the **measured loop** (validation.md), then the advisory subtraction pass and scored rubric. |

Scale the ceremony to the task: a quick concept needs one Clarify question; a
production revamp warrants all three gates in full.

---

## Core principles

**1. Charts + insights.** Every visualization that stays carries a headline insight that
adds what the chart doesn't already show — a cause, comparison, anomaly, implication, or
next action. *Bar: would a sharp analyst bother saying this out loud?* If the best you
can write restates the axis ("Thursday was highest"), drop the band and let the chart
speak. No boilerplate ("steady growth, +2%").

**2. Right medium, then right chart — a guard, not a cull.** Rich widgets are the
default; keep any that do real work. Use the medium check only to catch *gratuitous*
visuals (decoration with no decision behind it): `number/delta → sentence → table →
chart → headline + link`. Then match the chart type to the data's question — and verify
it against the *actual* values (the **data-fit check**: values that render visually
identical, e.g. 91/91/95/102, become numbers + deltas, not bars).

**3. Creative, purposeful layouts.** Escape card-grid monotony (hero, bento, magazine,
hub-and-spoke). The dashboard is a **launchpad** — headline + entry points — not an
everything-page; push depth to dedicated views.

**4. Actionable.** Every widget answers "what can I do next?" through *earned* CTAs and
real drill-down destinations — never a generic "View details".

**5. Earn every element.** Widget anatomy is a **menu, not a mandate**: title, insight,
visual, legend, context, and CTA are each included only when they pull their weight.
Loading / empty / error states are the exception — always required.

**6. Selection ≠ execution.** Picking the right chart isn't enough; render it *well*.
Flag known pitfalls (recharts' default `FunnelChart` is a pointy triangle — use a clean
horizontal stepped funnel), use `tabular-nums` for figures, avoid clipped axes, and
ground the build in *current* library conventions (pull live docs) rather than memory.

**7. Inherit the project's vocabulary; own the quality decisions.** Run a light
**project-context scan** (`package.json`, Tailwind/token config, one sample component).
*Inherit* theme, chart library, component primitives, and framework conventions so the
dashboard feels native. *Own* layout, chart selection, the insight layer, and edge
states — that's the improvement. Follow the **what** (their choices), upgrade the
**how** (current best practice). **Ask** which way to lean, and **flag** conflicts
rather than silently abiding or overriding.

**8. Verify by measurement, not checkbox.** Validation renders and *measures*: screenshot
the build, check data-differentiation on the real values, measure contrast on the
*actual* palette, test breakpoints. Self-review is the fallback only when no
browser/harness is available.

---

## Project Context: inherit / own / flag

One scan feeds every "inherit" decision — and the same scan powers "derive theme."

| Concern | Stance | Note |
|---|---|---|
| Theme / design tokens | **Inherit** | Derive from project; else the light/dark default |
| Chart library | **Inherit** | Match existing; don't add a 2nd. Greenfield default: **Recharts + Tremor** for complex/composed widgets |
| Component primitives | **Inherit** | Build widgets from shadcn / MUI / etc. when present |
| Framework conventions | **Inherit** | File structure, TS, Tailwind-vs-CSS, icons |
| Information architecture / layout | **Own** | The old layout is the baseline to beat |
| Chart selection | **Own** | Apply the medium + data-fit checks |
| Insight + actionability layer | **Own** | Usually absent — the main value-add |
| Edge states, motion, hierarchy, density | **Own** | Elevate beyond the baseline |

> **Ask the user:** *"Match your project's existing conventions, or want me to push a
> fresher direction?"* — the answer materially changes output quality.

---

## Decision classification

**Must ask (preference genuinely changes the output):** theme source (derive from
project / describe a vibe / default light+dark), inherit-vs-own lean, audience archetype,
the 1–2 must-show metrics.

**Should ask (offer options, recommend one):** dashboard type, layout pattern, chart
alternatives where the data fits more than one.

**Can decide (best practice applies):** accessibility (WCAG 2.1 AA), data-fit check,
contrast, grid alignment, tabular figures, earned-element gating.

Don't ask about things the project or data already answers — and never ask a question
whose answer wouldn't change what you build.

---

## Anti-patterns to avoid

**Layout** — defaulting to "4 KPIs + 2 charts + table"; every widget the same size;
cramming depth that belongs on a drill-down page.

**Visualization** — a chart with only a title (no earned insight); a chart whose values
render visually identical (use numbers); ≥3 widgets all collapsing to horizontal bars
(differentiate one); the pointy default funnel.

**Insight** — boilerplate that restates the axis; an insight band on every widget out of
habit; a **loose colored insight sentence** styled like the captions around it (contain it in
a banner); **surfacing an insight the data already makes obvious** instead of gating it behind
a "Show insights" reveal. (See design-system.md → Surfacing insights.)

**Color & attention** — everything colored for emphasis, so nothing reads as urgent; a warm
accent (amber/orange) used as the primary bar fill so the whole page runs "hot"; alert-red on
more than the 1–2 truly urgent items; an advisory callout colored like an alarm. Keep a calm
neutral baseline; reserve red for genuine alerts. (See design-system.md → Attention hierarchy.)

**Actionability** — dead-end displays; "View details" as the only action.

**Process** — interrogating the user through long question scripts; applying the generic
Tailwind-blue/Inter default as if it were a choice; stripping rich widgets by reflex in
the name of "simplicity"; self-attesting validation without rendering.

---

## Output templates

Requirements brief → [requirements.md](requirements.md) · Strategy brief →
[strategy.md](strategy.md) · Widget spec → [components.md](components.md) · Validation
report → [validation.md](validation.md).
