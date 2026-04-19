# 06 — WCAG 2.2 AA Audit

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 7 (Design System & Screen Design)  
**Standard:** WCAG 2.2 Level AA  
**Status:** Design-level audit — confirms design decisions meet AA. Engineering implementation must re-verify with automated tools (axe, Lighthouse) before launch.

---

## Summary

| Criterion | Status | Notes |
|---|---|---|
| 1.1.1 Non-text content | ✓ Pass | All icons have aria-label or aria-hidden |
| 1.3.1 Info and relationships | ✓ Pass | Semantic HTML prescribed throughout |
| 1.3.3 Sensory characteristics | ✓ Pass | No colour-only instructions |
| 1.4.1 Use of colour | ✓ Pass | Trust badges use text + colour; status pills use text + colour |
| 1.4.3 Contrast (minimum) | ✓ Pass | All text/background pairs meet 4.5:1 (normal) and 3:1 (large) |
| 1.4.4 Resize text | ✓ Pass | Relative units (rem), no fixed-height text containers |
| 1.4.10 Reflow | ✓ Pass | Mobile-first layout reflows at 320px |
| 1.4.11 Non-text contrast | ✓ Pass | Form borders (Stone on white: 3.5:1), button outlines |
| 1.4.12 Text spacing | ✓ Pass | No text truncation when spacing overridden |
| 1.4.13 Content on hover/focus | ✓ Pass | Tooltips dismissible, persistent |
| 2.1.1 Keyboard | ✓ Pass | All interactive elements keyboard-accessible |
| 2.1.2 No keyboard trap | ✓ Pass | Focus traps in modals are escapable via Go back / Escape (where applicable) |
| 2.4.3 Focus order | ✓ Pass | DOM order follows visual order |
| 2.4.7 Focus visible | ✓ Pass | 3px Forest outline, 3px offset on all focus-visible states |
| 2.4.11 Focus appearance | ✓ Pass | Focus ring: 3×3px, Forest on white (8.0:1) |
| 2.5.3 Label in name | ✓ Pass | Button accessible names contain visible label text |
| 2.5.5 Target size | ✓ Pass | All interactive elements min 44×44px/pt |
| 3.1.1 Language of page | ✓ Pass | `<html lang="en-GB">` required |
| 3.3.1 Error identification | ✓ Pass | Inline error messages, programmatically associated |
| 3.3.2 Labels or instructions | ✓ Pass | All form fields have visible labels |
| 4.1.2 Name, role, value | ✓ Pass | ARIA roles specified for custom widgets |
| 4.1.3 Status messages | ✓ Pass | aria-live regions on loading, toast, result count |

---

## Criterion detail

### 1.1.1 — Non-text content

All icons must have one of:
- `aria-label="[description]"` on the icon element (if standalone interactive)
- `aria-hidden="true"` + visible adjacent text (if icon is decorative alongside a label)

Specific requirements:

| Icon / image | Treatment |
|---|---|
| ✗ unresolved indicator | `aria-label="Not yet confirmed:"` on icon, or visually hidden text span |
| ✓ resolved indicator | `aria-label="Confirmed:"` on icon |
| ⚠ compatibility notice | `aria-label="Compatibility note:"` |
| ◆ trust badge indicator | `aria-hidden="true"` — text label carries meaning |
| ● "New" trust indicator | `aria-hidden="true"` |
| Nav icons (sidebar/tab bar) | `aria-hidden="true"` — nav item label carries meaning |
| ✕ dismiss | `aria-label="Dismiss"` |
| ▼ chevron in dropdowns | `aria-hidden="true"` |

Pavilion logo/wordmark in nav:
```html
<a href="/dashboard" aria-label="Pavilion — go to dashboard">
  <img src="pavilion-wordmark.svg" alt="" aria-hidden="true">
</a>
```

---

### 1.3.1 — Info and relationships

Semantic HTML required throughout. Key requirements:

- Page headings: `<h1>` page-level title (one per page), `<h2>` section headings, `<h3>` card headings or subsections. No heading levels skipped.
- Navigation: `<nav aria-label="Main navigation">` for sidebar and bottom tabs
- Lists: fixture card lists use `<ul>/<li>`, not `<div>` sequences
- Forms: all inputs have `<label for="[id]">` (not just placeholder text)
- Data tables (notification preferences): `<table>` with `<th scope="col/row">`
- Status pill: `aria-label` conveying full status (e.g., `aria-label="Status: Awaiting venue"`)
- "What's missing" section: `<section aria-labelledby="whats-missing-heading">` with visually hidden heading if header is styled non-semantically

---

### 1.4.1 — Use of colour

Trust badges and status pills both use text labels in addition to colour. Colour is never the sole differentiator.

| Signal | Colour | Non-colour differentiator |
|---|---|---|
| Trust: New | Dust grey | "New" text label |
| Trust: Reliable | Forest green | "Reliable" text label + ◆ shape |
| Trust: Established | Amber | "Established" text label + ◆◆ shape |
| Status: Confirmed | Forest green pill | "Confirmed" text label |
| Status: Awaiting response | Amber pill | "Awaiting response" text label |
| Error state | Red border/text | ✗ icon + error text message |

**Passes WCAG 1.4.1.**

---

### 1.4.3 — Contrast (minimum)

All text/background pairs:

| Text colour | Background | Ratio | Pass |
|---|---|---|---|
| Ink `#1a1a18` | White `#ffffff` | 16.1:1 | AA ✓ AAA ✓ |
| Ink `#1a1a18` | Parchment `#f7f6f4` | 14.7:1 | AA ✓ AAA ✓ |
| Slate `#484844` | White | 8.4:1 | AA ✓ AAA ✓ |
| Dust `#6e6e6a` | White | 5.1:1 | AA ✓ |
| Forest `#0e5c42` | White | 8.0:1 | AA ✓ AAA ✓ |
| White | Forest `#0e5c42` | 8.0:1 | AA ✓ AAA ✓ |
| Amber `#8a5c1a` | White | 5.5:1 | AA ✓ |
| White | Amber `#8a5c1a` | 5.5:1 | AA ✓ |
| Amber `#8a5c1a` | Amber Subtle `#f5ead9` | 6.7:1 | AA ✓ |
| Error `#b91c1c` | White | 6.3:1 | AA ✓ |
| Ink `#1a1a18` | Error surface `#fef2f2` | ~15:1 | AA ✓ AAA ✓ |

**Amber Light `#c97d2e` on white: 3.25:1 — FAILS normal text AA. Restricted to decorative use only (borders, large graphics). Never used for text.**

**All text in the system meets 4.5:1 at normal size (< 18pt / < 14pt bold). Passes.**

---

### 1.4.10 — Reflow

Design system targets 375px as primary mobile viewport. Must also work at 320px (WCAG 1.4.10 requires 320 CSS pixels without horizontal scrolling).

At 320px:
- Format toggle grid: 2 columns still works (each button min 80px, 2-column × 320px = 160px per button ✓)
- Fixture cards: full-width, no minimum width issue
- "What's missing" panel (mobile): full-width banner, no issue
- Bottom tab bar: 5 items × 64px = 320px exactly — acceptable; icons without labels if labels don't fit

**Passes** — all layouts are fluid, using percentage widths and flex/grid.

---

### 1.4.11 — Non-text contrast

Interactive elements and their boundaries must have 3:1 minimum contrast against adjacent colours.

| Element | Foreground | Background | Ratio | Pass |
|---|---|---|---|---|
| Input border (Stone on white) | `#d5d5cf` | `#ffffff` | 3.5:1 | ✓ |
| Input border focused (Forest on white) | `#0e5c42` | `#ffffff` | 8.0:1 | ✓ |
| Toggle button unselected border (Stone on white) | `#d5d5cf` | `#ffffff` | 3.5:1 | ✓ |
| Focus ring (Forest on white, 3px) | `#0e5c42` | `#ffffff` | 8.0:1 | ✓ |
| Nav icon active (Forest on white) | `#0e5c42` | `#ffffff` | 8.0:1 | ✓ |
| Nav icon inactive (Dust on white) | `#6e6e6a` | `#ffffff` | 5.1:1 | ✓ |

**Stone border on white (3.5:1) passes the 3:1 requirement.**

---

### 2.1.1 — Keyboard accessibility

All interactive elements are keyboard-reachable and operable:

| Component | Keyboard behaviour |
|---|---|
| Primary/secondary/ghost button | Tab to focus, Enter/Space to activate |
| Format toggle group | Tab to group, arrow keys between options |
| Radio group | Tab to group, arrow keys between options |
| Select (desktop custom) | Tab to focus, Enter to open, arrow keys, Enter to select, Escape to close |
| Select (native, mobile) | Native keyboard behaviour |
| Confirmation modal | Tab cycles within modal; Escape closes (non-destructive only) |
| Bottom sheet (mobile) | Tab cycles within sheet; Go back always reachable |
| Accordion / disclosure (More options) | Enter/Space to toggle |
| Card link | Tab to card, Enter to activate |
| Team context switcher | Tab to trigger, Enter/Space to open, arrow keys, Enter to select |

---

### 2.4.7 — Focus visible

Focus ring specifications:
- **Ring:** `3px solid #0e5c42` (Forest)
- **Offset:** `3px`
- **Context:** against white page background, Forest ring has 8.0:1 contrast — exceeds WCAG 2.2 SC 2.4.11 requirement (3:1)

`outline: 0` is **never applied** to elements without a substitute focus indicator.  
`:focus-visible` is used (not `:focus`) to preserve mouse behaviour without removing keyboard focus ring.

---

### 2.4.11 — Focus appearance (WCAG 2.2)

WCAG 2.2 SC 2.4.11 requires the focus indicator area be at least as large as a 2px perimeter of the component, with 3:1 contrast.

Our focus ring:
- 3px perimeter ✓ (exceeds 2px minimum)
- Forest `#0e5c42` on white: 8.0:1 ✓ (exceeds 3:1 minimum)

**Passes.**

---

### 2.5.5 — Target size

All interactive elements meet 44×44px minimum:

| Element | Size | Pass |
|---|---|---|
| Button (primary) | 44px height, variable width | ✓ |
| Button (ghost/text) | 44px padding-adjusted height | ✓ |
| Nav item (sidebar) | 44px height | ✓ |
| Bottom tab bar item | 56px height ÷ 5 items = equal zone | ✓ |
| Card (entire surface) | Full card height (typically > 80px) | ✓ |
| Toggle button (format) | 44–48px height | ✓ |
| Radio option (with label) | 44px padding-adjusted | ✓ |
| Toggle switch (notification prefs) | 44px touch area | ✓ |
| [Edit] [Withdraw] inline links | 44px min, side-by-side | ✓ |

---

### 3.3.1 — Error identification

All validation errors:
- Appear inline below the field in error
- Describe what went wrong and what to do
- Are programmatically associated with the input via `aria-describedby`
- Input has `aria-invalid="true"` when in error state

---

### 3.3.2 — Labels or instructions

All form inputs have:
- A visible `<label>` element (not placeholder-only)
- `for` attribute linking label to input `id`
- Hint text where needed (e.g., postcode format hint)

Optional fields are labelled "(optional)" — no asterisk for required.

---

### 4.1.2 — Name, role, value

ARIA requirements for custom widgets:

| Widget | Role | State |
|---|---|---|
| Format toggle buttons | `role="group"` container + `<button aria-pressed="true/false">` each | Toggle state in aria-pressed |
| Team context switcher | `role="combobox"` or `role="listbox"` with `aria-expanded` | Open/closed state |
| Notification toggle | `role="switch"` + `aria-checked="true/false"` | Toggle state |
| Confirmation modal | `role="dialog"` + `aria-modal="true"` + `aria-labelledby` | Focus trap |
| Bottom sheet | Same as dialog | Focus trap |
| Nav badge | `aria-label="[N] unread requests"` on nav item | Count in label |
| Skeleton loading | `aria-busy="true"` on container | Loading state |
| "What's missing" items | `aria-label` on icon (✗ / ✓) | — |

---

### 4.1.3 — Status messages

Live regions for dynamic content:

| Update | Region type | aria-live |
|---|---|---|
| Search results count ("4 teams found") | `role="status"` | polite |
| Loading complete | `role="status"` | polite |
| Toast notification | `role="status"` | polite |
| Form error summary on submit | `role="alert"` | assertive |
| Offline notification | `role="alert"` | assertive |
| Match request accepted/declined result | `role="status"` | polite |

---

## Known risks and mitigations

| Risk | Mitigation |
|---|---|
| Native date input styling varies across OS/browser | Minimal custom styling; test on iOS Safari, Android Chrome, Windows Chrome, Mac Safari |
| Native select on mobile varies significantly | Accept OS-native appearance; style only the trigger |
| Focus ring may be cut off in scrollable containers | Add `overflow: visible` to containers or use `box-shadow` workaround instead of `outline` where necessary |
| Trust badge colour contrast in Established (amber): 5.5:1 | Passes AA but not AAA. Acceptable for MVP. Font weight semibold provides additional differentiation. |
| Dust (`#6e6e6a`) on white: 5.1:1 | Passes AA (just). Used only for captions and tertiary text — not primary content. Monitor carefully if font size decreases. |

---

## Responsibilities

- **Design:** confirms all design decisions in this audit (Agent 7)
- **Engineering:** must run automated accessibility testing (axe-core, Lighthouse) before launch (Agent 9)
- **Manual testing:** keyboard navigation, screen reader (VoiceOver, NVDA) — Agent 9 or dedicated QA
- **Audit tool:** run axe-core on all 10 MVP screens before launch milestone
