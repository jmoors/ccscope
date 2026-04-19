# 03 — Screen Designs: Desktop

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 7 (Design System & Screen Design)  
**Status:** Pre-usability-test version — structure finalised; may update after Agent 6 usability results  
**Viewport:** 1280px. Sidebar: 240px. Content area: 1040px. Max inner content: 960px.  
**Figma page:** Desktop screens (page 2 in Pavilion Design System.fig)

---

## Layout system

```
┌──────────────┬──────────────────────────────────────────────────────────┐
│              │  ┌──────────────────────────────────────────────────┐    │
│   Sidebar    │  │  Page header (breadcrumb / title / team context) │    │
│   240px      │  └──────────────────────────────────────────────────┘    │
│              │                                                           │
│   (C17)      │  Content area                                            │
│              │  max-width: 960px, horizontally centered                 │
│              │                                                           │
└──────────────┴──────────────────────────────────────────────────────────┘
```

- Sidebar: `position: fixed`, full height, `z-index: 10`
- Content area: `margin-left: 240px`, `padding: 40px 48px`
- Page title: H2 (serif, 32px, medium), below breadcrumb

---

## Page header pattern

```
[← Back to [destination]]       ← breadcrumb, type-label, ghost link; omit on Dashboard
─────────────────────────────────────────────────────────────────────────
[Page title]                                [Graham Okafor] · [2nd XI ▼]
```

- Breadcrumb: `--text-secondary`, 14px; always labelled with destination (not just "Back")
- Horizontal rule: 1px solid `--border-default`, `margin-bottom: --space-6`
- Title: H2 (serif, 32px)
- Team context switcher: top-right, see C16

---

## Screen 01 — Dashboard

### 01-A Default state

**URL:** `/dashboard`  
**Page title:** none (greeting is the lead)

**Layout:**
```
Good evening, Graham.                            [Graham Okafor] · [2nd XI ▼]

┌──────────────────────────────────────────────────────────────────────────┐
│ NEEDS YOUR ATTENTION                                                     │
│                                                                          │
│ ┌──────────────────────────────────────────────────────────────────────┐ │
│ │ Match request from Thornton CC 1st XI         [View request →]       │ │
│ │ Sunday 14 June · T20 · Home at Thornton Park                        │ │
│ │ "We'd love a game. Similar level, good pitch."                      │ │
│ │ ◆ Reliable                                                          │ │
│ └──────────────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────────┘

UPCOMING FIXTURES

┌────────────────────────────────┐  ┌────────────────────────────────┐
│ Sat 23 May                     │  │ Sun 7 June                     │
│ vs Redfield CC 2nd XI          │  │ [Awaiting response]            │
│ ◆ Confirmed                    │  │ Sent to Westfield CC 1st XI    │
│ T20 · Home                     │  │ Waiting since 2 days ago       │
│ [View →]                       │  │ [View →]  [Withdraw]           │
└────────────────────────────────┘  └────────────────────────────────┘

┌────────────────────────────────┐  ┌────────────────────────────────┐
│ Sun 14 June                    │  │ Sat 20 June                    │
│ vs Oldwick CC 1st XI           │  │ vs TBC                         │
│ [Awaiting venue]               │  │ [Awaiting opponent]            │
│ T20 · Away                     │  │ T20 · Home preferred           │
│ [View →]                       │  │ Posted 5 days ago              │
└────────────────────────────────┘  └────────────────────────────────┘

──────────────────────────────────────────────────────────────────────────

[Find a game]         [Post availability]
```

**Specifications:**

- Greeting: H3 (serif, 24px, medium). First name only. Time-based prefix (Good morning/afternoon/evening). No "Welcome back!"
- "NEEDS YOUR ATTENTION" section:
  - Appears only when action items exist; absent otherwise
  - Section label: `type-label`, `--text-tertiary`, uppercase, `--letter-spacing-widest`
  - Container: amber-subtle background `#f5ead9`, 1px amber-light border, `--radius-lg`
  - Inline match request cards within this section: white background
- "UPCOMING FIXTURES" label: same as section label above
- Fixture cards: 2-column grid, `gap: --space-4 (16px)`, C02 component
- Bottom CTA row: `margin-top: --space-8 (32px)`, two buttons side-by-side
  - [Find a game]: Primary button
  - [Post availability]: Secondary button

**Needs-attention card (match request inline):**
- Shows: club name, date, format, venue, trust badge, first 60 chars of note
- Single action: [View request →] ghost link, right-aligned
- Trust badge: inline variant (C03)

**Content density note:** Always show minimum 3 fixture cards. If fewer than 3, show "Post availability" prompt card in remaining slots as a soft nudge.

---

### 01-B Empty state

**Condition:** New user, no fixtures, no availability posted.

```
Good morning, Graham.                           [Graham Okafor] · [2nd XI ▼]

┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Your fixture list is empty.                                             │
│                                                                          │
│  Start by searching for available teams, or post your own availability   │
│  so other clubs can find you.                                            │
│                                                                          │
│  [Find a game]          [Post availability]                              │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘

──────────────────────────────────────────────────────────────────────────

HOW IT WORKS

1. Search for available teams near you on a specific date and format.
2. Send a match request when you find a suitable team.
3. They accept, and your fixture is confirmed.
4. If no teams are available, post your own availability.
   Other clubs searching for the same date will find you.
```

**Specifications:**
- Empty state card: C09 Dashboard empty variant
- "HOW IT WORKS" section: `margin-top: --space-12 (48px)`, numbered list in `type-body`
- Section label same as other section labels
- No fake data, no illustration

---

### 01-C Loading state

Skeleton cards in place of fixture grid. "Needs your attention" section omitted during load (appears only when data confirms action items exist).

```
Good [time], [name].

[Skeleton: greeting placeholder — 200px width bar]

[Skeleton: card]   [Skeleton: card]
[Skeleton: card]   [Skeleton: card]
```

- aria-busy="true" on content area
- aria-label="Loading dashboard"
- Skeleton appears after 200ms (CSS transition-delay)

---

### 01-D Error state

```
Good [time], [name].

Unable to load your dashboard.
Check your internet connection and try again.

[Try again]

If this continues, contact support at support@pavilion.cricket
```

- Greeting preserved (cached from session)
- Error message: `type-body`, `--text-primary`
- No red colour — this is a transient state, not a validation error
- "Try again": Primary button
- Support contact: plain text, `type-caption`

---

## Screen 02 — Find a game

### 02-A Default state

**URL:** `/find`  
**Breadcrumb:** none (top-level nav item)  
**Page title:** "Find a game"

```
Find a game                                    [Graham Okafor] · [2nd XI ▼]
──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Date                                                                    │
│  ┌────────────────────────┐                                              │
│  │  14 June 2026       ▼  │  or  [Search across a date range ▼]         │
│  └────────────────────────┘                                              │
│                                                                          │
│  Format                                                                  │
│  ┌──────┐ ┌────────┐ ┌────────┐ ┌──────────────┐ ┌──────────────┐      │
│  │  T20 │ │ 40-ov  │ │ 50-ov  │ │ Timed decl.  │ │ Sunday XI    │      │
│  └──────┘ └────────┘ └────────┘ └──────────────┘ └──────────────┘      │
│  (none pre-selected — user must choose)                                  │
│                                                                          │
│  Venue preference                                                        │
│  ○ No preference   ● Home preferred   ○ Away preferred                  │
│                                                                          │
│  Distance                                                                │
│  ┌──────────────────────────┐                                            │
│  │  Within 20 miles      ▼  │  Searching from: Thornton, GU14 [Change]  │
│  └──────────────────────────┘                                            │
│                                                                          │
│  ▶ More options (age group, gender)                                      │
│                                                                          │
│  ┌──────────────────────────────────────────┐                            │
│  │  Search for available teams              │                            │
│  └──────────────────────────────────────────┘                            │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

**Specifications:**
- Form container: white, `--border-default` border, `--radius-lg`, `--space-8` padding
- Date input: C12 select, 220px width
- "Search across a date range" is a disclosure toggle (`<details>/<summary>` or button) that reveals a date-from / date-to pair
- Format toggle group: C15, horizontal row, 5 buttons. No pre-selection. If submitted without selecting format: inline validation error "Please select a format."
- "Home preferred" radio: pre-selected as most common scenario. If club has no home ground set, show "(Add your home ground in Club settings)" greyed note
- Distance select: C12, 200px. Default 20 miles.
- Search origin: `type-caption` below distance select. [Change] ghost link opens a postcode input overlay.
- "More options" disclosure: reveals age group radio (Open / U18 / U15 / U13) and gender radio (Open / Men's / Women's / Mixed). Collapsed by default.
- Submit button: Primary, 300px width on desktop

**Validation:**
- Format is the only required field (date defaults to today + 7 days if not changed; distance defaults to 20 miles)
- If format not selected on submit: red inline error above format group

---

### 02-B Loading state (after submit)

**URL:** `/search-results` (transitional)

```
Find a game                                    [Graham Okafor] · [2nd XI ▼]
──────────────────────────────────────────────────────────────────────────

Searching for teams available on 14 June · T20...

──────────────────────────────────────────────────────────────────────────
[Skeleton: card]
[Skeleton: card]
[Skeleton: card]
```

- Page title changes to search context string
- Skeleton cards appear after 200ms
- aria-live="polite" region updates to "4 teams found" when results arrive (or "No teams found")

---

## Screen 03 — Search results

### 03-A Populated state

**URL:** `/search-results?date=2026-06-14&format=t20&pref=home&distance=20`  
**Breadcrumb:** `← Back to search`

```
[← Back to search]  14 June · T20 · Home preferred · within 20 miles

4 teams available                               [Graham Okafor] · [2nd XI ▼]
──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────┐
│ Thornton CC 1st XI                                        8 miles away  │
│ T20 · Men's · Open · Tier 3                     ◆ Reliable              │
│ Home: Thornton Park, Thornton                                            │
│                                             [View availability →]       │
└──────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│ Redfield CC 2nd XI                                       13 miles away  │
│ T20 · Men's · Open · Tier 3                              ● New          │
│ Home: Redfield Recreation Ground                                         │
│                                             [View availability →]       │
└──────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│ Southbury CC Sunday XI                                   18 miles away  │
│ Sunday format preferred · Men's · Open · Tier 2                         │
│ ⚠ Format note: Sunday XI matches on T20 by agreement                   │
│ ◆ Reliable                                                               │
│                                             [View availability →]       │
└──────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│ Oldwick CC 1st XI                                        19 miles away  │
│ T20 · Men's · Open · Tier 4                                              │
│ ⚠ Tier note: They play at a higher tier level (Tier 4 vs your Tier 3)  │
│ ◆ Established                                                            │
│                                             [View availability →]       │
└──────────────────────────────────────────────────────────────────────────┘

──────────────────────────────────────────────────────────────────────────

None of these right?  [Post your availability instead →]
```

**Specifications:**
- Result count ("4 teams available"): H3, serif, `--text-primary`, positioned below search summary line
- Search summary line: `type-label`, `--text-secondary`, immediately below breadcrumb
- Result cards: full width of content area, `gap: --space-3 (12px)` between cards
- Card header line: club/team name left (H3-like weight, 18px, medium sans), distance right (`--text-tertiary`, 14px)
- Card detail line: format · gender · age · tier, all `--text-secondary`, 14px
- Trust badge: inline variant (C03), right of detail line
- Compatibility notice ⚠ (C06): below detail line, amber-subtle tinted, inline
- Action link "View availability →": right-aligned, `--color-primary-forest`, 14px, underline on hover
- Entire card is clickable (same as [View availability →] action)

**Footer:**
- Divider
- "None of these right?" `--text-secondary` 14px + "[Post your availability instead →]" Forest ghost link
- Always present, even when results exist

---

### 03-B Empty state

```
[← Back to search]  14 June · T20 · Home preferred · within 20 miles
──────────────────────────────────────────────────────────────────────────

No availability found for 14 June within 20 miles.

┌──────────────────────────────────────────────────────────────────────────┐
│ Try adjusting your search                                                │
│                                                                          │
│  • Widen to 35 miles                                    [Try this →]    │
│  • Try a different date                             [Adjust dates →]    │
│  • Include away games                          [Change preference →]    │
└──────────────────────────────────────────────────────────────────────────┘

──────────────────────────────────────────────────────────────────────────

Or post your availability for this date.
Other teams searching for a 14 June T20 will find you.

[Post availability for 14 June]    ← Primary button, pre-fills form
```

**Note:** [Try this →] links apply search parameter adjustments inline — they re-run the search, not navigate away. Each "Try" link is only shown if its suggestion is contextually valid.

---

## Screen 04 — Fixture detail

### 04-A Awaiting venue state

**URL:** `/fixtures/[id]`  
**Breadcrumb:** `← My fixtures`

```
[← My fixtures]                                [Graham Okafor] · [2nd XI ▼]

Thornton CC 2nd XI vs Westfield CC 2nd XI
Sunday 14 June 2026 · T20 · Men's                    [Awaiting venue]

──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────┐  ┌───────────────────────┐
│  FIXTURE DETAILS                             │  │ WHAT'S MISSING        │
│                                              │  │                       │
│  Home team    Thornton CC 2nd XI             │  │ ✗ Venue               │
│  Away team    Westfield CC 2nd XI            │  │   [Confirm venue →]   │
│  Format       T20                            │  │                       │
│  Date         Sunday 14 June 2026            │  │ ✓ Opponent            │
│  Start time   13:00 (unconfirmed)            │  │ ✓ Officials n/a       │
│  Venue        Not confirmed                  │  │   (friendly)          │
│  Officials    Not required                   │  │                       │
│                                              │  │ Once venue is         │
│  ────────────────────────────────────────    │  │ confirmed, this       │
│                                              │  │ fixture is Confirmed. │
│  CONTACTS                                    │  └───────────────────────┘
│  Your FM        You
│  Their FM       Sarah Okonkwo
│  Contact via    sarah@westfield.cc
│
│  ────────────────────────────────────────
│
│  HISTORY
│  23 Apr 2026    Match request sent
│  24 Apr 2026    Match request accepted by Westfield CC
│
│  ────────────────────────────────────────
│
│  [Cancel fixture]                           ← destructive, bottom
└──────────────────────────────────────────────┘
```

**Specifications:**
- Two-column layout: main content ~70%, "What's missing" panel ~30% (min 240px)
- Fixture title: H2 (serif, 32px, medium)
- Status pill (C04) right of subtitle line
- Section labels: `type-label`, `--text-tertiary`, uppercase
- Detail rows: label in `--text-tertiary` 14px, value in `--text-primary` 16px. Two-column grid (`140px label`, `auto value`)
- Contact email: anchor tag (mailto:), Forest colour, underline on hover
- History entries: `--text-secondary`, 14px. Date in `--text-tertiary`
- "Cancel fixture": `--color-error-text` ghost link. Below a visual divider. On click: C08 confirmation dialog (destructive variant)

**"What's missing" panel (C05 — desktop column variant):**
- Floats right, sticky within the content column (position: sticky, top: 40px)
- Always visible within the viewport at 1280px
- If window narrows below 900px, panel moves below main content (single column)

---

### 04-B Confirmed state

Status pill: [Confirmed] (Forest green pill)

"What's missing" panel header changes to:
```
┌───────────────────────┐
│ ALL CONFIRMED ✓       │
│                       │
│ ✓ Opponent            │
│ ✓ Venue               │
│ ✓ Officials n/a       │
│                       │
│ [Cancel fixture]      │
└───────────────────────┘
```

Panel background: rgba(14,92,66,0.06), Forest-tinted.

---

### 04-C Completed state (fixture date passed)

After the fixture date passes, a prompt appears above the fixture details:

```
┌──────────────────────────────────────────────────────────────────────────┐
│ Did this fixture take place?                                             │
│                                                                          │
│ [Mark as complete]   [Cancel this fixture]                               │
└──────────────────────────────────────────────────────────────────────────┘
```

After "Mark as complete":
- Status pill changes to [Completed]
- A review prompt appears:

```
┌──────────────────────────────────────────────────────────────────────────┐
│ Leave a review for Westfield CC 2nd XI?                                  │
│ Your review is private and helps other clubs find good games.            │
│                                                                          │
│ [Leave a review →]    [Not now — remind me in 3 days]                   │
└──────────────────────────────────────────────────────────────────────────┘
```

---

### 04-D Cancelled state

Status pill: [Cancelled]
"What's missing" panel removed. Replaced with:

```
This fixture was cancelled.
[date and reason if known]
```

Main details remain visible (read-only). No action buttons.

---

### 04-E Loading state

Two-column skeleton:
- Left: skeleton panel (~70% width)
- Right: skeleton panel (~30% width, matching "What's missing" height)

---

### 04-F Error state

```
Unable to load this fixture.
[Try again]   support@pavilion.cricket
```

---

## Screen 05 — Send match request

### 05-A Default state

**URL:** `/send-request/[availability-id]`  
**Breadcrumb:** `← Westfield CC 2nd XI availability`

```
[← Westfield CC 2nd XI availability]          [Graham Okafor] · [2nd XI ▼]

Send match request to Westfield CC 2nd XI
──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────┐
│  FIXTURE DETAILS                                                         │
│  These are drawn from the availability you found. They cannot be        │
│  changed here.                                                           │
│                                                                          │
│  Date          Sunday 14 June 2026          (locked)                    │
│  Format        T20                          (locked)                    │
│  Your team     Thornton CC 2nd XI           (locked)                    │
│                                                                          │
│  ────────────────────────────────────────────────────────────────────   │
│                                                                          │
│  ADD A NOTE  (optional)                                                  │
│  ┌──────────────────────────────────────────────────────────────────┐   │
│  │                                                                  │   │
│  │  e.g. "We play a similar level and have a good outfield.         │   │
│  │  Happy to provide teas."                                         │   │
│  │                                                                  │   │
│  └──────────────────────────────────────────────────────────────────┘   │
│  0 / 200 characters                                                      │
│                                                                          │
│  ────────────────────────────────────────────────────────────────────   │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────┐   │
│  │  ⚠  FORMAT NOTE                                                  │   │
│  │  Westfield CC Sunday XI prefer Sunday format. You're requesting  │   │
│  │  T20. Both teams will need to confirm the format before the      │   │
│  │  match.                                                          │   │
│  └──────────────────────────────────────────────────────────────────┘   │
│  ☐  I understand and will confirm the format with Westfield CC           │
│                                                                          │
│  ────────────────────────────────────────────────────────────────────   │
│                                                                          │
│           [Cancel]                    [Send match request]               │
└──────────────────────────────────────────────────────────────────────────┘
```

**Specifications:**
- Locked fields: displayed as definition list (label / value), not form inputs
- Note textarea: C14, full width of form, min 120px height
- Compatibility notice (C06): amber-subtle background, amber-light left border, only shown when applicable
- Checkbox: styled checkbox, aria-required, links to label with `for`
- [Cancel]: Ghost button, left-aligned. Links back (does not send).
- [Send match request]: Primary button, right-aligned. Disabled until checkbox ticked (if notice present).

**Success confirmation (after submit):**

```
Match request sent.

We've notified Westfield CC 2nd XI's fixture manager.
They have 7 days to respond. You'll be notified when they do.

[Back to My fixtures]     [Find another game]
```

---

### 05-B Error: duplicate request for date

```
┌──────────────────────────────────────────────────────────────────────────┐
│ You already have a match request pending for 14 June.                    │
│ Your availability for this date is locked while that request is active.  │
│                                                                          │
│ [View your pending request →]                                            │
└──────────────────────────────────────────────────────────────────────────┘
```

This replaces the form. User cannot proceed. [View pending request] links to that fixture.

---

## Screen 06 — Match request detail (receiving team)

### 06-A Default state

**URL:** `/requests/[id]`  
**Breadcrumb:** `← Requests`

```
[← Requests]                                   [Priya Sharma] · [Ladies XI ▼]

Match request from Thornton CC 1st XI
Received 2 hours ago
──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────┐
│  REQUESTING TEAM                                                         │
│                                                                          │
│  Thornton CC 1st XI                                                      │
│  T20 · Women's · Open · Tier 3                                           │
│  Home ground: Thornton Park, Thornton (8 miles from your ground)         │
│                                                                          │
│  Trust badge: ● New  (joined platform this season)                       │
│                                                                          │
│  ────────────────────────────────────────────────────────────────────   │
│                                                                          │
│  FIXTURE DETAILS                                                         │
│                                                                          │
│  Date      Sunday 7 June 2026                                            │
│  Format    T20                                                           │
│  Venue     To be agreed — both teams have home grounds available         │
│                                                                          │
│  ────────────────────────────────────────────────────────────────────   │
│                                                                          │
│  NOTE FROM THORNTON CC                                                   │
│                                                                          │
│  "We're looking for a Sunday T20 to start our season. Similar level.    │
│  We can provide teas."                                                   │
│                                                                          │
│  ────────────────────────────────────────────────────────────────────   │
│                                                                          │
│  This request expires on 14 June 2026 (7 days from now).                │
│  Your availability for 7 June is reserved until you respond.             │
│                                                                          │
│                     [Decline]              [Accept]                      │
└──────────────────────────────────────────────────────────────────────────┘
```

**Specifications:**
- Trust badge: inline (C03), explanatory text in parentheses at 14px `--text-secondary`
- Expiry notice: `type-caption`, `--text-secondary`, above buttons
- Reservation notice: same treatment
- [Decline]: Ghost/secondary button. No reason required. On click: confirmation "Are you sure? Declining will release your availability for 7 June. [Confirm decline] [Go back]"
- [Accept]: Primary button. On click: C08 confirmation dialog (modal):
  - Title: "Accept match request"
  - Body: "Accepting creates a fixture on 7 June with Thornton CC 1st XI. Cancellations within 48 hours of the match affect your trust record."
  - Primary CTA: [Confirm — Accept] (Primary button)
  - Secondary: [Go back] (Ghost)
  - Initial focus: [Go back] (prevents accidental acceptance)

---

### 06-B Error: request expired or withdrawn

```
This match request is no longer active.

Thornton CC 1st XI withdrew their request on 8 June.
Your availability for 7 June is open again.

[Back to requests]
```

Read-only, no action buttons except back link.

---

## Screen 07 — Post availability

### 07-A Default state

**URL:** `/availability/post`  
**Breadcrumb:** `← Dashboard` or `← Search results` (context-dependent)  
**Page title:** "Post availability"

```
Post availability                              [Graham Okafor] · [2nd XI ▼]
──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  Date                                                                    │
│  ┌───────────────────────────┐                                           │
│  │  Select a date         ▼  │                                           │
│  └───────────────────────────┘                                           │
│                                                                          │
│  Format                                                                  │
│  ┌──────┐ ┌────────┐ ┌────────┐ ┌──────────────┐ ┌──────────────┐      │
│  │  T20 │ │ 40-ov  │ │ 50-ov  │ │ Timed decl.  │ │ Sunday XI    │      │
│  └──────┘ └────────┘ └────────┘ └──────────────┘ └──────────────┘      │
│                                                                          │
│  Venue preference                                                        │
│  ○ No preference   ● Home preferred   ○ Away preferred                  │
│                                                                          │
│  ▶ More options (distance, age group, gender)                            │
│                                                                          │
│                                 [Post availability]                      │
└──────────────────────────────────────────────────────────────────────────┘
```

**When navigated from empty search results, date and format are pre-filled from the search.**

**Success state:**

```
Availability posted for 14 June.

Other clubs searching for a T20 on or near 14 June will see your listing.
You'll be notified if someone sends a match request.

[Back to dashboard]    [Post another date]
```

---

## Screen 08 — Review form

### 08-A Default state

**URL:** `/review/[fixture-id]`  
**Breadcrumb:** `← [Fixture name]`

```
Leave a review for Westfield CC 2nd XI
Sunday 14 June 2026 · T20
──────────────────────────────────────────────────────────────────────────

Your review is private. It contributes to trust signals on the platform
but is never shown to other clubs in full.

────────────────────────────────────────────────────────────────

1.  Did the match take place as agreed?

    ○ Yes, everything as agreed
    ○ Minor changes (venue, time, format) but still played
    ○ No — they cancelled or didn't show

────────────────────────────────────────────────────────────────

2.  How would you describe the experience of organising this match?

    ○ Straightforward — good communication throughout
    ○ Some issues, but resolved
    ○ Difficult — slow or no communication

────────────────────────────────────────────────────────────────

3.  Would you play this club again?

    ○ Yes — would recommend
    ○ Possibly — with reservations
    ○ No

────────────────────────────────────────────────────────────────

[Submit review]    [Not now — remind me later]
```

**Specifications:**
- Exactly 3 questions. Exactly 3 options each. No open text. No optional questions.
- Questions: `type-lead` (20px, medium sans)
- Options: radio group (C13), vertical, full-width labels
- Privacy note: `type-caption`, `--text-secondary`, above question 1
- Horizontal rules: `--border-default`, `--space-6` margin
- [Submit review]: Primary. Disabled until all 3 answered.
- [Not now]: Ghost link. "Remind me in 3 days" functionality behind this.

---

## Screen 09 — Club onboarding (3-step)

### Step 1 of 3 — Club details

**URL:** `/onboarding/club`

```
Set up your club                               [Graham Okafor] · [New user]

Step 1 of 3 · Club details
──────────────────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────┐
│  Club name                                                               │
│  ┌──────────────────────────────────────────────────────────────────┐   │
│  │  e.g. Thornton Cricket Club                                      │   │
│  └──────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│  Home ground postcode                                                    │
│  ┌──────────────────────┐                                                │
│  │  e.g. GU14 8AB       │                                                │
│  └──────────────────────┘                                                │
│  Used to show distance to other clubs. Not publicly displayed.           │
│                                                                          │
│  County                                                                  │
│  ┌──────────────────────────────────────┐                                │
│  │  Select county                    ▼  │                                │
│  └──────────────────────────────────────┘                                │
│                                                                          │
│                                               [Next: Teams →]            │
└──────────────────────────────────────────────────────────────────────────┘
```

### Step 2 of 3 — Teams

Add team(s): team name dropdown (1st XI / 2nd XI / Sunday XI / Ladies XI / etc.) + gender + age group + tier estimate (optional).

[+ Add another team] ghost link to add more.

### Step 3 of 3 — Review and confirm

Summary of club + teams. Edit links inline. [Complete setup] primary button.

---

## Screen 10 — Notification preferences

**URL:** `/settings/notifications`  
**Breadcrumb:** `← Settings`

Simple table of notification types × delivery channels (Email / In-app):

| Notification | Email | In-app |
|---|---|---|
| New match request received | ✓ toggle | ✓ toggle |
| Match request accepted | ✓ toggle | ✓ toggle |
| Match request declined | ✓ toggle | ✓ toggle |
| Match request expired | ✓ toggle | ✓ toggle |
| Fixture confirmed | ✓ toggle | ✓ toggle |
| Fixture cancelled by other team | ✓ toggle | ✓ toggle |
| Review reminder | ✓ toggle | — |
| Platform announcements | ✓ toggle | — |

Toggle inputs: accessible toggle switches (not checkboxes). `role="switch"`, `aria-checked`.

Auto-saved on toggle. No "Save" button needed. Confirmation: brief "Saved" toast (bottom of screen, Forest background, white text, disappears after 3s).
