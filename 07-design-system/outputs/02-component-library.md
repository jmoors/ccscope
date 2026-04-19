# 02 — Component Library

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 7 (Design System & Screen Design)  
**Status:** MVP set — complete  
**Figma page:** Components (page 5 in Pavilion Design System.fig)

---

## Component inventory

| # | Component | Variants | States | Used in |
|---|-----------|----------|--------|---------|
| C01 | Button | Primary / Secondary / Ghost / Destructive / Link | Default / Hover / Active / Disabled / Loading | All screens |
| C02 | Fixture card | Standard / Compact | Per fixture status (7) | Dashboard, My fixtures |
| C03 | Trust badge | New / Reliable / Established | — | Search results, request detail, team profile |
| C04 | Status pill | 7 fixture statuses | — | Fixture card, fixture detail |
| C05 | What's missing panel | Desktop (column) / Mobile (banner) | Unresolved / Partially resolved / All confirmed | Fixture detail |
| C06 | Compatibility notice | Format / Age / Gender | — | Search result card, send match request |
| C07 | Nav badge | — | Count 0 (hidden) / Count 1–9 / Count 9+ | Sidebar nav, bottom tab bar |
| C08 | Confirmation dialog | Desktop (modal) / Mobile (bottom sheet) | — | Accept / cancel / block flows |
| C09 | Empty state block | Per screen (8 variants) | — | Dashboard, search results, fixture list |
| C10 | Skeleton loader | Card / Panel / Form | — | Any loading state |
| C11 | Form: Text input | Default / With label / With hint | Default / Focused / Error / Disabled / Filled | Forms |
| C12 | Form: Select | Desktop (styled) / Mobile (native) | Default / Focused / Error / Disabled | Search form, settings |
| C13 | Form: Radio group | Vertical / Horizontal | Default / Selected / Disabled | Search form |
| C14 | Form: Textarea | — | Default / Focused / Error / At limit | Send request note |
| C15 | Form: Toggle button | Single / Group | Unselected / Selected / Disabled | Format selector |
| C16 | Team context switcher | Desktop (dropdown) / Mobile (prominent tap target) | Default / Open | Global |
| C17 | Nav: Sidebar | — | Item default / Active / Hover | Desktop only |
| C18 | Nav: Bottom tab bar | — | Item default / Active | Mobile only |
| C19 | Notification bar | Offline / Attention | — | Mobile, desktop |

---

## C01 — Button

### Anatomy
```
[leading icon?] [label] [trailing icon?]
```

### Variants and specs

**Primary**
- Background: `--color-primary-forest` (#0e5c42)
- Text: `--color-neutral-white`
- Border: none
- Border-radius: `--radius-md` (6px)
- Padding: `--space-3` vertical (12px), `--space-5` horizontal (20px)
- Font: Source Sans 3, 16px, SemiBold, no letter-spacing
- Min height: 44px (tap target compliance)
- Min width: fit-content
- Hover: background `--interactive-primary-hover` (#0a4c37)
- Active: background `--interactive-primary-active` (#073d2c)
- Disabled: opacity 0.4, cursor not-allowed, no hover effect
- Focus: `--focus-ring` 3px offset

**Secondary**
- Background: transparent
- Text: `--color-primary-forest`
- Border: 1px solid `--color-neutral-stone`
- Border-radius: `--radius-md`
- Padding: same as Primary (adjusted for 1px border: 11px vertical)
- Hover: background `--surface-subtle`, border-color `--color-primary-forest`
- Focus: `--focus-ring` 3px offset

**Ghost / text link**
- Background: transparent
- Text: `--color-primary-forest`
- Border: none
- Underline: on hover only
- Padding: `--space-2` vertical, `--space-3` horizontal
- Min height: 44px
- Use: Decline, Cancel, Back, secondary actions

**Destructive**
- Background: `--color-error-text` (#b91c1c)
- Text: white
- Use: Confirm cancel, confirm block
- Same padding as Primary
- Always precede with a confirmation dialog — never direct action

**Full-width variant**
- `width: 100%`
- Used exclusively on mobile for all primary actions

### States

| State | Visual |
|---|---|
| Default | As above |
| Hover (pointer device) | Background lightened/darkened per variant |
| Active (press) | Darker than hover |
| Disabled | opacity: 0.4 — do not use greyscale colour swap |
| Loading | Replace label with spinner, aria-busy="true", prevent click |
| Focus-visible | 3px solid Forest, 3px offset |

### CSS class names
```css
.btn              /* base */
.btn--primary     /* primary variant */
.btn--secondary   /* secondary variant */
.btn--ghost       /* ghost/link variant */
.btn--destructive /* destructive variant */
.btn--full        /* full-width modifier */
.btn--sm          /* small: 36px height, 14px font */
```

---

## C02 — Fixture card

Used in: Dashboard upcoming fixtures, My fixtures list, My availability list.

### Anatomy
```
┌─────────────────────────────────────────────────────┐
│ [Date]                                [Status pill] │
│ [Fixture name / vs / availability summary]          │
│ [Format · Home/Away]                                │
│ [Secondary info / elapsed time]                     │
│ [Action links]                                      │
└─────────────────────────────────────────────────────┘
```

### Standard variant (dashboard)

- Width: ~560px desktop / 100% mobile
- Background: `--surface-base` (white)
- Border: 1px solid `--border-default`
- Border-radius: `--radius-md` (6px)
- Padding: `--space-4` (16px) all sides
- Shadow: none (shadow-sm on hover only — desktop)
- Entire card is a link (keyboard + mouse)

### Compact variant (list view)

- Reduced padding: `--space-3` (12px) all sides
- Status pill and date condensed to same line
- No action links (card itself is the link)

### State-specific content

| Status | Status pill | Secondary info | Actions |
|---|---|---|---|
| Awaiting opponent | Awaiting opponent | Published N days ago | [Edit] [Withdraw] |
| Awaiting response | Awaiting response | Sent to [team] · N days ago | [View] [Withdraw] |
| Awaiting venue | Awaiting venue | Opponent confirmed | [View →] |
| Awaiting officials | Awaiting officials | Venue confirmed | [View →] |
| Confirmed | Confirmed | Date + venue | [View →] |
| Completed | Completed | Date (past) | [View →] [Leave a review] |
| Cancelled | Cancelled | Cancelled reason if known | — |

### Loading (skeleton)

Replace card content with `<C10 Skeleton loader — Card>`.

---

## C03 — Trust badge

### Design constraint (from Agent 2 + Agent 6)
- Text labels required (New / Reliable / Established)
- Not stars, not percentage, not numeric
- Text is the primary differentiator — colour reinforces but never sole signal
- Must not compete with status pills for visual prominence
- Quiet but readable

### Anatomy
```
[indicator] [label]
```

The indicator is a simple geometric shape in the badge colour. Three distinct shapes:

- **New:** ○ open circle (empty inside — appropriate metaphor: just starting)
- **Reliable:** ◆ filled diamond (solid, established shape)
- **Established:** ◆◆ two filled diamonds (more of the same, not different)

### Specs

| Badge | Indicator | Label | Fill colour | Label colour | Contrast |
|---|---|---|---|---|---|
| New | ○ | New | — | `--color-trust-new` (#6e6e6a) on white | 5.1:1 AA ✓ |
| Reliable | ◆ | Reliable | `--color-trust-reliable` (#0e5c42) | white | 8.0:1 AAA ✓ |
| Established | ◆◆ | Established | `--color-trust-established` (#8a5c1a) | white | 5.5:1 AA ✓ |

### Layout modes

**Inline (within a card):**
- No background fill — indicator + text label in badge colour
- Font: Source Sans 3, 14px, Medium
- "New" uses outline circle (fill = transparent)

**Standalone pill:**
- Pill shape (`--radius-pill`), filled background
- Font: `type-badge` (12px, SemiBold, 0.08em tracking, uppercase)
- Padding: 4px 10px
- Used in: Search result card, match request detail

**Note on "New":** The standalone pill for "New" uses `--color-trust-new` as background with white text (5.1:1 ✓), unlike inline mode. This is intentional: when shown as a pill alongside Reliable and Established pills, it needs the same visual treatment.

### Copy note
Trust badge labels are title case, never all-caps in the display label. ALL-CAPS is only for the CSS badge class styling (`text-transform: uppercase`).

---

## C04 — Status pill

Used on fixture cards and fixture detail page.

### Hierarchy note (from CLAUDE.md)
Status pills are the **loudest** visual element after page headings. They convey the fixture's current state. Never let trust badges approach this level of prominence.

### Specs

All status pills:
- Shape: `--radius-pill` (9999px)
- Font: `type-badge` (12px, SemiBold, 0.08em tracking, uppercase)
- Padding: 4px 12px
- Border: 1px solid (see per-status)

| Status | Background | Text | Border | Semantic meaning |
|---|---|---|---|---|
| Awaiting opponent | `--surface-subtle` (#f7f6f4) | `--text-secondary` (#484844) | `--border-default` (#d5d5cf) | Neutral — waiting |
| Awaiting response | `--color-accent-amber-subtle` (#f5ead9) | `--color-accent-amber` (#8a5c1a) | `--color-accent-amber-light` (#c97d2e) | Attention — pending |
| Awaiting venue | `--color-accent-amber-subtle` | `--color-accent-amber` | `--color-accent-amber-light` | Attention — pending |
| Awaiting officials | `--color-accent-amber-subtle` | `--color-accent-amber` | `--color-accent-amber-light` | Attention — pending |
| Confirmed | `--color-primary-forest` (#0e5c42) | `--color-neutral-white` | none | Success |
| Completed | `--surface-subtle` | `--text-tertiary` (#6e6e6a) | `--border-default` | Neutral — archived |
| Cancelled | `--surface-subtle` | `--text-tertiary` | `--border-default` | Neutral — ended |

**Contrast check:**
- Amber (#8a5c1a) on amber-subtle (#f5ead9): 6.7:1 AA ✓
- White on Forest (#0e5c42): 8.0:1 AAA ✓
- Slate (#484844) on parchment (#f7f6f4): 8.2:1 AA ✓
- Dust (#6e6e6a) on parchment: 4.5:1 AA ✓ (just passes at this size due to font-weight boost)

---

## C05 — What's missing panel

### Desktop variant (right column, 240px)

```
┌──────────────────────┐
│ WHAT'S MISSING       │  ← label, type-label, text-tertiary
│                      │
│ ✗ Venue              │  ← unresolved item, text-primary
│   [Confirm venue →]  │  ← action link, Forest color
│                      │
│ ✓ Opponent           │  ← resolved item, text-tertiary
│ ✓ Officials n/a      │  ← deferred item, text-tertiary
│                      │
│ Once venue is        │  ← contextual helper text, caption
│ confirmed, this      │
│ fixture is           │
│ Confirmed.           │
└──────────────────────┘
```

- Background: `--surface-subtle` (#f7f6f4)
- Border: 1px solid `--border-default`
- Border-radius: `--radius-lg` (8px)
- Padding: `--space-4` (16px)
- Width: 240px
- Must be visible without scrolling at 1280px viewport

**ALL CONFIRMED state:**
- Background: tint of Forest at 6% opacity: rgba(14,92,66,0.06)
- Header: "ALL CONFIRMED ✓" in Forest
- All items show ✓, text-tertiary

### Mobile variant (top banner, full-width)

```
┌─────────────────────────────────────────┐
│ ⚠ WHAT'S MISSING                        │  ← amber accent
│                                         │
│ ✗ Venue   [Confirm venue]               │  ← full-width action
│ ✓ Opponent confirmed                    │
│ ✓ Officials n/a                         │
└─────────────────────────────────────────┘
```

- Background: `--color-accent-amber-subtle` (#f5ead9)
- Border-bottom: 2px solid `--color-accent-amber-light`
- No border-radius (spans full width)
- Padding: `--space-4` (16px) horizontal, `--space-3` (12px) vertical
- "⚠" icon: `--color-accent-amber` (#8a5c1a), aria-hidden="true"
- Text: `--text-primary`
- Action link: `--color-primary-forest`, underline on hover

**ALL CONFIRMED — mobile variant:**
- Background: rgba(14,92,66,0.06)
- Replace ⚠ with ✓ icon in Forest
- Header: "ALL CONFIRMED"

### Item states

| Item | Icon | Text treatment |
|---|---|---|
| Unresolved | ✗ (red, aria-label="Not yet confirmed:") | Bold, text-primary |
| Resolved | ✓ (green, aria-label="Confirmed:") | Normal, text-tertiary |
| Deferred (n/a) | ✓ (green) | Normal, text-tertiary, appended "(n/a)" or "(friendly)" |

**Accessibility:** The ✗ and ✓ icons must not rely on colour alone. Use `aria-label` on each item's icon to convey meaning to screen readers. The item text is always present.

---

## C06 — Compatibility notice

Used on search result cards and Send match request screen.

**Purpose:** Informational, not an error. Must not alarm. Resolves ambiguity before it becomes a problem.

### Anatomy
```
⚠ [Notice type]: [Explanation text]
```

### Specs

- Icon: ⚠ in `--color-accent-amber` (#8a5c1a), `aria-label="Compatibility note:"`
- Background: `--color-accent-amber-subtle` (#f5ead9) — on Send request screen only; inline on cards
- Border-left: 3px solid `--color-accent-amber-light` — on Send request screen only
- Text: `--text-primary`, 14px, Regular
- Padding: `--space-2` (8px) `--space-3` (12px) — on Send request screen

### Variants

| Type | Label | Example text |
|---|---|---|
| Format | Format note | "Sunday XI. Playing T20 by agreement." |
| Tier | Tier note | "They play at a higher tier (Tier 4 vs Tier 3)." |
| Age group | Age group | "This team has an age restriction." |
| Gender | Gender | "This team's gender category differs from your search." |

### On Send request screen with acknowledgement checkbox

When a compatibility notice is present on the Send match request form:
- Display the notice as a highlighted block (left border + amber-subtle background)
- Add a required checkbox: "I understand and will confirm the details with the other team"
- Form cannot be submitted without checkbox ticked
- Error if submitted without: "Please confirm you've read the format note."

---

## C07 — Nav badge (notification count)

Used on: Requests nav item, Notifications nav item.

### Specs

- Shape: `--radius-pill`
- Background: `--color-primary-forest`
- Text: white, `type-badge`, 11px
- Min width: 18px, height: 18px
- Padding: 0 4px
- Position: top-right of nav icon, offset -4px -4px from icon corner
- Visibility: hidden when count = 0 (do not show "0")
- Content: count number; when > 9, show "9+"
- Aria: `aria-label="[N] unread notifications"` on the parent nav item

---

## C08 — Confirmation dialog

### Desktop: Modal dialog

```
┌────────────────────────────────────┐
│  [Title]                           │  ← serif, H3
│                                    │
│  [Body text]                       │  ← body, text-primary
│                                    │
│  [Secondary action]  [Primary CTA] │
└────────────────────────────────────┘
```

- Max-width: 480px
- Background: white
- Border-radius: `--radius-lg` (8px)
- Padding: `--space-8` (32px)
- Shadow: `--shadow-md`
- Backdrop: rgba(26,26,24,0.4)
- Never auto-dismiss — requires explicit action
- Focus trap: keyboard focus cycles within dialog
- Initial focus: primary CTA button
- Close on Escape: only for non-destructive dialogs
- aria-modal="true", role="dialog", aria-labelledby pointing to title

**For destructive actions (Cancel fixture, Block club):**
- Primary button: Destructive variant (red)
- Initial focus: Secondary action ("Go back") — prevents accidental confirm
- No close-on-Escape

### Mobile: Bottom sheet

```
┌─────────────────────────────┐   ← handle bar at top: 4px × 36px, Stone
│                             │
│  [Title]                    │
│  [Body text]                │
│                             │
│  [Primary CTA — full width] │
│  [Secondary action]         │
└─────────────────────────────┘
```

- Slides up from bottom
- Border-radius: `--radius-lg` top-left and top-right only
- Background: white
- Shadow: `--shadow-md` upward
- Max height: 80vh, overflow-y: auto
- Backdrop: rgba(26,26,24,0.4)
- Swipe-down to dismiss (non-destructive only)

---

## C09 — Empty state block

### Design principle
The empty state is not a fallback. For many new users it is the primary experience. Each screen's empty state is unique — no generic "Nothing here" fallback.

### Anatomy
```
[Heading]
[Body copy — 1-2 sentences]
[Primary CTA]
[Secondary CTA — optional]
[Supporting content — optional, e.g., "How it works"]
```

### Per-screen specs

**Dashboard empty:**
- Heading (H3, serif): "Your fixture list is empty."
- Body: "Start by searching for available teams, or post your own availability so other clubs can find you."
- CTA 1: [Find a game] — Primary button
- CTA 2: [Post availability] — Secondary button
- Below divider: "How it works" — 4-step plain list, body size
- Background: white (not parchment — avoid making empty feel like an error)

**Search results empty:**
- No standalone heading — inline in page with search params visible at top
- Body: "No availability found for [date] within [distance]."
- Suggestions block (bordered, parchment background):
  - Dynamic — only show options that actually apply to this search
  - [Widen to [suggested distance]] [Try this →]
  - [Try a different date] [Adjust dates →]
  - [Include away games] [Change →]
- Below divider: "Or post your availability for this date." [Post availability for [date]]
- The Post availability CTA pre-fills date and format from failed search

**My fixtures empty:**
- Heading: "No fixtures yet."
- Body: "When you accept or send a match request, your fixtures appear here."
- CTA: [Find a game] — Primary button

**My availability empty:**
- Heading: "No availability posted."
- Body: "You can post availability when no teams come up in your search — or any time you want to be found."
- CTA: [Post availability] — Primary button

**Requests empty:**
- Heading: "No requests at the moment."
- Body: "Match requests from other clubs will appear here."
- No CTA

**Notifications empty:**
- Heading: "No notifications."
- Body: "You'll be notified when a team responds to your request or sends you one."

### Sizing and placement
- Empty state block: max-width 520px, horizontally centred in content area
- Vertical position: ~25% from top of content area (not dead-centre — reads as loading mid-page)
- Desktop: white background card with `--border-default` border and `--radius-lg`
- Mobile: no card border — flows in content area

---

## C10 — Skeleton loader

### Design principle
Skeleton shapes match the layout of the content they represent. Content-shaped loading prevents layout shift when content arrives.

### Pulse animation

```css
@keyframes skeleton-pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.4; }
}

.skeleton {
  background-color: var(--color-neutral-stone);
  border-radius: var(--radius-sm);
  animation: skeleton-pulse 1.5s ease-in-out infinite;
}
```

No spinner. No "Loading..." text. Pulsing grey shapes only.

### Skeleton: Card

Matches fixture card height and internal structure.

```
┌─────────────────────────────────────────────────────┐
│ [████████████]           [████████]                 │  ← date + status pill shape
│ [████████████████████]                              │  ← fixture name shape
│ [████████████]                                      │  ← format/detail shape
└─────────────────────────────────────────────────────┘
```

- 3 rows of skeleton bars: width 35% / 65% / 40%
- Heights: 14px / 20px / 14px
- Row gap: 8px
- Card height: ~80px (matches filled card)
- Appears after 200ms delay (prevents flash for fast loads)

### Skeleton: Panel

Used for "What's missing" panel placeholder.

### Skeleton: Form

Used for search form loading (e.g., if user preferences load async).

### Aria
```html
<div aria-busy="true" aria-label="Loading fixture list">
  <!-- skeleton items -->
</div>
```

---

## C11 — Form: Text input

```
[Label]           ← type-label, text-primary
[Hint text]       ← type-caption, text-tertiary (optional)
┌───────────────────────────┐
│ [Value or placeholder]    │
└───────────────────────────┘
[Error message]   ← type-caption, error-text, with ✗ icon (error state only)
```

### Specs

- Height: 44px min (tap target)
- Border: 1px solid `--border-default`
- Border-radius: `--radius-md` (6px)
- Background: white
- Text: `--text-primary`, 16px (never below 16px on mobile — prevents iOS zoom)
- Placeholder: `--text-tertiary`, 16px — never a sentence, never "Type here"
- Padding: 0 `--space-3` (12px) horizontal

**States:**

| State | Border | Background | Notes |
|---|---|---|---|
| Default | `--border-default` | white | — |
| Focused | `--border-focus` (Forest, 2px) | white | Plus focus ring on outer element |
| Filled | `--border-default` | white | — |
| Error | `--border-error` (2px) | `--surface-error` | Error message below |
| Disabled | `--border-default` (opacity 0.5) | `--surface-subtle` | cursor: not-allowed |

---

## C12 — Form: Select

**Desktop:** Styled dropdown replacing native `<select>`. Must be fully keyboard-navigable (arrow keys, enter, escape). Uses `role="listbox"` / `role="option"`.

**Mobile:** Native `<select>` element. OS-native picker is accessible and familiar. Custom styling limited to the trigger appearance.

Trigger specs match C11 text input. Add a chevron icon (▼) right-aligned.

---

## C13 — Form: Radio group

Used for Home/away preference on search form.

- Each radio + label: min 44px touch target (extend clickable area via padding)
- Label: 16px, text-primary
- Selected: Forest-coloured radio dot, Forest border
- Gap between options: `--space-2` (8px) vertical, `--space-6` (24px) horizontal
- **Desktop:** Horizontal layout (3 options side by side)
- **Mobile:** Vertical stack (prevents cramping on 375px)

---

## C14 — Form: Textarea

Used for match request note.

- Min height: 120px
- Resize: vertical only
- Character counter: right-aligned below field, `type-caption`, `--text-tertiary`
  - At limit: counter turns `--text-error`
  - Near limit (< 20 chars remaining): counter turns `--color-accent-amber`
- All other specs: same as text input (C11)

---

## C15 — Form: Toggle button (format selector)

Used to select game format on search form.

### Anatomy
```
┌─────────┐
│  T20    │   unselected: white bg, Stone border, Ink text
│   ●     │   selected: Forest bg, white text, no border
└─────────┘
```

**Desktop:** 5 buttons in a horizontal row (flex, gap `--space-2`)
- Min width: 80px each
- Height: 44px

**Mobile:** 2-row grid (3+2 layout)
- Full available width
- Height: 44px per button
- Grid: `repeat(3, 1fr)` first row, `repeat(2, 1fr)` second row

**States:**

| State | Background | Text | Border |
|---|---|---|---|
| Unselected | white | `--text-primary` | `--border-default` |
| Hovered | `--surface-subtle` | `--text-primary` | `--color-primary-forest` |
| Selected | `--color-primary-forest` | white | none |
| Disabled | `--surface-subtle` (opacity 0.5) | `--text-tertiary` | `--border-default` |

**Accessibility:** Use `role="group"` + `aria-label="Format"` on the container. Each button is a `<button type="button">` with `aria-pressed="true/false"`.

---

## C16 — Team context switcher

The team context switcher is always visible and prominent. It communicates which team the user is acting as.

### Desktop variant

Position: top-right of page header, beside user name.

```
[Thornton CC] · [2nd XI ▼]
```

- Club name: `--text-secondary`, `type-label`
- Team name + chevron: `--text-primary`, `type-label`, medium weight
- Dropdown on click — lists all teams associated with this user's account
- Selected team has Forest-colour check mark ✓ in list

### Mobile variant

Position: top of content area, below any top bar.

```
┌──────────────────────────────┐
│  Thornton CC · 2nd XI  ▼    │  ← full-width tappable row
└──────────────────────────────┘
```

- Full-width tappable area, 44px height minimum
- Background: `--surface-subtle`
- Border-bottom: 1px solid `--border-default`
- Text: `--text-primary`, `type-label`
- Chevron: `--text-tertiary`
- Opens an action sheet (OS native style or C08 bottom sheet) listing available teams

---

## C17 — Nav: Sidebar (desktop)

```
┌────────────────────────────┐
│                            │
│  [PAVILION wordmark]       │  ← top, 40px height
│  ─────────────────────     │  ← divider
│                            │
│  ● Dashboard               │  ← active item
│  ○ Find a game             │  ← default item
│  ○ My fixtures             │
│  ○ Requests     [1]        │  ← with nav badge
│  ○ Notifications [3]       │  ← with nav badge
│                            │
│  ─────────────────────     │  ← divider, pushes to bottom
│                            │
│  ○ Club                    │  ← secondary items
│  ○ Settings                │
│                            │
└────────────────────────────┘
```

- Width: 240px, fixed
- Background: `--surface-base` (white)
- Border-right: 1px solid `--border-default`
- Padding: `--space-4` (16px) horizontal, `--space-6` (24px) top
- Item height: 44px (tap target, even on desktop)
- Item padding: `--space-2` (8px) vertical, `--space-3` (12px) horizontal
- Item border-radius: `--radius-md` (6px)

**Active item:**
- Background: rgba(14,92,66,0.08) (Forest 8% opacity tint)
- Text: `--color-primary-forest`
- Font weight: Medium (500)
- No border or left-border indicator (avoid hockey-stick design debt)

**Hover item:**
- Background: `--surface-subtle`

**Nav icon:** 20×20px, line icon, `--text-tertiary` (default) / `--text-brand` (active)

---

## C18 — Nav: Bottom tab bar (mobile)

```
┌──────────────────────────────────────────┐
│  [Home]  [Find]  [Fixtures]  [Req.] [🔔] │
└──────────────────────────────────────────┘
```

- Height: 56px + safe area inset (handles devices with home indicator)
- Background: white
- Border-top: 1px solid `--border-default`
- Always visible — does NOT hide on scroll
- 5 items, equal width
- Each item: icon (24px) + label (10px, Source Sans 3 Medium)
- Active item: Forest icon + label
- Inactive: Dust icon + label
- Badge on Requests + Notifications: see C07
- `aria-label` on nav element: "Main navigation"
- Active item: `aria-current="page"`

**Labels:**
- Home
- Find a game
- Fixtures
- Requests
- Notifications

---

## C19 — Notification bar

A system-level bar for non-screen-specific alerts. Not the same as screen-level error states.

### Offline bar (mobile)
- Position: top of screen, full width, below OS status bar
- Background: `--color-neutral-slate`
- Text: white, `type-caption`, centred
- "No internet connection. Showing last saved data."

### Attention bar (global)
- Background: `--color-accent-amber-subtle`
- Text: `--text-primary`
- Used for: account warnings, club profile incomplete notices
- Dismiss button (✕) on right — `aria-label="Dismiss"`
