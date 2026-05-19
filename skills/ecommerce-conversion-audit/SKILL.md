---
name: ecommerce-conversion-audit
description: Audit ecommerce storefronts for conversion touchpoints, buying-confidence nudges, mobile-first PDP/homepage UX, offer clarity, trust signals, and data readiness. Use when asked to improve an ecommerce site, product detail page, home page, merchandising flow, checkout-adjacent prompts, purchase-decision copy, or to produce a prioritized recommendations/data-availability matrix for any online store.
---

# Ecommerce Conversion Audit

## Overview

Use this skill to inspect ecommerce stores like a pragmatic go-to-market, sales, product, and UX operator. Optimize for fast purchase decisions, low cognitive load, truthful nudges, and a clear split between what can be implemented now and what needs data or operational confirmation.

Prioritize mobile first, then desktop. Prioritize PDPs first, then home, then listing/cart-adjacent touchpoints unless the user asks otherwise.

## Workflow

1. Establish the store surface:
   - Identify platform, live URL, local app, repo, theme, CMS, analytics sources, and commerce backend if available.
   - Inspect the real storefront when possible. Capture or reference mobile evidence before desktop evidence.
   - If there is a repo, read the current templates/components/settings before recommending implementation.

2. Audit the purchase questions:
   - PDP: price, discount/savings, active offer, delivery timeline, delivery coverage/location fit, payment options, returns/exchange, product images, product dimensions/materials, variants/options, related alternatives, reviews/social proof, support path, stock/availability, and add-to-cart behavior.
   - Home: what the store sells, current offer, fast path to all products, fast path to key categories, credible popular picks, USP, trust reasons, brand clarity, and campaign entry points.
   - Listing/product cards: price, discount, image clarity, variant cues, one clear action, and scan speed.
   - Cart-adjacent nudges: free shipping, free gift, discount reminders, delivery/support clarity, and checkout risk reducers.

3. Classify each opportunity:
   - `Implement now`: existing data/config supports the claim or UI change.
   - `Needs confirmation`: likely available but must be confirmed in admin, analytics, logistics, marketing, or ops.
   - `Blocked/missing`: requires a new integration, policy decision, data source, or operational setup.

4. Prioritize by impact and effort:
   - Impact: purchase confidence, first-viewport clarity, checkout movement, support deflection, merchandising discovery, or trust.
   - Effort: `XS` copy/config, `S` theme/component change, `M` multi-component or data mapping, `L` integration/ops dependency.
   - Mobile PDP improvements usually outrank desktop polish unless the evidence says otherwise.

5. Recommend nudges without adding clutter:
   - Prefer compact decision stacks, short proof rows, inline delivery/offer cues, clear CTAs, and progressive disclosure.
   - Do not add banners, badges, or urgency copy unless they answer a real buying question.
   - Keep prompts subtle, specific, and close to the decision they support.

## Data Rules

- Do not claim "best seller", "most purchased", "trending", "limited time", rating counts, review averages, pincode delivery precision, or free gifts unless the backing source is confirmed.
- Use "Popular picks", "Featured", or "Curated" when merchandising is manual and order analytics is unavailable.
- Show exact discount mechanics only when confirmed: automatic discount, manual code, popup code, tiered discount, compare-at saving, or cart threshold.
- Treat delivery as layered precision:
  - Store-wide policy is acceptable for broad copy.
  - Region/pincode-specific promises require logistics data or an API.
  - Uncertain delivery should route to support instead of pretending precision.
- Treat reviews, UGC, Instagram, inventory, cross-sells, and sibling products as gated modules when data coverage is unknown.

## Recommendation Patterns

Use these patterns when supported by evidence:

- PDP decision stack: price, savings, offer, delivery promise, delivery coverage, COD/free shipping/returns trust, and support.
- Offer clarity block: one primary active offer near the buy controls, with exact redemption behavior.
- Delivery nudge: concise timeline and coverage near add-to-cart, with support fallback for location-specific questions.
- Sticky action guard: sticky add-to-cart appears only after context, never covers content, and coordinates with chat/WhatsApp widgets.
- Product media confidence: clear image gallery, count/progress cues, lifestyle/detail balance, and mobile-friendly swipe behavior.
- Options rail: variants, colors, sizes, bundles, or sibling products shown close to the decision area when reliable mappings exist.
- Home discovery rail: all products, best sellers or curated picks, top categories, bundles/combos, and campaign collections.
- USP strip: three to five concrete reasons to buy from this store, not generic brand slogans.
- Product-card simplification: image, title, price, savings, one clear action, and minimal competing badges.
- Social proof gate: show reviews/UGC only with real content; otherwise use craft, policy, or service proof.
- Cart threshold nudge: show only if the threshold is actually enforced in checkout/cart logic.

## Output Format

Adapt the format to the user request, but default to this structure:

```markdown
## Executive Summary
[Mobile-first diagnosis in 3-5 bullets.]

## Highest-Impact Changes
| Priority | Surface | Suggestion | Why it matters | Effort | Data confidence |
|---|---|---|---|---|---|

## Data Readiness Matrix
| Suggestion | Required data/config | Current confidence | Can implement now? | Notes/blocker |
|---|---|---|---|---|

## Mobile Audit
### PDP
[Evidence-backed observations and recommendations.]

### Home
[Evidence-backed observations and recommendations.]

### Listing/Cart Adjacent
[Include only if relevant or inspected.]

## Desktop Audit
[Only after mobile. Focus on hierarchy, spacing, scanning, and purchase confidence.]

## Implementation Batches
1. Batch 1: confirmed-data, low-risk wins.
2. Batch 2: needs configuration/admin confirmation.
3. Batch 3: new integrations or data sources.

## Validation Plan
[Browser checks, analytics checks, admin checks, and copy/data QA.]
```

## Evidence Standard

- Cite URLs, screenshots, repo files, admin settings, API responses, analytics exports, or browser observations when available.
- Say clearly when a recommendation is based on heuristic best practice rather than verified store data.
- If the user asks for implementation, convert recommendations into scoped changes and preserve the data gates in the code or configuration.
