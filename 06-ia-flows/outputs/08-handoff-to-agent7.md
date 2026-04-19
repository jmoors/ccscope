# 08 — Handoff to Agent 7 (Design System & Screen Design)

**Version:** 1.0  
**Date:** 2026-04-19  
**From:** Agent 6 (Information Architecture & Flows)  
**To:** Agent 7 (Design System & Screen Design)  
**Status:** Draft — usability testing not yet complete; wireframes may be revised

---

## What is in this handoff

| Artefact | File | Status |
|---|---|---|
| Sitemap & navigation model | `01-sitemap.md` | Complete |
| Service blueprint | `02-service-blueprint.md` | Complete |
| Journey maps (12 maps) | `03-journey-maps.md` | Complete |
| Desktop wireframes (6 priority screens, all states) | `04-wireframes-desktop.md` | Draft — awaiting usability test |
| Mobile wireframes (6 priority screens, all states) | `05-wireframes-mobile.md` | Draft — awaiting usability test |
| Edge case wireframes | `06-edge-case-wireframes.md` | Complete |
| Usability test plan | `07-usability-test-plan.md` | Ready — testing not yet started |

**Note:** These wireframes represent the pre-test version. Agent 7 should treat them as the structural foundation but should expect revisions after usability testing completes. Do not build the full component library from these until usability results are available. However, starting on design tokens, colour system, and typography (which are not affected by IA findings) is appropriate now.

---

## What Agent 7 needs to know about the IA

### Navigation model summary

- **Desktop:** Left sidebar (240px), persistent. 5 primary nav items.
- **Mobile:** Bottom tab bar, always visible. 5 items. No hamburger menu.
- **Team context switcher:** Always visible and prominent. Top-right on desktop; top of content area on mobile. Users with multiple team roles need this constantly.
- **Back navigation:** Always labelled with destination ("← My fixtures"), not generic "← Back."

### Screen design priorities

**Priority 1 (most used, most visible):**
1. Dashboard — default and empty states
2. Find a game (search form)
3. Search results — populated and empty states
4. Fixture detail — with "What's missing" panel

**Priority 2 (important but less frequent):**
5. Match request detail (receiving team)
6. Send match request
7. Post availability

**Priority 3 (needed but less complex):**
8. Review form
9. Club onboarding (3-step)
10. Settings / notification preferences

---

## Component inventory (from wireframes)

The following reusable components are identified in the wireframes. Agent 7 should build these as distinct components with labelled variants.

### Availability / fixture card

Used in: Dashboard, My fixtures list, My availability list.

**Variants:**
- State: Awaiting opponent / Awaiting response / Awaiting venue / Awaiting officials / Confirmed / Completed / Cancelled
- Size: Standard (dashboard) / Compact (list view)
- Action links: variable per state

### Trust badge

Used in: Search results, availability detail, match request detail, team profile.

**Variants:**
- New (● or similar)
- Reliable (◆ or similar)
- Established (◆◆ or similar)

Must be text-based, not star-based. Must be readable at small size (within a result card). Must not look like a rating system.

### "What's missing" panel

Used in: Fixture detail.

**Variants:**
- Desktop: Right-column panel
- Mobile: Top banner, full width
- States: All resolved (confirmed) / 1 gap / 2 gaps (priority-ordered)
- Items: ✗ (unresolved) / ✓ (resolved) / ○ (deferred — e.g., officials pending venue)

### Compatibility notice

Used in: Search results (inline on card), send match request form.

**Variants:**
- Format notice
- Age group notice
- Gender notice

Icon: ⚠ or equivalent. Must not alarm — informational, not error-level.

### Notification badge

Used in: Nav (Requests, Notifications tabs).

**Variant:** Number badge on nav item. Disappears when count = 0.

### Confirmation dialog / sheet

Used in: Accept match request, cancel fixture, block club.

**Desktop:** Modal dialog.  
**Mobile:** Bottom sheet or full-screen overlay.

**Key design constraint:** Never auto-dismiss. Requires explicit user action to close.

### Empty state block

Used in: Dashboard, search results, fixture list, availability list.

**Variants per screen:** Each has unique copy (not a generic "Nothing here" pattern). Copy is provided in wireframes as placeholder; Agent 8 finalises.

### Form fields

- Date picker: Prefer native where possible (especially mobile). Custom only if accessibility requires it.
- Dropdown: Native select on mobile. Styled dropdown on desktop (accessible, keyboard-navigable).
- Radio group: Full-width on mobile. Horizontal on desktop where space allows.
- Textarea: Character counter visible. Placeholder text is a concrete example, not "Type here."
- Toggle buttons: Format selection on search form. 2-row grid on mobile.

---

## State variants required (per screen)

Every screen must have:

| State | Description |
|---|---|
| Default | Normal, populated content |
| Empty | No content in that context |
| Loading | Skeleton loading, not spinner |
| Error | Network or system failure |

Edge cases (covered in `06-edge-case-wireframes.md`) are additional states on specific screens. They must be layered into the Figma file as separate frames, not as design notes.

---

## Design constraints from IA

### Things Agent 7 must not change

- "What's missing" panel must always be visible without scrolling on desktop (right column) and above the fold on mobile (top banner). If the design system requires a different layout approach, escalate before proceeding.
- Trust badge must use text labels (New / Reliable / Established), not stars, not percentages, not numeric scores. This is a domain decision from Agent 1 and Agent 2.
- The review form must have exactly 3 questions, each with a 3-point scale. No open text fields. No optional questions.
- The "Post availability" CTA on the empty search results page must pre-fill the date and format from the failed search. This is a critical usability mechanism.
- Bottom tab bar must always be visible on mobile — must not hide on scroll.
- Touch targets: minimum 44×44pt on all interactive elements.
- WCAG 2.2 AA minimum — this includes colour contrast, keyboard navigation, and focus states.

### Things Agent 7 has latitude on

- Exact visual treatment of the trust badge indicator (◆, ●, etc. in wireframes are placeholders)
- Animation and transition details (within the "calm, not flashy" constraint)
- The exact visual design of the skeleton loading pattern
- Typography scale and spacing within the design tokens from Agent 5
- How exactly the team context switcher is styled (dropdown vs. pills vs. segmented control) — as long as it's always visible and prominent

---

## Tone guidance for visual design

From Agent 1 (Product Foundations) and Agent 5 (Brand Identity):

- **Calm, institutional-in-a-good-way.** Not startup-loud, not sports-media.
- **Comparison points:** National Trust, Ordnance Survey, GOV.UK.
- **Greyscale wireframes become a full colour system.** Reference Agent 5 outputs for the colour system and design tokens.
- **No animation that serves itself.** Any transition must serve orientation or task clarity.
- **Error and empty states must feel part of the product, not afterthoughts.** They are the most common first experience for new users.

---

## Collaboration protocol

| When | What |
|---|---|
| Agent 7 has a design question about a specific screen layout | Check the wireframe annotations first; if not answered, contact Agent 6 |
| Agent 7 wants to change a layout that has an IA rationale | Agree with Agent 6 before implementing — IA constraints are not aesthetic preferences |
| Agent 7 finds an inconsistency between desktop and mobile wireframes | Flag to Agent 6; do not resolve unilaterally |
| Agent 8 finalises copy | Agent 7 updates placeholder copy in Figma from Agent 8's outputs |
| Usability testing results arrive | Agent 6 shares revised wireframes; Agent 7 updates Figma accordingly |

---

## Known open questions (Agent 7 should not resolve these alone)

| Question | Owner |
|---|---|
| Email-only accept flow for umpires: does the confirmation page require login or not? | Agent 9 (engineering) + Agent 6 |
| How are notifications displayed in-app — a panel, a full page, or inline on the dashboard? | Agent 6 (not yet wireframed in detail) |
| Service provider (/sp/) portal design scope — full responsive layout or simplified email-first? | Agent 1 decision needed |
| Figma file naming and handoff conventions | Agent 7 to propose; Agent 6 to confirm |

---

## Figma file structure recommendation

```
06-ia-flows-to-agent7.fig
├── 0. Cover (link to this document)
├── 1. Navigation model (sitemap diagram)
├── 2. Desktop screens
│   ├── Dashboard (Default / Empty / Loading / Error)
│   ├── Find a game
│   ├── Search results (Populated / Empty)
│   ├── Fixture detail (each state variant)
│   ├── Send match request
│   └── Match request detail
├── 3. Mobile screens (same screens, independent layouts)
├── 4. Edge cases
├── 5. Components (by type, with all variants labelled)
└── 6. Flow diagrams (linking screens in sequence)
```

Layer naming convention:
- Screen frames: `[Screen name] / [State]` e.g., `Dashboard / Empty`
- Components: `[Component name] / [Variant]` e.g., `Trust badge / Reliable`
- Annotations: A separate layer named `Annotations` on each screen frame, toggleable

---

## What comes after this handoff

1. Agent 7 begins design system and screen design from this IA foundation
2. Agent 6 runs usability testing (Segment A–F, 50+ participants)
3. Usability results documented in `09-usability-results.md`
4. Agent 6 shares revised wireframes for any screens where hypotheses failed
5. Agent 7 updates Figma accordingly
6. Final handoff artefact from Agent 7 to Agent 9 (Engineering)
