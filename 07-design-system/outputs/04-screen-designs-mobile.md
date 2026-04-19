# 04 — Screen Designs: Mobile

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 7 (Design System & Screen Design)  
**Status:** Pre-usability-test version  
**Viewport:** 375px (iPhone SE / mid-range Android). Designed independently — not shrunk from desktop.  
**Figma page:** Mobile screens (page 3 in Pavilion Design System.fig)

---

## Mobile layout system

```
┌─────────────────────────────────────────────┐
│  Status bar (OS)                            │  ← OS-managed, safe area
├─────────────────────────────────────────────┤
│  Top bar — 56px                             │  ← Back nav + page title OR
│                                             │     team context switcher (Dashboard)
├─────────────────────────────────────────────┤
│                                             │
│  Content area                               │
│  padding: 16px horizontal                   │
│  padding-top: 16px                          │
│  padding-bottom: 80px (tab bar clearance)   │
│                                             │
├─────────────────────────────────────────────┤
│  Bottom tab bar — 56px + safe area          │  ← Always visible, never hides
│  [Home] [Find] [Fixtures] [Req.] [Notif.]   │
└─────────────────────────────────────────────┘
```

**Top bar:**
- Background: white
- Border-bottom: 1px solid `--border-default`
- Left: ← [destination label] — `type-label`, `--color-primary-forest`
- Centre: page title — `type-label`, `--text-primary`, medium weight
- Right: contextual action (e.g., ⚙, filter) — optional

**Bottom tab bar:** C18 component. Always visible. Does not hide on scroll.

---

## Global mobile patterns

### Card tap target
Entire card surface is tappable — `<a>` wraps the entire card. Not just the "[View →]" link.
```css
.card-link {
  display: block;
  text-decoration: none;
  color: inherit;
}
.card-link:focus-visible {
  outline: var(--focus-ring);
  outline-offset: 2px;
}
```

### Form fields
- All inputs: `font-size: 16px` minimum — prevents iOS auto-zoom
- Date: native `<input type="date">` — OS-native date picker sheet
- Select: native `<select>` — OS-native picker sheet
- No horizontal scrolling anywhere

### Destructive actions
Always at the bottom of the screen, after a visual separator. Never adjacent to primary actions.

### Confirmation dialogs
Bottom sheet pattern (C08 mobile variant), not modal dialogs.

---

## Screen 01 — Dashboard (mobile)

### 01-A Default state

**Top bar:** No back arrow. "Pavilion" wordmark centred. Settings icon right.

```
┌─────────────────────────────────────────────┐
│  ← ·····  Pavilion  ····· ⚙               │  ← top bar
├─────────────────────────────────────────────┤
│                                             │
│  ┌─────────────────────────────────────┐    │  ← team context switcher (C16)
│  │  Thornton CC · 2nd XI           ▼  │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  Good evening, Graham.                      │  ← H3 serif, greeting
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  NEEDS YOUR ATTENTION                       │  ← section label
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Match request                      │    │
│  │  Thornton CC 1st XI                 │    │
│  │  14 June · T20 · 8 miles           │    │
│  │  ◆ Reliable                         │    │
│  │  [View request →]                   │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  UPCOMING FIXTURES                          │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Sat 23 May                         │    │
│  │  vs Redfield CC 2nd XI              │    │
│  │  ◆ Confirmed · T20 · Home           │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Sun 7 June                         │    │
│  │  [Awaiting response]                │    │
│  │  Sent to Westfield CC 1st XI        │    │
│  │  2 days ago                         │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Sun 14 June                        │    │
│  │  vs Oldwick CC 1st XI               │    │
│  │  [Awaiting venue] · T20             │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  MY AVAILABILITY                            │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Sun 28 June · T20                  │    │
│  │  Awaiting opponent                  │    │
│  │  [Edit]    [Withdraw]               │    │  ← both tappable, 44px min
│  └─────────────────────────────────────┘    │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Find a game                        │    │  ← Primary button, full-width
│  └─────────────────────────────────────┘    │
│  ┌─────────────────────────────────────┐    │
│  │  Post availability                  │    │  ← Secondary button, full-width
│  └─────────────────────────────────────┘    │
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.1]  [🔔3]    │  ← bottom tab bar
└─────────────────────────────────────────────┘
```

**Specifications:**
- Team context switcher: full-width, `--surface-subtle` background, 44px height, top of content
- Greeting: 20px (type-lead), serif, below switcher
- Section labels: `type-label`, `--text-tertiary`, uppercase, `--letter-spacing-widest`
- Needs-your-attention section: amber-subtle background, amber-light bottom border, `--space-4` padding. Absent when no action items.
- Fixture cards: full-width, `--border-default` border, `--radius-md`, `--space-4` padding, `--space-3` gap between cards. Entire card tappable.
- "NEEDS YOUR ATTENTION" inline card: full-width within the section container. Has explicit [View request →] action link for clarity (even though full card is tappable).
- Status pills (C04): inline within card, right of fixture date or as second line
- [Edit] and [Withdraw]: side-by-side, each min 44px touch target. Ghost/text button style.
- Primary CTA row: stacked full-width buttons at bottom, `--space-3` gap

---

### 01-B Empty state (mobile)

```
┌─────────────────────────────────────────────┐
│  ← ·····  Pavilion  ·····               ⚙ │
├─────────────────────────────────────────────┤
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Thornton CC · 2nd XI           ▼  │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  Hello, Graham.                             │
│                                             │
│  You have no fixtures yet.                  │
│                                             │
│  Start by searching for available teams,    │
│  or post your availability so other clubs   │
│  can find you.                              │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Find a game                        │    │
│  └─────────────────────────────────────┘    │
│  ┌─────────────────────────────────────┐    │
│  │  Post availability                  │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  How it works                               │  ← type-lead, serif
│                                             │
│  1. Search for available teams near you     │
│     on a specific date and format.          │
│  2. Send a match request when you find      │
│     a suitable team.                        │
│  3. They accept — fixture confirmed.        │
│  4. If no results, post your availability.  │
│     Other clubs will find you.              │
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

---

### 01-C Loading state (mobile)

Skeleton cards in single-column layout. Team context switcher shows (from session cache).

### 01-D Error state (mobile)

```
[Pavilion wordmark]

Unable to load your dashboard.
Check your connection and try again.

[Try again]

support@pavilion.cricket
```

---

## Screen 02 — Find a game (mobile)

### 02-A Default state

**Top bar:** `← Home` (left), "Find a game" (centre)

```
┌─────────────────────────────────────────────┐
│  ←  Home        Find a game                 │  ← top bar
├─────────────────────────────────────────────┤
│                                             │
│  Date                                       │
│  ┌─────────────────────────────────────┐    │
│  │  14 June 2026                    ▼  │    │  ← native date input
│  └─────────────────────────────────────┘    │
│                                             │
│  Format                                     │
│                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │   T20    │  │  40-ov   │  │  50-ov   │  │  ← 3 per row
│  └──────────┘  └──────────┘  └──────────┘  │
│  ┌──────────┐  ┌──────────┐               │
│  │  Timed   │  │ Sunday   │               │  ← 2 per row (staggered)
│  └──────────┘  └──────────┘               │
│                                             │
│  Venue preference                           │
│  ○ No preference                            │
│  ● Home preferred                           │
│  ○ Away preferred                           │
│                                             │
│  Distance                                   │
│  ┌─────────────────────────────────────┐    │
│  │  Within 20 miles                 ▼  │    │  ← native select
│  └─────────────────────────────────────┘    │
│                                             │
│  ▶ More options                             │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Search for available teams         │    │  ← Primary full-width
│  └─────────────────────────────────────┘    │
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

**Specifications:**
- Date: `<input type="date">`, full-width, native picker on tap
- Format: Toggle button grid C15 (3+2 layout), each button `height: 48px`
- Venue preference: vertical radio group C13, each option 44px min touch target
- Distance: `<select>` full-width, native picker
- "More options" disclosure: expands to show Age group and Gender radios (each vertical stack)
- Search button: full-width primary, `height: 52px` for prominence
- Bottom tab bar nav item "Find" is active on this screen

---

### 02-B Loading state (mobile)

```
┌─────────────────────────────────────────────┐
│  ←  Search     14 June · T20                │  ← top bar shows search params
├─────────────────────────────────────────────┤
│                                             │
│  Searching...                               │  ← live region, aria-live="polite"
│                                             │
│  [Skeleton card]                            │
│  [Skeleton card]                            │
│                                             │
└─────────────────────────────────────────────┘
```

---

## Screen 03 — Search results (mobile)

### 03-A Populated state

**Top bar:** `← 14 June · T20 · 20 mi` (left), result count badge

```
┌─────────────────────────────────────────────┐
│  ←  14 June · T20 · 20 mi                  │
├─────────────────────────────────────────────┤
│                                             │
│  4 teams available                          │  ← H3 serif
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Thornton CC 1st XI                 │    │
│  │  8 miles · T20 · Tier 3             │    │
│  │  ◆ Reliable                         │    │
│  └─────────────────────────────────────┘    │  ← full card tappable
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Redfield CC 2nd XI                 │    │
│  │  13 miles · T20 · Tier 3            │    │
│  │  ● New                              │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Southbury CC Sunday XI             │    │
│  │  18 miles · Sunday                  │    │
│  │  ⚠ Format to be agreed              │    │
│  │  ◆ Reliable                         │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Oldwick CC 1st XI                  │    │
│  │  19 miles · T20 · Tier 4            │    │
│  │  ⚠ Higher tier level                │    │
│  │  ◆ Established                      │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ─────────────────────────────────────      │
│  None of these right?                       │
│  [Post availability →]                      │  ← Forest ghost link
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

**Result card specs (mobile):**
- Full width, `--border-default`, `--radius-md`, `--space-4` padding
- Club name: 16px, medium sans, `--text-primary`
- Distance + format: 14px, `--text-secondary`
- Compatibility notice ⚠ (if present): amber text, amber-subtle background inline block, full width, 14px
- Trust badge: inline, 14px, badge-colour text + indicator icon

---

### 03-B Empty state (mobile)

```
┌─────────────────────────────────────────────┐
│  ←  14 June · T20 · 20 mi                  │
├─────────────────────────────────────────────┤
│                                             │
│  No teams available for 14 June             │
│  within 20 miles.                           │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Try adjusting:                     │    │
│  │                                     │    │
│  │  Widen to 35 miles                  │    │
│  │  [Try this →]                       │    │
│  │                                     │    │
│  │  Try a different date               │    │
│  │  [Adjust dates →]                   │    │
│  │                                     │    │
│  │  Include away games                 │    │
│  │  [Change →]                         │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  Or post your availability for this date.   │
│  Teams searching for a 14 June T20          │
│  will find you.                             │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Post availability for 14 June      │    │  ← Primary full-width, pre-fills
│  └─────────────────────────────────────┘    │
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

---

## Screen 04 — Fixture detail (mobile)

### 04-A Awaiting venue state

**Top bar:** `← My fixtures` (left), "Fixture" (centre)

```
┌─────────────────────────────────────────────┐
│  ←  My fixtures      Fixture                │
├─────────────────────────────────────────────┤
│                                             │
│  vs Westfield CC 2nd XI                     │  ← H3 serif, 24px
│  Sun 14 June · T20                          │  ← type-lead, secondary
│  [Awaiting venue]                           │  ← Status pill (C04)
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  ⚠ WHAT'S MISSING                   │    │  ← amber-subtle bg, amber border
│  │                                     │    │
│  │  ✗ Venue                            │    │  ← bold, text-primary
│  │  ┌─────────────────────────────┐    │    │
│  │  │ Confirm venue               │    │    │  ← Secondary full-width button
│  │  └─────────────────────────────┘    │    │
│  │                                     │    │
│  │  ✓ Opponent confirmed               │    │  ← tertiary text
│  │  ✓ Officials n/a (friendly)         │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  FIXTURE DETAILS                            │
│  ─────────────────────────────────────      │
│  Home team   Thornton CC 2nd XI             │
│  Away team   Westfield CC 2nd XI            │
│  Format      T20                            │
│  Date        Sun 14 June 2026               │
│  Start time  13:00 (unconfirmed)            │
│  Venue       Not confirmed                  │
│  Officials   Not required                   │
│                                             │
│  CONTACTS                                   │
│  ─────────────────────────────────────      │
│  Your FM     You                            │
│  Their FM    Sarah Okonkwo                  │
│              sarah@westfield.cc             │  ← mailto: link
│                                             │
│  HISTORY                                    │
│  ─────────────────────────────────────      │
│  24 Apr    Request accepted                 │
│  23 Apr    Request sent                     │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  [Cancel fixture]                           │  ← ghost text, error-text colour, bottom
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

**Specifications:**
- "What's missing" panel: full-width banner, amber-subtle background, amber-light bottom border, `--space-4` padding
- "Confirm venue" button within the panel: Secondary full-width, 44px min, inside the panel
- Section labels: `type-label`, `--text-tertiary`, uppercase, `--space-5` top margin
- Detail rows: label 40% width, value 60%, both 16px, `--space-2` vertical gap
- Contact email: tappable `mailto:` link, Forest colour
- History entries: 14px, `--text-secondary`; date in `--text-tertiary`
- "Cancel fixture": `--color-error-text`, text button, 44px min touch target; opens C08 bottom sheet

---

### 04-B Confirmed state (mobile)

"What's missing" banner changes to:
```
┌─────────────────────────────────────────────┐
│  ✓ ALL CONFIRMED                            │  ← Forest colour header
│                                             │
│  ✓ Opponent: Westfield CC 2nd XI            │
│  ✓ Venue: Thornton Park                     │
│  ✓ Officials n/a                            │
└─────────────────────────────────────────────┘
```
Background: rgba(14,92,66,0.06). Border: none (no longer warning).

---

### 04-C Mark complete / completed prompt (mobile)

```
┌─────────────────────────────────────────────┐
│  Did this fixture take place?               │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Mark as complete                   │    │  ← Primary full-width
│  └─────────────────────────────────────┘    │
│  ┌─────────────────────────────────────┐    │
│  │  Cancel this fixture                │    │  ← Secondary full-width
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
```

After marking complete, review prompt as bottom sheet:

```
[Bottom sheet]
Leave a review for Westfield CC?
Your review is private.
[Leave a review]     (44px, primary)
[Not now]            (ghost link below)
```

---

### 04-D Loading state (mobile)

Skeleton rows in single-column. Top banner area shows skeleton block (same height as "What's missing").

---

## Screen 05 — Send match request (mobile)

**Top bar:** `← Westfield CC availability` (left), "Match request" (centre)

```
┌─────────────────────────────────────────────┐
│  ← Westfield CC        Match request        │
├─────────────────────────────────────────────┤
│                                             │
│  Send match request                         │  ← H3 serif
│  to Westfield CC 2nd XI                     │  ← type-lead, secondary
│                                             │
│  DATE                                       │
│  Sunday 14 June 2026                        │
│  From their availability                    │  ← caption, tertiary
│                                             │
│  FORMAT                                     │
│  T20                                        │
│  From their availability                    │
│                                             │
│  YOUR TEAM                                  │
│  Thornton CC 2nd XI                         │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  ADD A NOTE  (optional)                     │
│  ┌─────────────────────────────────────┐    │
│  │                                     │    │
│  │  e.g. "Happy to provide teas.       │    │
│  │  Similar level."                    │    │
│  │                                     │    │
│  │                                     │    │
│  └─────────────────────────────────────┘    │
│  0 / 200 characters                         │  ← caption, tertiary
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  ⚠  FORMAT NOTE                     │    │  ← amber-subtle bg
│  │  Sunday XI prefer Sunday format.    │    │
│  │  You're requesting T20. Confirm     │    │
│  │  with them before the match.        │    │
│  └─────────────────────────────────────┘    │
│  ☐ I understand and will confirm            │
│    the format with Westfield CC             │  ← checkbox + label, 44px
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Send match request                 │    │  ← Primary full-width
│  └─────────────────────────────────────┘    │
│                                             │
│  [Cancel]                                   │  ← ghost link, centred
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

---

## Screen 06 — Match request detail (mobile, receiving team)

**Top bar:** `← Requests` (left), "Match request" (centre)

```
┌─────────────────────────────────────────────┐
│  ←  Requests         Match request          │
├─────────────────────────────────────────────┤
│                                             │
│  Match request from                         │  ← type-lead, secondary
│  Thornton CC 1st XI                         │  ← H3 serif
│  2 hours ago                                │  ← caption, tertiary
│                                             │
│  WHO'S ASKING                               │
│  ─────────────────────────────────────      │
│  Thornton CC 1st XI                         │  ← medium, 16px
│  T20 · Women's · Tier 3                     │  ← 14px, secondary
│  8 miles from your ground                   │
│                                             │
│  Trust badge: ● New                         │  ← badge (C03) + explanation
│  (joined platform this season)              │  ← 14px, secondary
│                                             │
│  FIXTURE DETAILS                            │
│  ─────────────────────────────────────      │
│  Date        Sun 7 June 2026                │
│  Format      T20                            │
│  Venue       To be agreed                   │
│                                             │
│  THEIR NOTE                                 │
│  ─────────────────────────────────────      │
│  "We're looking for a June T20. Similar     │
│  level. We can provide teas."               │
│                                             │
│  ─────────────────────────────────────      │
│  Expires 14 June (7 days).                  │  ← caption, secondary
│  Your availability for 7 June is            │
│  reserved until you respond.                │
│  ─────────────────────────────────────      │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Accept                             │    │  ← Primary full-width
│  └─────────────────────────────────────┘    │
│                                             │
│  [Decline]                                  │  ← ghost text, centred, 44px
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.1]  [🔔]     │
└─────────────────────────────────────────────┘
```

**Accept confirmation (bottom sheet):**
```
┌─────────────────────────────────────────────┐
│  ─────   (drag handle)                      │
│                                             │
│  Accept match request                       │  ← H3 serif
│                                             │
│  This creates a fixture on 7 June           │
│  with Thornton CC 1st XI.                   │
│                                             │
│  Cancellations within 48 hours of           │
│  the match affect your trust record.        │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Confirm — Accept                   │    │  ← Primary full-width
│  └─────────────────────────────────────┘    │
│                                             │
│  [Go back]                                  │  ← ghost link, initial focus
│                                             │
└─────────────────────────────────────────────┘
```

**Decline confirmation (bottom sheet):**
```
Are you sure you want to decline?
Declining will release your availability for 7 June.

[Confirm — Decline]    (destructive button)
[Go back]              (ghost link, initial focus)
```

---

## Screen 07 — Post availability (mobile)

**Top bar:** `← Dashboard` (or `← Search results`), "Post availability"

```
┌─────────────────────────────────────────────┐
│  ←  Dashboard    Post availability          │
├─────────────────────────────────────────────┤
│                                             │
│  Date                                       │
│  ┌─────────────────────────────────────┐    │
│  │  Select a date                   ▼  │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  Format                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │   T20    │  │  40-ov   │  │  50-ov   │  │
│  └──────────┘  └──────────┘  └──────────┘  │
│  ┌──────────┐  ┌──────────┐               │
│  │  Timed   │  │ Sunday   │               │
│  └──────────┘  └──────────┘               │
│                                             │
│  Venue preference                           │
│  ○ No preference                            │
│  ● Home preferred                           │
│  ○ Away preferred                           │
│                                             │
│  ▶ More options                             │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Post availability                  │    │  ← Primary full-width
│  └─────────────────────────────────────┘    │
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

---

## Screen 08 — Review form (mobile)

**Top bar:** `← Fixture detail`, "Review"

```
┌─────────────────────────────────────────────┐
│  ← Fixture detail    Review                 │
├─────────────────────────────────────────────┤
│                                             │
│  Leave a review for                         │
│  Westfield CC 2nd XI                        │
│  14 June · T20                              │
│                                             │
│  Your review is private.                    │  ← caption, tertiary
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  1. Did the match take place as agreed?     │  ← type-lead, 20px serif
│                                             │
│  ○ Yes, everything as agreed                │  ← 44px touch targets
│  ○ Minor changes but still played           │
│  ○ No — they cancelled or didn't show       │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  2. How was organising this match?          │
│                                             │
│  ○ Straightforward — good communication     │
│  ○ Some issues, but resolved                │
│  ○ Difficult — slow or no communication     │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  3. Would you play this club again?         │
│                                             │
│  ○ Yes — would recommend                    │
│  ○ Possibly — with reservations             │
│  ○ No                                       │
│                                             │
│  ─────────────────────────────────────      │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Submit review                      │    │  ← Primary, disabled until all 3 answered
│  └─────────────────────────────────────┘    │
│                                             │
│  [Not now — remind me later]                │  ← ghost link
│                                             │
├─────────────────────────────────────────────┤
│  [Home]  [Find]  [Fix.]  [Req.]  [🔔]      │
└─────────────────────────────────────────────┘
```

---

## Screen 09 — Club onboarding (mobile, 3-step)

**Step indicator:** "Step 1 of 3" — plain text, `type-label`, `--text-tertiary`, below top bar.

Step 1: Club name (text input), postcode (text input), county (native select).  
Step 2: Team setup — name, gender, age group, tier. [+ Add another team] ghost link.  
Step 3: Review summary. All entries shown as read-only. Edit links (ghost) per section. [Complete setup] primary full-width.

No progress bar — step count text is sufficient. Progress bars suggest a longer process than 3 steps warrant.

---

## Screen 10 — Notification preferences (mobile)

**Top bar:** `← Settings`, "Notifications"

List of notification types as rows. Each row: notification name (left) + email toggle (right) + in-app toggle (far right, or stacked if space tight).

Toggles: `role="switch"`, `aria-checked`, 44px touch target.  
Auto-save. Brief "Saved" toast (Forest, 3s, bottom of screen above tab bar).
