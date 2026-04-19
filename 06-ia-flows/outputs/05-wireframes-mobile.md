# 05 — Wireframes: Mobile

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft

**Viewport:** 375px (iPhone SE / mid-range Android). Designed independently — not shrunk from desktop.  
**Navigation:** Bottom tab bar. No sidebar. Hamburger menu avoided (hides key actions).  
**Touch targets:** Minimum 44×44pt per Apple HIG / WCAG 2.5.5. Interactive elements are full-width or clearly oversized.  
**Greyscale only.** Borders = outlines. Fills = blocks. Text = real copy.

---

## Screen 1 — Dashboard (mobile)

### Default state

```
┌─────────────────────────────┐
│  Thornton CC · 2nd XI  ▼   │  ← team context, tappable to switch
│  ─────────────────────────  │
│                             │
│  NEEDS YOUR ATTENTION       │
│                             │
│  ┌─────────────────────────┐ │
│  │ Match request           │ │
│  │ Thornton CC 1st XI      │ │
│  │ 14 June · T20 · 8 mi   │ │
│  │ ◆ Reliable              │ │
│  │ [View request →]        │ │
│  └─────────────────────────┘ │
│                             │
│  UPCOMING FIXTURES          │
│                             │
│  ┌─────────────────────────┐ │
│  │ Sat 23 May              │ │
│  │ vs Redfield CC 2nd XI   │ │
│  │ ◆ Confirmed · T20       │ │
│  │ [View →]                │ │
│  └─────────────────────────┘ │
│                             │
│  ┌─────────────────────────┐ │
│  │ Sun 7 June              │ │
│  │ [Awaiting response]     │ │
│  │ Sent to Westfield CC    │ │
│  │ 2 days ago              │ │
│  │ [View →]                │ │
│  └─────────────────────────┘ │
│                             │
│  MY AVAILABILITY            │
│                             │
│  ┌─────────────────────────┐ │
│  │ Sun 28 June · T20       │ │
│  │ Awaiting opponent       │ │
│  │ [Edit]  [Withdraw]      │ │
│  └─────────────────────────┘ │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔3] │  ← bottom tab bar
└─────────────────────────────┘
```

**Annotations:**
- [A] Team context switcher is at the top — one tap. On desktop it was in the header; here it's the first element in the content area.
- [B] Bottom tab bar: Home / Find a game / Fixtures / Requests / Notifications. Five items max. Labels are abbreviated but recognisable. Badge count on notifications.
- [C] Cards are full-width. Tap targets fill the card (entire card is tappable, not just the "[View →]" link).
- [D] "Needs your attention" section is collapsed/absent when there's nothing to action. Not a permanent section header.

---

### Empty state (mobile)

```
┌─────────────────────────────┐
│  Thornton CC · 2nd XI  ▼   │
│  ─────────────────────────  │
│                             │
│  Hello, Graham.             │
│                             │
│  You have no fixtures yet.  │
│                             │
│  ┌─────────────────────────┐ │
│  │ [Find a game]           │ │
│  └─────────────────────────┘ │
│                             │
│  ┌─────────────────────────┐ │
│  │ [Post availability]     │ │
│  └─────────────────────────┘ │
│                             │
│  How it works:              │
│  1. Search for available    │
│     teams in your area.     │
│  2. Send a match request.   │
│  3. They accept — fixture   │
│     confirmed.              │
│  4. No results? Post your   │
│     availability instead.   │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

---

## Screen 2 — Find a game (mobile)

Mobile search form is a full-screen experience, not a sidebar panel.

### Default state

```
┌─────────────────────────────┐
│  ←  Find a game             │
│  ─────────────────────────  │
│                             │
│  Date                       │
│  ┌─────────────────────────┐ │
│  │  14 June 2026        ▼  │ │
│  └─────────────────────────┘ │
│                             │
│  Format                     │
│  ┌───┐ ┌──────┐ ┌──────┐   │
│  │T20│ │40-ov.│ │50-ov.│   │
│  │ ● │ │      │ │      │   │
│  └───┘ └──────┘ └──────┘   │
│  ┌──────┐ ┌──────┐         │
│  │Timed │ │Sunday│         │
│  │      │ │      │         │
│  └──────┘ └──────┘         │
│                             │
│  Home or away               │
│  ○ No preference            │
│  ● Home preferred           │
│  ○ Away preferred           │
│                             │
│  Distance                   │
│  ┌─────────────────────────┐ │
│  │  Within 20 miles     ▼  │ │
│  └─────────────────────────┘ │
│                             │
│  ▶ More options             │
│                             │
│  ┌─────────────────────────┐ │
│  │  Search for teams       │ │
│  └─────────────────────────┘ │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

**Annotations:**
- [A] Format selection uses a 2-row grid of toggle buttons (not a horizontal scroll — too fragile on small screens). All 5 formats visible without scrolling.
- [B] "Search for teams" is a full-width button at the bottom. Large touch target. No tiny "Go" button.
- [C] The ← back button returns to dashboard preserving no state — a new search starts fresh. Search results preserve state on their own back button.

---

### Loading state (mobile)

```
┌─────────────────────────────┐
│  ←  14 June · T20 · 20 mi  │
│  ─────────────────────────  │
│                             │
│  Searching...               │
│                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░ │  ← skeleton card
│  ░░░░░░░░░░░░░░░░░░░░░      │
│  ░░░░░░░░░░░░                │
│                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░ │
│  ░░░░░░░░░░░░░░░░░░░░░      │
│  ░░░░░░░░░░░░                │
│                             │
└─────────────────────────────┘
```

---

## Screen 3 — Search results (mobile)

### Populated state

```
┌─────────────────────────────┐
│  ← 14 June · T20 · 20 mi   │
│  4 teams available          │
│  ─────────────────────────  │
│                             │
│  ┌─────────────────────────┐ │
│  │ Thornton CC 1st XI      │ │
│  │ 8 miles · T20 · Tier 3  │ │
│  │ ◆ Reliable              │ │
│  │ [View →]                │ │
│  └─────────────────────────┘ │
│                             │
│  ┌─────────────────────────┐ │
│  │ Redfield CC 2nd XI      │ │
│  │ 13 miles · T20 · Tier 3 │ │
│  │ ● New                   │ │
│  │ [View →]                │ │
│  └─────────────────────────┘ │
│                             │
│  ┌─────────────────────────┐ │
│  │ Southbury Sunday XI     │ │
│  │ 18 miles · Sunday · T2  │ │
│  │ ⚠ Format to be agreed   │ │
│  │ ◆ Reliable              │ │
│  │ [View →]                │ │
│  └─────────────────────────┘ │
│                             │
│  ┌─────────────────────────┐ │
│  │ Oldwick CC 1st XI       │ │
│  │ 19 miles · T20 · Tier 4 │ │
│  │ ⚠ Higher tier level     │ │
│  │ ◆ Established           │ │
│  │ [View →]                │ │
│  └─────────────────────────┘ │
│                             │
│  ─────────────────────────  │
│  None right?                │
│  [Post availability →]      │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

**Annotations:**
- [A] Cards are compact on mobile. Key info: team name, distance, format, trust badge. Compatibility notice ⚠ is inline — visible without tapping.
- [B] Full cards are tappable. The "[View →]" link is an affordance indicator, not the only tap target.
- [C] "None right? [Post availability →]" is always at the bottom, even when results exist.

---

### Empty state (mobile)

```
┌─────────────────────────────┐
│  ← 14 June · T20 · 20 mi   │
│  ─────────────────────────  │
│                             │
│  No teams available for     │
│  14 June within 20 miles.   │
│                             │
│  ┌─────────────────────────┐ │
│  │ Try adjusting:          │ │
│  │                         │ │
│  │ Widen to 35 miles       │ │
│  │ [Try this →]            │ │
│  │                         │ │
│  │ Different date          │ │
│  │ [Adjust dates →]        │ │
│  │                         │ │
│  │ Include away games      │ │
│  │ [Change →]              │ │
│  └─────────────────────────┘ │
│                             │
│  ─────────────────────────  │
│                             │
│  Or post your availability. │
│  Teams searching for a 14   │
│  June T20 will find you.    │
│                             │
│  ┌─────────────────────────┐ │
│  │ Post availability for   │ │
│  │ 14 June                 │ │
│  └─────────────────────────┘ │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

---

## Screen 4 — Fixture detail (mobile)

Mobile fixture detail is a single-column view. "What's missing" panel becomes a banner at the top, not a right-column panel.

### Awaiting venue state

```
┌─────────────────────────────┐
│  ← My fixtures              │
│  ─────────────────────────  │
│                             │
│  vs Westfield CC 2nd XI     │
│  Sun 14 June · T20          │
│                             │
│  ┌─────────────────────────┐ │
│  │ ⚠ WHAT'S MISSING        │ │
│  │                         │ │
│  │ ✗ Venue                 │ │
│  │ [Confirm venue]         │ │
│  │                         │ │
│  │ ✓ Opponent confirmed    │ │
│  │ ✓ Officials n/a         │ │
│  └─────────────────────────┘ │
│                             │
│  Status: Awaiting venue     │
│                             │
│  FIXTURE DETAILS            │
│  Home team: Thornton CC     │
│  Away team: Westfield CC    │
│  Format: T20                │
│  Date: Sun 14 June          │
│  Start: 13:00 (unconfirmed) │
│  Venue: Not confirmed       │
│                             │
│  CONTACTS                   │
│  Your FM: You               │
│  Their FM: Sarah Okonkwo    │
│  sarah@westfield.cc         │
│                             │
│  HISTORY                    │
│  24 Apr: Request accepted   │
│  23 Apr: Request sent       │
│                             │
│  ─────────────────────────  │
│  [Cancel fixture]           │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

**Annotations:**
- [A] "What's missing" panel is now a banner at the top of the content area. On mobile it cannot be a right-column — it becomes the first thing the user sees after the page title.
- [B] "Confirm venue" is a full-width tap target within the banner.
- [C] Contact email is tappable (mailto: link on device).
- [D] "Cancel fixture" is a text link at the bottom — low visual weight. It is accessible but not prominent.

---

### Confirmed state (mobile)

```
┌─────────────────────────────┐
│  ← My fixtures              │
│                             │
│  vs Westfield CC 2nd XI     │
│  Sun 14 June · T20          │
│                             │
│  ┌─────────────────────────┐ │
│  │ ◆ ALL CONFIRMED          │ │
│  │                         │ │
│  │ ✓ Opponent              │ │
│  │ ✓ Venue: Thornton Park  │ │
│  │ ✓ Officials n/a         │ │
│  └─────────────────────────┘ │
│                             │
│  [rest of detail as above]  │
│                             │
│  [Cancel fixture]           │
│                             │
└─────────────────────────────┘
```

---

### Completed — mark complete (mobile)

```
┌─────────────────────────────┐
│  vs Westfield CC 2nd XI     │
│  Sun 14 June (past)         │
│                             │
│  ┌─────────────────────────┐ │
│  │ Did this fixture take   │ │
│  │ place?                  │ │
│  │                         │ │
│  │ [Mark as complete]      │ │
│  │ [Cancel this fixture]   │ │
│  └─────────────────────────┘ │
└─────────────────────────────┘
```

**Annotations:** After fixture date passes, the fixture transitions to a prompt state. "Mark as complete" vs "Cancel this fixture" clarifies the two possibilities without requiring the user to understand state machine vocabulary.

---

## Screen 5 — Send match request (mobile)

```
┌─────────────────────────────┐
│  ← Westfield CC availability│
│  ─────────────────────────  │
│                             │
│  Send match request         │
│  to Westfield CC 2nd XI     │
│                             │
│  DATE                       │
│  Sun 14 June 2026           │
│  (from their availability)  │
│                             │
│  FORMAT                     │
│  T20                        │
│  (from their availability)  │
│                             │
│  YOUR TEAM                  │
│  Thornton CC 2nd XI         │
│                             │
│  ─────────────────────────  │
│                             │
│  ADD A NOTE (optional)      │
│  ┌─────────────────────────┐ │
│  │                         │ │
│  │ e.g. "Happy to provide  │ │
│  │ teas. Similar level."   │ │
│  │                         │ │
│  │                         │ │
│  └─────────────────────────┘ │
│  0 / 200 characters         │
│                             │
│  ─────────────────────────  │
│                             │
│  ┌─────────────────────────┐ │
│  │  Send match request     │ │
│  └─────────────────────────┘ │
│                             │
│  [Cancel]                   │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

**Annotations:**
- [A] Fixed fields (date, format, team) are displayed as read-only text, not form inputs. This reduces visual noise and prevents confusion about what's editable.
- [B] Note textarea is the only interactive field. Keyboard-friendly: tapping opens keyboard, field scrolls into view.
- [C] Send button is full-width, high-contrast. "Cancel" is a plain text link below — accessible but not competing for attention.

---

## Screen 6 — Match request detail, receiving team (mobile)

```
┌─────────────────────────────┐
│  ← Requests                 │
│  ─────────────────────────  │
│                             │
│  Match request              │
│  from Thornton CC 1st XI    │
│  2 hours ago                │
│                             │
│  WHO'S ASKING               │
│  Thornton CC 1st XI         │
│  T20 · Women's · Tier 3     │
│  8 miles from your ground   │
│  Trust badge: ● New         │
│  (joined this season)       │
│                             │
│  FIXTURE DETAILS            │
│  Date: Sun 7 June 2026      │
│  Format: T20                │
│  Venue: To be agreed        │
│                             │
│  THEIR NOTE                 │
│  "We're looking for a June  │
│  T20. Similar level. We     │
│  can provide teas."         │
│                             │
│  ─────────────────────────  │
│  Expires 14 June (7 days).  │
│  Your availability for 7    │
│  June is reserved until     │
│  you respond.               │
│  ─────────────────────────  │
│                             │
│  ┌─────────────────────────┐ │
│  │  Accept                 │ │
│  └─────────────────────────┘ │
│                             │
│  [Decline]                  │
│                             │
├─────────────────────────────┤
│ [Home] [Find] [Fix.] [Req.] [🔔] │
└─────────────────────────────┘
```

**Annotations:**
- [A] "Trust badge: ● New (joined this season)" — the parenthetical explanation is important on mobile where screen real estate is limited. It prevents the "New" badge from being misread as "newcomer = untrustworthy" without surfacing the full trust design.
- [B] Accept is a full-width primary button. Decline is a plain text link — accessible, but lower visual weight. This is intentional: the platform is routing toward connection, not conflict. However, decline is never hidden.
- [C] Accept confirmation dialog (not shown above, appears on tap):

```
┌─────────────────────────────┐
│  Confirm?                   │
│                             │
│  Accepting creates a        │
│  fixture on 7 June with     │
│  Thornton CC 1st XI.        │
│                             │
│  Cancellations within 48    │
│  hours affect your trust    │
│  record.                    │
│                             │
│  [Confirm — Accept]         │
│  [Go back]                  │
└─────────────────────────────┘
```

**Why this dialog matters:** Priya is on her phone during lunch. The confirmation dialog provides a speed bump before the action is irreversible. It also surfaces the trust implication of late cancellation at the right moment — not buried in T&Cs.

---

## Mobile-specific patterns (applying across all screens)

### 1. Form handling
- All form fields that open a keyboard scroll the input into view automatically
- No form requires horizontal scrolling
- Date pickers use native device date picker (not custom JS calendar)
- Dropdowns use native select element on mobile (OS-native picker sheet)

### 2. Navigation conventions
- The ← back arrow in the top bar always matches the breadcrumb text (e.g., "← My fixtures" not just "← Back")
- Bottom tab bar is always visible. It does not hide on scroll.
- No floating action buttons (FAB). Actions are inline or in the bottom of the content area.

### 3. Touch targets
- All tappable elements minimum 44×44pt
- Cards are entirely tappable, not just the label/link within
- Destructive actions (Cancel fixture, Decline, Withdraw) are always at the bottom of the screen, never adjacent to a primary action

### 4. Notifications
- On-device notification (push, v2) → deep links to specific screens
- Email notification → mobile browser, deep link, no app required for Service Provider Bernard-type users

### 5. Offline state (mobile)

```
┌─────────────────────────────┐
│  ─────────────────────────  │
│  No internet connection.    │
│  Showing last saved data.   │
│  ─────────────────────────  │
│  [last known dashboard      │
│   content shown below,      │
│   read-only]                │
└─────────────────────────────┘
```

The platform gracefully degrades to read-only mode when offline. No actions can be taken. Submitted review drafts are queued and sent on reconnect.

---

## Key differences from desktop (not just resized)

| Screen | Desktop | Mobile |
|---|---|---|
| Dashboard | Left sidebar + card grid | Bottom tabs + single-column cards |
| What's missing panel | Right-column, always visible | Top banner, full width |
| Search form | Inline on page | Full-screen form |
| Format selection | 5-button horizontal row | 2-row 5-button grid |
| Trust badge | Icon + text label | Icon + text, same label |
| Match request detail | Two-column layout | Single column, action at bottom |
| Accept confirmation | Modal dialog | Bottom sheet / new screen |
| Team context switch | Top-right header dropdown | Top of content area, prominent |
