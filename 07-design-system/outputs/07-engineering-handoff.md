# 07 — Engineering Handoff

**Version:** 1.0  
**Date:** 2026-04-19  
**From:** Agent 7 (Design System & Screen Design)  
**To:** Agent 9 (Engineering)  
**Status:** Pre-usability-test — token system and component library stable; screen designs may update after usability testing

---

## Overview

This document is the primary handoff from design to engineering for the Pavilion MVP. Read it alongside the other outputs in `07-design-system/outputs/`.

### What is stable now

- Design token system (`01-token-implementation.css`) — implement this immediately
- Component library specifications (`02-component-library.md`) — all 19 components with variants and states
- WCAG 2.2 AA audit (`06-wcag-audit.md`) — accessibility requirements for all components
- Pattern documentation (`05-patterns.md`) — empty states, loading, errors, forms, confirmation flows

### What may update

- Screen designs (`03-screen-designs-desktop.md`, `04-screen-designs-mobile.md`) — structural layout is solid; copy and some interaction details may refine after Agent 6 usability testing completes
- Copy throughout — all copy is placeholder; Agent 8 finalises all user-facing strings

---

## Design system file structure

```
07-design-system/outputs/
├── 01-token-implementation.css     ← CSS custom properties. Source of truth for all tokens.
├── 02-component-library.md         ← Component specs (19 components, all variants and states)
├── 03-screen-designs-desktop.md    ← All 10 MVP screens, desktop, all states
├── 04-screen-designs-mobile.md     ← All 10 MVP screens, mobile, all states
├── 05-patterns.md                  ← Patterns: empty, loading, error, forms, confirmation
├── 06-wcag-audit.md                ← WCAG 2.2 AA design-level audit
└── 07-engineering-handoff.md       ← This document
```

**Source tokens** (from Agent 5): `05-brand-identity/outputs/08-design-tokens.json`  
`01-token-implementation.css` is the CSS implementation of those tokens. Do not modify token values without Agent 5 sign-off.

---

## Implementation checklist

### Phase 1 — Foundation (before any screens)

- [ ] Import `01-token-implementation.css` as first stylesheet
- [ ] Confirm Google Fonts: Source Serif 4 + Source Sans 3 loaded (variable font versions)
- [ ] `<html lang="en-GB">` on root
- [ ] Global `box-sizing: border-box`
- [ ] Global `font-size: 16px` base
- [ ] Focus-visible polyfill confirmed (if targeting older browsers)
- [ ] Run axe-core on blank page template

### Phase 2 — Component library

Build components in this priority order (most used → least used):

1. Button (C01) — all variants
2. Fixture card (C02) — Standard and Compact
3. Status pill (C04)
4. Trust badge (C03)
5. Skeleton loader (C10)
6. Form fields: text input (C11), select (C12), radio (C13), textarea (C14), toggle button (C15)
7. Empty state block (C09) — all 6 per-screen variants
8. Nav: Sidebar (C17) + Bottom tab bar (C18)
9. Team context switcher (C16)
10. "What's missing" panel (C05) — desktop + mobile variants
11. Compatibility notice (C06)
12. Nav badge (C07)
13. Confirmation dialog / bottom sheet (C08)
14. Notification bar (C19)

### Phase 3 — Screens

Priority order matches Agent 6 guidance:

**P1 (implement first):**
1. Dashboard — all states
2. Find a game
3. Search results — all states
4. Fixture detail — all states

**P2:**
5. Match request detail
6. Send match request
7. Post availability

**P3:**
8. Review form
9. Club onboarding (3-step)
10. Notification preferences

---

## Typography implementation

### Font loading

```html
<!-- In <head> — preconnect + preload for critical weights -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Use variable font for performance -->
<link href="https://fonts.googleapis.com/css2?family=Source+Serif+4:ital,opsz,wght@0,8..60,400..600;1,8..60,400..600&family=Source+Sans+3:wght@400..600&display=swap" rel="stylesheet">
```

Or self-host from Google Fonts download (preferred for privacy and performance).

### Type scale usage

```css
/* H1 — Page titles (used sparingly, only true top-level pages) */
/* H2 — Section headings within content */
/* H3 — Card titles, subsection headings */
/* Heading elements must not be used for visual styling — use CSS classes */

/* Correct: */
<h2 class="type-h2">Find a game</h2>

/* Incorrect: */
<p class="type-h2">Find a game</p>  /* — screen readers won't pick up heading structure */
```

---

## Colour implementation

Never use hex values directly in component code. Always reference tokens:

```css
/* Correct */
.fixture-card {
  border: 1px solid var(--border-default);
  background-color: var(--surface-base);
  color: var(--text-primary);
}

/* Incorrect */
.fixture-card {
  border: 1px solid #d5d5cf;
  background-color: #ffffff;
  color: #1a1a18;
}
```

Semantic aliases (e.g., `--text-primary`) are preferred over raw tokens (e.g., `--color-neutral-ink`) for component code. Raw tokens are acceptable in the token file itself.

---

## Spacing implementation

The spacing scale is the only source for margins, paddings, and gaps. Do not use arbitrary pixel values.

```css
/* Correct */
.card { padding: var(--space-4); }
.card-grid { gap: var(--space-3); }

/* Incorrect */
.card { padding: 15px; }   /* 15px is not in the scale */
```

---

## Focus states

**This is a hard requirement, not a nice-to-have.**

```css
/* Required on ALL interactive elements */
:focus-visible {
  outline: var(--focus-ring);          /* 3px solid #0e5c42 */
  outline-offset: var(--focus-ring-offset);  /* 3px */
}

/* Remove browser default only for non-keyboard focus */
:focus:not(:focus-visible) {
  outline: none;
}
```

Never set `outline: 0` or `outline: none` without a substitute.

---

## Touch target sizes

**All interactive elements: minimum 44×44px (CSS pixels).**

For small visual elements (text links, icon buttons), extend the tap target using padding or pseudo-elements:

```css
/* Example: ghost link that appears smaller visually */
.ghost-link {
  padding: var(--space-2) var(--space-3);  /* 8px 12px = extends tap area */
  min-height: 44px;
  display: inline-flex;
  align-items: center;
}
```

---

## Form field notes

### Date input

Use native `<input type="date">` on mobile — it triggers the OS date picker.

On desktop, the styled custom select (C12) with a date-aware dropdown is acceptable, but only if it passes keyboard navigation testing. If in doubt, use native `<input type="date">` on both platforms.

**Font size:** `font-size: 16px` minimum on ALL inputs — prevents iOS Safari auto-zoom on focus.

### Character counter (textarea)

```javascript
// Update character count on input
textarea.addEventListener('input', () => {
  const remaining = maxLength - textarea.value.length;
  counter.textContent = `${textarea.value.length} / ${maxLength} characters`;

  if (remaining <= 0) {
    counter.style.color = 'var(--color-error-text)';
    counter.textContent = '0 characters remaining';
  } else if (remaining <= 20) {
    counter.style.color = 'var(--color-accent-amber)';
  } else {
    counter.style.color = 'var(--text-tertiary)';
  }
});
```

---

## Confirmation dialogs

### Focus management

On dialog open:
1. Move focus to the dialog container
2. For non-destructive: focus first interactive element (usually the CTA)
3. **For destructive dialogs:** focus the secondary action ("Go back") — this prevents accidental confirm on fast keyboard users

On dialog close:
1. Return focus to the element that opened the dialog

```javascript
// On open
dialog.focus();  // or firstSecondaryButton.focus() for destructive

// On close (store trigger element reference before opening)
triggerElement.focus();
```

### Focus trap

While a modal/bottom sheet is open, Tab and Shift+Tab must cycle within the dialog only.

```javascript
// Focus trap implementation — cycle within dialog
dialog.addEventListener('keydown', (e) => {
  if (e.key !== 'Tab') return;
  const focusable = dialog.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  const first = focusable[0];
  const last = focusable[focusable.length - 1];

  if (e.shiftKey && document.activeElement === first) {
    e.preventDefault();
    last.focus();
  } else if (!e.shiftKey && document.activeElement === last) {
    e.preventDefault();
    first.focus();
  }
});
```

---

## Loading state timing

- Skeleton appears after 200ms CSS delay (avoids flash on fast loads)
- Transition from loading to error state after 10 seconds
- Use aria-live="polite" to announce when content loads

```css
.skeleton-container {
  transition-delay: 200ms;
}
```

---

## Offline handling (mobile)

```javascript
window.addEventListener('online', handleOnline);
window.addEventListener('offline', handleOffline);

function handleOffline() {
  offlineBar.hidden = false;
  // Disable all interactive elements except read-only views
  document.querySelectorAll('button, a[href], input, select')
    .forEach(el => el.setAttribute('disabled', ''));
}

function handleOnline() {
  offlineBar.hidden = true;
  // Re-enable interactivity
  // Trigger data refresh
}
```

Queue review drafts in localStorage; submit on reconnect.

---

## Component state matrix

Every component must handle every state. The full matrix:

| Component | Default | Hover | Focus | Active | Disabled | Loading | Error | Empty |
|---|---|---|---|---|---|---|---|---|
| Button - Primary | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — | — |
| Button - Secondary | ✓ | ✓ | ✓ | ✓ | ✓ | — | — | — |
| Fixture card | ✓ | ✓ | ✓ | ✓ | — | ✓ | — | — |
| Form input | ✓ | — | ✓ | — | ✓ | — | ✓ | — |
| Nav item | ✓ | ✓ | ✓ | — | — | — | — | — |
| What's missing panel | ✓ | — | — | — | — | ✓ | — | ✓ (all confirmed) |
| Search results page | ✓ | — | — | — | — | ✓ | ✓ | ✓ |
| Dashboard page | ✓ | — | — | — | — | ✓ | ✓ | ✓ |

---

## Assets

### Fonts

| Font | File | Format |
|---|---|---|
| Source Serif 4 (variable) | `Source_Serif_4[opsz,wght].ttf` | Variable TrueType |
| Source Sans 3 (variable) | `Source_Sans_3[wght].ttf` | Variable TrueType |

Available from Google Fonts or Adobe Fonts. Serve via CDN or self-hosted. SIL OFL 1.1 licence — no licensing cost.

### Logo/wordmark

| Asset | File | Use |
|---|---|---|
| Primary logo (horizontal) | `05-brand-identity/outputs/05-logo-primary.svg` | Full-size nav, marketing |
| Monogram | `05-brand-identity/outputs/06-logo-monogram.svg` | App icon, square favicon |
| Favicon | `05-brand-identity/outputs/07-favicon.svg` | Browser tab |

Do not modify SVG files — all text converted to paths. Do not add effects, shadows, or colour overlays.

---

## Open questions (design → engineering)

These require answers before engineering decisions are locked. Agent 9 should resolve with Agent 6 (or Agent 1 where indicated).

| Question | Owner | Impact |
|---|---|---|
| Email-only accept flow for umpires: does the confirmation page require login? | Agent 9 + Agent 6 | Umpire/service provider screen design |
| In-app notification display: panel, page, or inline on dashboard? | Agent 6 (not yet wireframed) | Notification component design |
| Service provider portal scope: full responsive or email-first for MVP? | Agent 1 decision | Entire SP portal design |
| Back-navigation state: should "← Back to search" restore scroll position as well as form state? | Agent 9 judgement | UX decision, implementation complexity |
| Should review reminder be a push notification (v2) or email only (v1)? | Agent 1 / product | Review flow trigger |

---

## Non-negotiable implementation constraints

These come from Agent 6 and Agent 2 and are not design preferences:

1. **Trust badge** must use text labels (New / Reliable / Established) — not stars, not percentages, not numbers. This is a domain decision.
2. **"What's missing" panel** must be visible without scrolling on desktop (right column) and above the fold on mobile (top banner). If a technical constraint forces a change, escalate before implementing.
3. **Review form** must have exactly 3 questions, each with a 3-point scale. No open text fields. No optional questions.
4. **Post availability CTA** from empty search results must pre-fill date and format from the failed search.
5. **Bottom tab bar** must always be visible on mobile — must not hide on scroll.
6. **Minimum body text: 16px.** No text below 16px on mobile inputs (prevents iOS zoom).
7. **Minimum tap target: 44×44px/pt** on all interactive elements.
8. **WCAG 2.2 AA** on all implemented screens — verified with automated tools before launch.

---

## When to escalate back to Agent 7

| Situation | Action |
|---|---|
| Engineering constraint forces a meaningful visual change | Document in decision log, notify Agent 7 |
| A new token is needed (not in current system) | Escalate to Agent 5 for sign-off, then Agent 7 implements |
| A component needs a new state not specified | Agent 7 to specify before engineering implements |
| Accessibility automated testing reveals a failure not caught in design audit | Agent 7 + Agent 9 resolve together |
| Screen layout breaks at a viewport size not covered in designs | Agent 7 to specify breakpoint behaviour |

---

## Version history

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2026-04-19 | Initial handoff — pre-usability-test |
