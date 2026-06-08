# Validation Reference

> **When to use this file**: After the dashboard is built. This is the **Validate** gate.
> The headline belief: **verify by measurement, not checkbox.** A dashboard isn't done
> because boxes are ticked — it's done when the *rendered* output has been measured. Run
> the measured loop, then the advisory subtraction pass, then score the rubric.

Three movements, in order:

1. **The measured loop** — render the real build, screenshot it, measure the real values and the real palette.
2. **Advisory subtraction pass** — zoom out; question each widget against the decision it serves. Suggest, never strip.
3. **Scored rubric** — grade Visual / Analytical / UX out of 10 each, backed by the measurements above.

---

## 1. The measured loop

Self-attestation is the failure mode this skill exists to kill. "Contrast: ☑" means
nothing if no pixel was measured. Drive the **actual rendered build** through the loop
below using the available browser/harness (e.g. Claude-in-Chrome, Playwright, or the
project's own dev server + screenshot tooling). Serve the app — don't reason about it.

```
render → screenshot → differentiate data → measure contrast → test breakpoints → log findings
```

**Render.** Start the dashboard with real (or realistic) mock data — the same values that
ship, not flattering placeholders. Near-identical numbers are where charts lie; they must
be present.

**Screenshot.** Capture the full dashboard at the intended default viewport. Look at it as
a first-time user would — overall balance, breathing room, hierarchy — *before* inspecting
widgets.

**Differentiate data (the data-fit check, now measured).** For every chart, read the bars
off the *rendered* image, not off intent. Do near-identical values (e.g. 91 / 91 / 95 /
102) produce bars a human can tell apart? If the differences are invisible, the chart is
lying — demote it to numbers + delta chips. Confirm the *picture* matches the *story* the
insight claims (an "up 40%" headline over four bars of equal height is a caught defect).

**Measure contrast — on the *actual* palette.** Pull the real foreground/background pairs
that rendered (chart text on chart surface, axis labels, delta chips, CTA on its fill) and
measure each. Thresholds live in **design-system.md** (§ contrast floors); this file does
the *measuring* against the shipped colors. Do not assert "contrast passes" — report the
measured ratio per pair, flag any below floor.

**Test breakpoints.** Resize and re-screenshot at **desktop / tablet / mobile**. Check:
nothing clips or overflows, charts stay legible (not squished into illegibility), touch
targets stay ≥44px on mobile, and the launchpad reflows rather than horizontal-scrolls.

**Log findings.** Each measurement is a line of evidence — it feeds the rubric in §3. A
measurement that fails is a defect to fix, then re-loop; it is not a box to leave unticked.

### Graceful degradation — self-review fallback

**Only when no browser/harness is available**, degrade to a *structured* self-review — and
say so explicitly ("no renderer available; reasoned review, not measured"). This is a
weaker signal, not an equivalent one. Reason carefully through:

- Read the data arrays and ask, per chart, whether the values are visually separable at
  the chart's pixel size — flag any that aren't.
- Compute contrast from the token hex values in **design-system.md** by hand (math, not
  vibes) for each foreground/background pair.
- Walk each breakpoint's grid mentally for clip/overflow risks.

Mark fallback findings as *unverified* in the rubric. Push to actually render as soon as a
harness exists.

---

## 2. Advisory subtraction pass (zoom out — suggest, never strip)

Rich widgets are the **default value**, not the bloat. This pass is **advisory**: it
*suggests* demotions with reasons and lets the user decide. It never auto-removes anything,
and its default answer is **keep**.

Step back to the whole artifact and ask of each chart / widget / insight:

> **"What decision does this support?"**

| Finding | Suggest | Never |
|---|---|---|
| Widget serves a real decision | **Keep** (default) | — |
| Gratuitous visual — decoration, no decision behind it | *Suggest* demote to a simpler medium, with the reason | Auto-delete |
| Insight restates the axis ("Thursday was highest") | *Suggest* dropping the band, let the chart speak | Strip the chart |
| Two widgets answer the same question | *Suggest* merging or cutting one | Silently remove |

Phrase every output as a proposal the user can decline:

```
ADVISORY — not applied:
• "Revenue gauge" duplicates the KPI card above it (both answer "are we on target?").
  Suggest demoting the gauge to a delta chip. Keep if you want the visual emphasis.
```

**Variety check (flag, don't fix).** If **≥3 widgets all collapse to horizontal bars**,
flag it — monotony reads as low effort. Suggest differentiating *one* (a different
encoding, or numbers + deltas where the data is near-identical). This is a flag for the
user, not an auto-edit.

> The bias is toward richness. Cutting a widget that does real work in the name of
> "simplicity" is the anti-pattern, not the cure.

---

## 3. Concrete accessibility must-dos (verified against the chosen palette)

Not assertions — checks. Run each against the **actual rendered palette**, not the ideal.

- **Chart text alternative / data-table fallback.** Every chart carries a text equivalent:
  an `aria-label` summarizing the takeaway, *and* an accessible data table (visually
  hidden or behind a toggle) so the underlying numbers are reachable without sight. A chart
  with no text path is a fail.
- **`prefers-reduced-motion`.** Any transition, count-up, or chart-draw animation is gated
  behind `@media (prefers-reduced-motion: reduce)` — motion off, content still complete.
  Verify by toggling the media feature and confirming nothing depends on the animation.
- **Colorblind-safe — *checked*, not claimed.** Run the **shipped categorical palette**
  through a deuteranopia/protanopia simulation (or compute pairwise color distance) and
  confirm adjacent series stay distinguishable. Where hue alone separates two series,
  require a redundant channel (pattern, label, direct annotation, dashed vs solid). Report
  which pairs were simulated and the result — do not write "colorblind-safe ✓" without the
  simulation behind it.

Contrast itself is measured in §1 against the design-system.md floors; this section covers
the non-contrast a11y surface. Keyboard nav, visible focus states, and 200%-zoom reflow
remain required and are exercised during the §1 breakpoint pass.

### WCAG 2.1 AA audit table

Run against the rendered build; record the *measured/observed* result, not a tick.

| Criterion | Requirement | How verified |
|-----------|-------------|--------------|
| Color contrast | ≥4.5:1 text · ≥3:1 graphics/UI | Measured per pair in §1 |
| Color independence | Shape / text / pattern redundancy, not hue alone | Colorblind simulation above |
| Keyboard navigation | All interactive elements reachable & operable | Tab through the rendered build |
| Focus indicators | Visible focus state on every control | Observe during keyboard pass |
| Text scaling | Usable at 200% zoom, no clipping | Re-screenshot at 200% |
| Reduced motion | Honors `prefers-reduced-motion` | Toggle media feature |

---

## 4. Project-conflict flagging

When a project convention collides with a best practice, **surface the conflict to the
user** — don't silently abide *and* don't silently override. State the tension, your
recommendation, and let them choose.

```
CONFLICT — your call:
• Project tokens use a 4.1:1 brand blue for body text; WCAG AA wants ≥4.5:1.
  Options: (a) keep brand blue, accept the gap; (b) darken to the nearest passing
  shade (#…); (c) use brand blue for large text only.
  Recommend (b). How do you want to proceed?
```

Same pattern for: an inherited chart library whose default funnel is the pointy triangle
(recommend the clean stepped funnel), a house style that bans the data-table fallback, or a
density convention that fights legibility at mobile. Inherit the *what*, flag where it
fights the *how*.

---

## 5. Scored visual rubric

The final check is a **grade**, not a checklist — the way a reviewer would score the
*rendered* dashboard. Three axes, each **/10, with evidence** drawn from the measurements
above. No score without a cited observation.

| Axis | Scores well when | Evidence to cite |
|---|---|---|
| **Visual** /10 | Clear hierarchy, breathing room, intentional layout, contrast passes, mobile holds | §1 screenshots, contrast measurements, breakpoint shots |
| **Analytical** /10 | Charts differentiate real data, right medium per question, insights add a cause/comparison/anomaly/implication/action (taxonomy in **visualization.md**), no axis-restating boilerplate | §1 data-fit findings, §2 subtraction notes |
| **UX** /10 | Actionable (earned CTAs, real drill-downs), edge states present, a11y verified, flows complete end-to-end | §3 a11y results, edge-states audit, keyboard pass |

```markdown
## Rubric
- Visual:     8/10 — clean bento hierarchy; contrast all ≥4.5:1 (measured);
                     mobile reflows cleanly. −2: tablet KPI row crowds at 768px.
- Analytical: 6/10 — funnel + trend read well. −4: 3 near-identical bar widgets
                     (91/91/95) — flagged for demotion to numbers + deltas (§2).
- UX:         7/10 — drill-downs real, edge states present. −3: 2 charts missing
                     data-table fallback (§3); reduced-motion not yet gated.

Overall: Needs Review. Blocking before ship: a11y fallbacks, bar-variety demotion.
```

Scoring rules:
- **Cite evidence or don't score.** "Visual 8/10" alone is self-attestation — the thing
  this file rejects. Tie each number to a measurement or screenshot.
- **Fallback findings are flagged unverified** (from §1 degradation) and cap confidence.
- A failing axis names the **blocking defect** to fix, then re-loop §1 — not a box to skip.

---

## Recovery protocols

**Missed preference.** If a preference (theme, density, brand color, must-show metric) was
never confirmed, don't paper over it — surface it before delivery:

```
⚠️ I didn't confirm your preference on [X]. I used [default] for [reason].
   Want [Option A] or [Option B] instead?
```

**Skipped gate.** If Clarify or Propose was skipped, present the decisions made for
sign-off rather than assuming agreement:

```
⚠️ I moved ahead on [aspect] without confirming. Here's what I chose and why —
   does it match what you had in mind, or should I adjust?
```

**Measured-loop failure.** A failing measurement (invisible bars, contrast below floor,
mobile overflow) is a **defect to fix and re-loop**, not a caveat to ship with. Re-run §1
on the fix before scoring.

---

## Delivery message

Close by telling the user what was measured, not just what was made:

```
Here's your dashboard. I rendered and measured it:
- Contrast: all pairs ≥4.5:1 (measured on the shipped palette)
- Data-fit: [chart] differentiates its values; [chart] demoted to numbers (near-identical)
- Breakpoints: holds at desktop/tablet/mobile
- Rubric: Visual 8 · Analytical 7 · UX 8

Defaults applied: [list]. Flagged for your call: [conflicts]. What would you like to adjust?
```
