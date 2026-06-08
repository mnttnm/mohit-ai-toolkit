# Requirements Reference

> **When to use this file**: At the **Clarify** gate — starting a dashboard, scanning the
> project, and resolving the few ambiguities that genuinely change the design. Pairs with
> SKILL.md's "First: New or Revamp?" decision and the three-gate flow.

Requirements is a *navigator* move, not an intake form. The goal isn't to fill every
field — it's to learn what the project already answers, audit what exists, and ask only
the handful of things that would change what you build.

---

## Step 1 — Scan the project (do this before asking anything)

The repo answers most "what conventions?" questions for free. Run a light
**project-context scan** first; it powers both *inherit the vocabulary* and *derive the
theme* (see SKILL.md Principle 7).

| Look at | For | Feeds |
|---|---|---|
| `package.json` | Chart library (recharts / tremor / chart.js / visx / nivo / echarts), UI primitives (shadcn / MUI / Chakra / Mantine), framework (Next / Vite / Remix) | Chart-lib + component inheritance |
| `tailwind.config.*` / theme file / CSS `:root` vars | Design tokens — colors, radius, spacing, font family | Theme sourcing (`design-system.md`) |
| One representative component | Conventions in the wild — TS vs JS, Tailwind vs CSS modules, icon set, file/folder layout, how cards/buttons are composed | Framework + primitive inheritance |
| Existing dashboard/chart code, if any | Patterns already in use, the baseline to beat | Strategy + visualization |

**Report what the scan found**, then state your inherit/own stance and ask only where the
answer would change output:

> "Scan found Next.js + shadcn/ui + Recharts, and a Tailwind theme with a violet primary
> and `rounded-lg` cards. I'll build native to that. Want me to match those conventions
> closely, or push a fresher direction?"

If there's no codebase (pure greenfield / mockup), say so and fall back to deriving a
theme from a described vibe or the light/dark default (`design-system.md`).

---

## Step 2 — New vs Revamp

**Revamp → audit the existing dashboard first**, before gathering anything new. Go
widget by widget and capture, for each:

- **What it shows** — the metric/visual.
- **What decision it supports** — or whether it supports none.
- **What's weak** — wrong chart for the data, no insight, dead-end, redundant, buried, or
  visually flat.

That audit *is* your requirements for a revamp: it surfaces what to keep, cut, merge, and
elevate. The old layout is the **baseline to beat, not a template to copy.**

**New → go straight to Step 3.** Start from the audience and the questions the dashboard
must answer.

---

## Step 3 — Clarify only what's ambiguous

Resolve *genuine* ambiguity, then move. Don't interrogate, don't run a script, and never
ask a question whose answer wouldn't change what you build. The project scan and the data
already answer most of it.

**Must resolve (preference genuinely changes the output):**
- **Decision** — the one main decision this dashboard should help make.
- **Audience** — who uses it, how often, in what context (desk / mobile / wall display).
- **Must-show metrics** — the 1–2 numbers that have to be prominent.
- **Theme source** — derive from the project, describe a vibe, or default light+dark — and
  the inherit-vs-own lean (match conventions vs push fresher).

**Offer options, recommend one (don't open-endedly ask):**
- Dashboard type (operational / analytical / strategic) — usually inferable; confirm in
  Strategy.
- Comparison context per metric (target / prior period / benchmark).
- Refresh cadence (real-time / periodic / static) when it's unclear.

**Decide yourself (best practice, no need to ask):** accessibility (WCAG 2.1 AA),
data-fit and contrast checks, grid/spacing, tabular figures, earned-element gating, chart
type where the data points to one answer.

**One opening pass is usually enough.** A quick concept may need a single question; a
production revamp warrants a fuller round. Scale the ceremony to the task.

> Sample opening (adapt, don't recite): *"Before I design — what's the main decision this
> should drive, who's the audience, and are there one or two metrics that must lead? On
> the look: derive a theme from your repo, match a product you like, or want a clean
> light+dark default?"*

**When the user defers** ("no preference", "just make it good"), don't loop on it — state
the default you'll apply and show a draft to react to:

> "I'll derive the theme from your project's tokens (else a clean light+dark default),
> lead with [metric], and keep it balanced — not sparse, not packed. I'll show a draft;
> easier to react than to spec."

---

## Watch for

- **"Show everything"** → push for the 1–2 that lead; the rest earn their place or move to
  a drill-down.
- **No clear audience** → the dashboard will serve no one well; pin this down.
- **Conflicting signals** (e.g. "minimal" + "show all 30 metrics") → surface the tension
  and let the user choose, rather than silently picking.
- **Project convention vs requested style clash** → flag it, don't silently abide or
  override (SKILL.md Principle 7).

---

## Output — Requirements brief

Keep it tight; fill only what's known. Unknowns that don't block design stay blank.

```markdown
# Dashboard Requirements: [Name]

## Context
- Mode: [New / Revamp]   ·   (Revamp) Audit summary: [keep / cut / elevate per widget]
- Project scan: [framework · chart lib · UI primitives · theme tokens found]
- Inherit/own lean: [match conventions / push fresher]

## Purpose
- Type: [Operational / Analytical / Strategic]  (confirm in Strategy)
- Primary decision: [what it drives]

## Audience
| Who | Frequency | Context (desk/mobile/display) | Technical level |
|-----|-----------|-------------------------------|-----------------|

## Metrics
| Metric | Lead? | Source | Refresh | Compare against |
|--------|-------|--------|---------|-----------------|

## Theme & feel
- Source: [derive from project / vibe: ___ / default light+dark]
- Density lean: [focused / balanced / comprehensive]
- Brand / anti-patterns: [colors, fonts, things to avoid — or "flexible"]

## Constraints
- Technical / accessibility / tools-to-match: [or "none noted"]
```

Hand off to **strategy.md** once the decision, audience, lead metrics, and theme source
are settled. Everything else can firm up as you design.
