# Edge States Reference

> **Load when**: handling empty, loading, error, or real-time states — first-run, no-data, slow fetches, failures, freshness.

**These states are not on the "earn every element" menu — they are always required.** Every other widget part (insight, legend, CTA) is included only when it pulls its weight; empty / loading / error are the non-negotiable floor. A widget without them isn't a leaner widget — it's an unfinished one.

Color/typography/motion tokens referenced below live in **[design-system.md](design-system.md)** — reference token names, don't re-list hex.

---

## Empty States

| Type | Context | Goal |
|------|---------|------|
| First-time use | New account, no data yet | Guide to first action |
| User-cleared | Inbox zero, tasks complete | Celebrate the achievement |
| No results | Search/filter returns nothing | Help refine or clear |
| Error-caused | Data failed to load | Explain and recover (→ Error States) |

```
┌─────────────────────────────────────────┐
│            [Illustration]               │ ← optional, adds personality
│         No data to display yet          │ ← clear explanation
│    Start by adding your first item      │ ← what to do next
│         [ Add First Item ]              │ ← primary CTA
└─────────────────────────────────────────┘
```

**Do:** explain what belongs here (help users picture the populated state); give one prominent next-action CTA; pre-populate with demo data / templates when possible; celebrate completions ("All caught up!"). Reach for an illustration only when it reduces anxiety, not as decoration.

```
First-time:  "Your dashboard is ready. Connect a data source to see insights. [Connect Source]"
No results:  "No matches for 'xyz'. Try different keywords or [Clear Filters]"
Completion:  "All tasks complete. Nothing to review — great work."
```

## Loading States

Pick the indicator by *expected* duration — under-indicating feels broken, over-indicating feels slow.

| Duration | Pattern |
|----------|---------|
| <200ms | No indicator (feels instant) |
| 200ms–2s | Spinner in context |
| >2s | Skeleton screen |
| Unknown / long | Progress bar + message |

### Skeleton screens
Mirror the layout of the real content so the page doesn't reflow on load:
```
Loading:                    Loaded:
┌─────────────────────┐    ┌─────────────────────┐
│ ████████████        │    │ Monthly Revenue     │
│ ████████████████    │    │      $1.2M          │
│ ████  ████████████  │    │ ↑ 15% vs last month │
└─────────────────────┘    └─────────────────────┘
```

```css
.skeleton {
  background: linear-gradient(90deg,
    var(--surface-secondary) 0%,
    var(--surface-tertiary) 50%,
    var(--surface-secondary) 100%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: var(--radius-sm);
}

@keyframes shimmer {
  0%   { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

**Progressive loading** — show the skeleton, then fill highest-value first: KPI values → charts → tables/detail.

## Error States

Never leave a user stranded. Explain what failed in human terms, give a resolution path (retry or alternative), and **degrade gracefully** — show cached data over nothing.

```
┌─────────────────────────────────────────┐
│            ⚠ Error Icon                 │
│    Unable to load revenue data          │ ← what failed
│    We're having trouble connecting      │ ← why (simplified)
│    to the data source.                  │
│    [ Try Again ]  [ View Cached ]       │ ← resolution options
│    Last updated: 2 hours ago            │ ← context
└─────────────────────────────────────────┘
```

| Error Type | Message Approach | Actions |
|------------|------------------|---------|
| Network | "Connection issue" | Retry, offline mode |
| Auth | "Session expired" | Re-login link |
| Not found | "Data not available" | Go back, search |
| Server | "Something went wrong" | Retry, contact support |
| Permission | "Access denied" | Request access |

### Graceful degradation ladder
```
Preferred:  Live data
Fallback 1: Cached data + "Last updated: X" warning
Fallback 2: Partial data (show what we have)
Fallback 3: Error state with recovery options
```

## Real-Time Update States

Always surface data freshness — a live number with no timestamp is untrustworthy.

```
┌─────────────────────────────────────────┐
│ Live Dashboard              ● Live      │
│                     Updated: Just now   │
└─────────────────────────────────────────┘
```

| State | Indicator |
|-------|-----------|
| Live / connected | Green dot + "Live" (`--color-success`) |
| Updating | Subtle pulse animation |
| Stale (> expected) | Warning + timestamp (`--color-warning`) |
| Disconnected | Error dot + "Reconnecting…" (`--color-error`) |

Briefly highlight changed values so updates register without jarring — fade from brand-subtle to transparent:
```css
.value-updated {
  animation: highlight 1.5s ease-out;
}

@keyframes highlight {
  0%   { background-color: var(--brand-primary-subtle); }
  100% { background-color: transparent; }
}
```

Give recent changes context where it helps:
```
Current: 156 users
         ↑ +3 in last 5 min   [View Last Hour ▼]
```

## Edge Case Handling

### Data
| Case | How to Handle |
|------|---------------|
| Zero values | Show "0", not empty |
| Negative numbers | Clear minus sign, error color |
| Very large numbers | Abbreviate (1.2M, 45K) |
| Very small numbers | Appropriate precision |
| Missing data points | Gap in chart + explanation |
| Single data point | Show value, note "trend unavailable" |

> Abbreviation pairs with the numeric-craft rule in [design-system.md](design-system.md): abbreviate for scale, set figures in `tabular-nums` so columns align.

### Display
| Case | How to Handle |
|------|---------------|
| Long text | Truncate + tooltip |
| Many items | Pagination or "Show all" |
| No comparison period | Note "No prior period" |
| Future dates | "Projected" label |
| Partial data | "Partial" badge |

## State Machine Pattern

Map every state and its transitions — gaps here are where production dashboards break.
```
            ┌──────────┐
            │  Empty   │
            └────┬─────┘
                 │ Data arrives
                 ▼
            ┌──────────┐
     ┌──────│ Loading  │──────┐
     │      └──────────┘      │
   Error                    Success
     │                        │
     ▼                        ▼
┌──────────┐            ┌──────────┐
│  Error   │◄───────────│  Loaded  │
└──────────┘   Refresh  └──────────┘
     │         fails          │
     └────────────────────────┘
           Retry succeeds
```

## Checklist

**Empty** — first-time, no-results, and completion states each designed; each has a clear CTA.
**Loading** — indicator matched to duration; skeletons mirror content layout; progressive load; no loading flash on fast responses.
**Error** — every error type messaged; recovery path clear; graceful degradation where possible; errors logged.
**Real-time** — freshness visible; connection status shown; stale-data warning; update animations subtle.
