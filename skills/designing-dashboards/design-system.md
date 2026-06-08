# Design System

> **Single source of truth for tokens.** Every color, type, space, radius, shadow, and
> motion value lives here. Other files reference these names; they don't redefine them.
>
> **When to use**: At the Design-system phase — establishing the theme, mapping a derived
> palette, wiring numeric craft, completing dark mode. Load when you need a token value or
> the theme-sourcing question.

A **navigator, not a prescriber.** The default below (Tailwind-blue `#3B82F6` + Inter +
rounded cards) is a *competent floor* — not a recommendation. That exact combination is
the generic "AI dashboard" look. Ship it knowingly, or move off it. Don't funnel every
project into it by reflex.

---

## Theme sourcing — ONE question, not a survey

The old flow asked the user to pick an aesthetic, a density, an animation level, a card
style. Those questions rarely changed the rendered output — they produced the same blue
default with a different label. Replace all of them with a single, load-bearing question:

> **"Should I derive the theme from your existing project, work from a vibe you describe,
> or use the default light/dark system below?"**

The light + dark theme in this file is the **floor** — a well-made, accessible starting
point that works unmodified. The three answers route from there:

### A — Derive from the project (best when a codebase exists)

The project-context scan (SKILL.md Principle 7) already located the config. Read it and
**map their tokens onto the names in this file** — don't invent a parallel set.

| Source | Read | Map to |
|---|---|---|
| `tailwind.config.{js,ts}` | `theme.extend.colors`, `borderRadius`, `boxShadow`, `fontFamily` | brand/surface/text, `--radius-*`, `--shadow-*`, `--font-sans` |
| CSS custom properties | `:root` / `[data-theme]` `--*` vars | match by role (`--background`→`--surface-primary`, etc.) |
| Token file (`tokens.json`, Style Dictionary, Figma export) | the primitive + semantic layers | semantic layer first; fall back to primitives |
| shadcn `globals.css` | `--background --foreground --primary --muted --border --radius` | the surface/text/brand/border block below |

Pull the **accent + the neutral ramp + radius** at minimum; those three carry most of a
brand's feel. Where the project is silent (e.g. no chart palette, no dark variant),
backfill from this file's defaults and **flag** the gap rather than guessing.

### B — From a vibe (best for greenfield / a described feeling)

Translate the adjective into concrete token *deltas* off the default. A vibe is not a
color — it's a coordinated shift across four levers:

| Lever | Quiet / corporate / "trustworthy" | Bold / consumer / "energetic" | Editorial / premium / "refined" |
|---|---|---|---|
| **Accent saturation** | desaturate (slate, muted) | high-chroma, vivid | one confident accent, restrained elsewhere |
| **Radius** | `--radius-sm` (4px), near-square | `--radius-lg`/`xl` (12–16px) | `--radius-md` (8px) or sharp `0` |
| **Shadow** | flat / border-only | lifted (`--shadow-lg`, colored glows) | hairline borders + one soft shadow |
| **Type** | tight scale, medium weights | larger display sizes, bold | high contrast (light body, bold display) |

Confirm the read-back ("So: slate accent, 4px corners, flat cards, restrained motion —
right?") before building. The vibe sets the *direction*; the tokens below stay the
vocabulary.

### C — Default (best when the user has no preference and wants to react to something)

Ship the light/dark system below as-is. Then show the rendered result and let the user
redirect — reacting to something concrete beats imagining it. Say plainly that this is the
common default look so the choice to keep it is deliberate.

---

## Color tokens

### Light mode

```css
:root {
  /* Surfaces */
  --surface-primary: #FFFFFF;
  --surface-secondary: #F9FAFB;
  --surface-tertiary: #F3F4F6;
  --surface-hover: rgba(0, 0, 0, 0.04);

  /* Text */
  --text-primary: #111827;
  --text-secondary: #6B7280;
  --text-tertiary: #9CA3AF;
  --text-disabled: #D1D5DB;

  /* Borders */
  --border-default: #E5E7EB;
  --border-subtle: #F3F4F6;

  /* Semantic — status */
  --color-success: #10B981;
  --color-success-bg: #ECFDF5;
  --color-warning: #F59E0B;
  --color-warning-bg: #FFFBEB;
  --color-error: #EF4444;
  --color-error-bg: #FEF2F2;
  --color-info: #3B82F6;
  --color-info-bg: #EFF6FF;

  /* Brand */
  --brand-primary: #3B82F6;
  --brand-primary-hover: #2563EB;
  --brand-primary-subtle: rgba(59, 130, 246, 0.1);
}
```

### Dark mode

Use a dark *gray* surface, not pure black — `#1F2937`, not `#000`. Semantic colors are
**desaturated and lifted** so they read on dark without vibrating.

```css
[data-theme="dark"] {
  /* Surfaces */
  --surface-primary: #1F2937;
  --surface-secondary: #111827;
  --surface-tertiary: #374151;
  --surface-hover: rgba(255, 255, 255, 0.05);

  /* Text */
  --text-primary: #F9FAFB;
  --text-secondary: #D1D5DB;
  --text-tertiary: #9CA3AF;
  --text-disabled: #6B7280;

  /* Borders */
  --border-default: #374151;
  --border-subtle: #1F2937;

  /* Semantic — desaturated for dark surfaces */
  --color-success: #34D399;
  --color-success-bg: rgba(52, 211, 153, 0.1);
  --color-warning: #FBBF24;
  --color-warning-bg: rgba(251, 191, 36, 0.1);
  --color-error: #F87171;
  --color-error-bg: rgba(248, 113, 113, 0.1);
  --color-info: #60A5FA;
  --color-info-bg: rgba(96, 165, 250, 0.1);
}
```

### Colorblind risk — flag, then verify

The success/error pair (`#10B981` green / `#EF4444` red) is the most common dashboard
color coding **and** the most common accessibility failure — red/green is
indistinguishable for the largest colorblindness group (~8% of men). Never let
color be the *only* signal:

- Pair every status color with an **icon, shape, or sign** (↑/↓, +/−, ✓/✕).
- For up/down deltas, prefer a **diverging blue↔orange or teal↔red** encoding over
  green↔red where the figure stands alone.

Verification (simulate the palette, measure contrast) happens in **validation.md** — this
file only flags the risk and supplies the safer encodings.

---

## Attention hierarchy — most of the page should be calm

Color is a budget, not decoration. If everything is colored for emphasis, nothing reads as
urgent. Three roles, used in roughly this proportion:

- **Neutral (the baseline, most of the page)** — structural data (most bars, sparklines,
  table rows, resting states) in a calm, *clean* neutral — the quiet field everything else
  stands against. **Use a cool slate, not a warm mid-gray:** a warm desaturated mid-tone
  (e.g. `#78716C`) reads as **disabled / muddy**, not "data." Cool neutrals also sit well
  *under* a warm accent (cool data + warm accent is a deliberate, premium pairing).
- **Accent (sparing spotlight)** — the brand color marks *one* thing per view worth the
  eye: a peak bar, the primary CTA, a #1 rank. Never the default fill for every bar.
- **Semantic (status, sparse)** — alert red/rose reserved for the **1–2 genuinely urgent
  items on the whole page.** A negative delta is a small signed chip, not a block of red.

Rules:
- **A warm accent collides with the warning color.** An amber/orange/red-ish accent already
  reads as "alert," so if you choose one, structural data MUST go neutral — otherwise the
  whole page runs "hot." Pick a cool accent, or neutralize everything else; don't paint
  every bar in a warm brand.
- **Color insights by valence, not red-by-default.** An advisory callout ("Thu leads —
  staff the Mon lull") is neutral text with a neutral icon; positive is calm-good; only a
  true alert gets red. Never default an insight to a red down-arrow.
- **Count the alarms.** If more than ~2 elements scream, demote the weakest until a clear
  triage emerges — the user should know where to look *first*.

---

## Surfacing insights — contain, then choose surface vs reveal

An insight is the value-add, but *how* it's presented decides whether the page reads or
clutters. Two rules, learned the hard way.

**1. Contain the insight — never loose colored text.** A one-line insight set beside the
title in a slightly-bigger, slightly-colored font is indistinguishable from the captions,
axis labels, and metadata around it — it reads as just another subtitle, and a page of them
runs together. Put every insight in a **banner/callout**: a bordered, tinted container reads
as *one deliberate object*, not a sentence floating in the layout. Hierarchy comes from
*containment*, not from nudging a font size.

**2. Surface the non-obvious; hide the deducible.** Not every insight deserves to be on
screen at all times.

| The insight is… | Treatment | Where |
|---|---|---|
| **Non-obvious** — the data alone won't yield it quickly (e.g. four near-identical numbers that *look* like a ranking but are actually a tight pack) | **Surfaced** — banner always shown, *above* the data: takeaway → evidence | Top of the card, under the title |
| **Deducible** — the data already shows it (sorted table, one bar already maxed) | **Hidden** behind a "Show insights" toggle that reveals the banner and can close it again | Toggle at the card's **top-right**; banner renders at the **top** on open |

Either way the insight lives at the **top**; the card bottom is then only metadata + the
action CTA (CTA always right). Surfacing everything is the clutter; hiding the obvious keeps
the glance-path clean while the analysis stays one click away.

**Banner tone — alarm vs delight.** A banner is not always an alarm:
- **Alarm** (a genuine problem): rose tint, *colored* title, warning icon. At most ~one per
  page — this is the one alarm from the color budget above.
- **Delight / informational** (useful but not bad news): calm indigo, **neutral-dark title**,
  a sparkle. The default for most surfaced insights.

Give the banner a **soft gradient wash (tint → surface) + a hairline border**, not a flat
filled block — it stays attention-worthy without looking pasted on top of the card.

**Affordance restraint.** The reveal trigger is a quiet static pill — *no* perpetual
shimmer/marquee. A constantly-moving element fights the calm you just built; any reveal
motion is a one-shot, gated behind `prefers-reduced-motion`.

---

## Typography

```css
:root {
  /* Family */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;

  /* Sizes */
  --text-xs: 0.75rem;    /* 12px */
  --text-sm: 0.875rem;   /* 14px */
  --text-base: 1rem;     /* 16px */
  --text-lg: 1.125rem;   /* 18px */
  --text-xl: 1.25rem;    /* 20px */
  --text-2xl: 1.5rem;    /* 24px */
  --text-3xl: 1.875rem;  /* 30px */
  --text-4xl: 2.25rem;   /* 36px */

  /* Weights */
  --font-light: 300;
  --font-regular: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;

  /* Line heights */
  --leading-tight: 1.25;
  --leading-normal: 1.5;
  --leading-relaxed: 1.75;

  /* Letter spacing */
  --tracking-tight: -0.025em;
  --tracking-normal: 0;
  --tracking-wide: 0.025em;
}
```

**Font loading is not optional.** `--font-sans` names Inter, but a named font isn't a
loaded font. If Inter isn't actually delivered (self-hosted `@font-face`, `next/font`, or
a `<link>` to the CDN), the browser silently falls back to `-apple-system` — and the
dashboard renders in San Francisco / Segoe, not Inter. Either **load it for real** (prefer
`next/font` or self-host to avoid layout shift) or **drop Inter from the stack** and design
deliberately for the system font. Don't ship a token that lies about what renders.

**Text hierarchy is the typographic analogue of the attention hierarchy above** — and it
carries through *weight + size + color*, not hue. Give text distinct roles: a quiet **eyebrow
title** (small, secondary), the **figure** that leads each KPI, and **captions / metadata**
that recede (small, tertiary). When everything sits at one size and weight, the eye can't tell
the takeaway from the footnote. Note: the *insight* is not just "a bigger line" in this ladder
— it's **contained** in a banner (see [Surfacing insights](#surfacing-insights--contain-then-choose-surface-vs-reveal)),
because a loose line, however weighted, still bleeds into the captions next to it.

---

## Numeric craft

Dashboards are mostly numbers. Two rules apply to every figure, KPI, axis label, and table
cell — they are *can-decide* best practice, not options:

**1. Tabular figures.** Proportional digits make columns of numbers ragged and KPIs
"jump" as they update. Mandate tabular lining figures everywhere a number appears:

```css
.figure, td.num, .kpi, .axis-label { font-variant-numeric: tabular-nums; }
```

Inter ships tabular-nums; if a derived/brand font lacks the feature, fall back to
`--font-mono` for figures rather than living with the jitter.

**2. Abbreviate large numbers consistently.** Raw `1240000` is unreadable in a KPI. Use a
single threshold table across the whole dashboard so `1.2M` never sits next to `1,240k`:

| Magnitude | Format | Example |
|---|---|---|
| < 1,000 | full | `847` |
| 1,000 – 999,999 | `0.0k` (1 decimal) | `10.3k`, `999.9k` |
| ≥ 1,000,000 | `0.0M` | `1.2M` |
| ≥ 1,000,000,000 | `0.0B` | `3.4B` |

Right-align numeric columns, keep the unit/suffix consistent, and show full precision on
hover/tooltip when the abbreviation hides something a user needs.

---

## Spacing — 4px base

```css
:root {
  --space-0: 0;
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-5: 1.25rem;   /* 20px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */
  --space-10: 2.5rem;   /* 40px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */
}
```

Density is a function of which steps you use (tight = `--space-2/3`, airy = `--space-6/8`),
not a separate token set.

---

## Border radius

```css
:root {
  --radius-none: 0;
  --radius-sm: 0.25rem;   /* 4px */
  --radius-md: 0.5rem;    /* 8px */
  --radius-lg: 0.75rem;   /* 12px */
  --radius-xl: 1rem;      /* 16px */
  --radius-full: 9999px;
}
```

---

## Shadows & elevation

```css
:root {
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.1);

  /* Card */
  --shadow-card:
    0 1px 3px rgba(0, 0, 0, 0.06),
    0 1px 2px rgba(0, 0, 0, 0.04);

  /* Elevated hover */
  --shadow-hover:
    0 4px 12px rgba(0, 0, 0, 0.08),
    0 2px 4px rgba(0, 0, 0, 0.04);
}
```

**Dark mode uses borders, not shadows.** A drop shadow is a dark blur on a dark surface —
nearly invisible. Convey elevation on dark with a **lighter border + a subtle surface
lift** instead:

```css
[data-theme="dark"] {
  /* Elevation = lifted bg + visible border, shadows near-zero */
  --shadow-card: 0 0 0 1px rgba(255, 255, 255, 0.06);
  --shadow-hover: 0 0 0 1px rgba(255, 255, 255, 0.12);
  --elevation-1: #1F2937;   /* base card    — = surface-primary */
  --elevation-2: #283548;   /* raised / hover — one step lighter */
  --elevation-3: #313f54;   /* popover / modal */
}
```

Rule of thumb: in light mode, things *float* (shadow); in dark mode, things *lift*
(brighter surface + border). Don't reuse the light shadow stack on dark.

---

## Motion

```css
:root {
  /* Durations */
  --duration-fast: 100ms;
  --duration-normal: 200ms;
  --duration-slow: 300ms;

  /* Easings */
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);

  /* Spring (JS / Framer Motion) */
  --spring-snappy: { stiffness: 400, damping: 30 };
  --spring-smooth: { stiffness: 300, damping: 30 };
}
```

Default to restraint: hover/transition only, chart-draw on first paint. Always honor
`prefers-reduced-motion` — gate count-ups, staggers, and draw animations behind it.

---

## Data-visualization palettes

Pull chart colors from these ramps, never ad-hoc hex. Match the ramp to the data's shape:
**categorical** for unordered groups, **sequential** for one-directional magnitude,
**divergent** for a meaningful midpoint.

```css
:root {
  /* Categorical — max 6 for distinction; beyond 6, group or facet */
  --chart-1: #3B82F6;  /* Blue */
  --chart-2: #10B981;  /* Green */
  --chart-3: #F59E0B;  /* Amber */
  --chart-4: #EF4444;  /* Red */
  --chart-5: #8B5CF6;  /* Purple */
  --chart-6: #EC4899;  /* Pink */

  /* Sequential — single hue, light→dark */
  --seq-1: #DBEAFE;
  --seq-2: #93C5FD;
  --seq-3: #60A5FA;
  --seq-4: #3B82F6;
  --seq-5: #2563EB;
  --seq-6: #1D4ED8;

  /* Divergent — red ↔ neutral ↔ green */
  --div-neg-3: #DC2626;
  --div-neg-2: #F87171;
  --div-neg-1: #FCA5A5;
  --div-neutral: #D1D5DB;
  --div-pos-1: #86EFAC;
  --div-pos-2: #34D399;
  --div-pos-3: #059669;
}
```

### Dark-mode chart palette (separate — the light ramp isn't valid on dark)

The light categorical colors lose contrast on `#1F2937` and several muddy together. Use a
**brighter, slightly desaturated** set tuned for dark surfaces — and re-check the divergent
midpoint, since `--div-neutral` (`#D1D5DB`) nearly disappears.

```css
[data-theme="dark"] {
  /* Categorical — lifted for dark surfaces */
  --chart-1: #60A5FA;  /* Blue */
  --chart-2: #34D399;  /* Green */
  --chart-3: #FBBF24;  /* Amber */
  --chart-4: #F87171;  /* Red */
  --chart-5: #A78BFA;  /* Purple */
  --chart-6: #F472B6;  /* Pink */

  /* Sequential — shift the ramp brighter so steps stay legible */
  --seq-1: #1E3A8A;
  --seq-2: #1D4ED8;
  --seq-3: #3B82F6;
  --seq-4: #60A5FA;
  --seq-5: #93C5FD;
  --seq-6: #DBEAFE;

  /* Divergent — neutral lifted off the dark bg */
  --div-neg-3: #F87171;
  --div-neg-2: #FCA5A5;
  --div-neg-1: #FECACA;
  --div-neutral: #6B7280;
  --div-pos-1: #86EFAC;
  --div-pos-2: #34D399;
  --div-pos-3: #6EE7B7;
}
```

The same red/green colorblind caveat applies to the categorical and divergent ramps:
`--chart-2`/`--chart-4` and the two poles of the divergent scale must be backed by a
non-color signal. Verify in **validation.md**.

---

## Accessibility — non-negotiable, never an option

| Requirement | Standard |
|---|---|
| Text contrast | ≥ 4.5:1 |
| Large text contrast | ≥ 3:1 |
| Graphics / UI contrast | ≥ 3:1 |
| Color independence | never color-only — pair with icon/shape/text |
| Focus indicators | visible on every interactive element |
| Touch targets | ≥ 44×44px |

These apply to *every* theme — default, derived, or vibe-based. Measure them on the actual
rendered palette in **validation.md**; don't attest from the token table.
