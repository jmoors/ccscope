# 05 — Pattern Documentation

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 7 (Design System & Screen Design)  
**Figma page:** Components (page 5), Screen patterns (page 6)

---

## Pattern index

| # | Pattern | Screens it applies to |
|---|---------|----------------------|
| P01 | Empty states | Dashboard, Search results, My fixtures, My availability, Requests, Notifications |
| P02 | Skeleton loading | All data screens |
| P03 | Error states | All data screens, form submissions |
| P04 | Form validation | Find a game, Post availability, Send match request, Review |
| P05 | Confirmation flows | Accept request, Cancel fixture, Decline request, Withdraw availability |
| P06 | Navigation and back behaviour | All screens |
| P07 | Toast notifications | Settings save, action confirmation |
| P08 | Offline mode | Mobile only |
| P09 | Pagination and list behaviour | My fixtures, search results |
| P10 | Compatibility notices | Search results, Send match request |

---

## P01 — Empty states

### Principle

Every empty state is unique. There is no generic "Nothing here" fallback.

For the first months of the product, the empty state IS the primary experience for most new users. It must communicate what the product does and what to do next — not apologise for missing data.

### Rules

1. Never use "There's nothing here yet" as the heading.
2. Never add a sad illustration or emoji.
3. Never say "Oops" or any exclamation-mark-heavy copy.
4. Always include at least one clear action (a next step).
5. The action must be contextually accurate — not just a generic "get started."
6. On the search empty state, always pre-fill the action CTA with the search parameters.

### Empty state anatomy

```
[Heading] — what's empty, stated plainly
[Body copy] — 1–2 sentences, what to do
[Primary CTA] — the next step
[Secondary CTA or supporting content] — optional
```

### Per-screen empty states (copy is placeholder — Agent 8 finalises)

See C09 component library for visual specs. Copy summary:

| Screen | Heading | Body (placeholder) | CTA |
|---|---|---|---|
| Dashboard | Your fixture list is empty. | Start by searching for available teams, or post your own availability. | [Find a game] [Post availability] |
| Search results | No availability found for [date] within [distance]. | Try adjusting your search below, or post your own availability. | Adjustments + [Post availability for [date]] |
| My fixtures | No fixtures yet. | When you accept or send a match request, your fixtures appear here. | [Find a game] |
| My availability | No availability posted. | You can post availability when no teams come up in search — or any time you want to be found. | [Post availability] |
| Requests | No requests at the moment. | Match requests from other clubs will appear here. | — |
| Notifications | No notifications. | You'll be notified when a team responds or sends a request. | — |

### Search empty state: dynamic adjustment suggestions

The "Try adjusting" block on search empty state is dynamic. Only show adjustments that are contextually valid:

- "Widen to [X] miles" — only show if search was narrower than 50 miles, and show a specific suggested distance (35 miles if searched 20, 50 if searched 35)
- "Try a different date" — always show
- "Include away games" — only show if "Home preferred" or "Away preferred" was selected; not if "No preference" was already set
- "Try a different format" — only show if a single format was selected

---

## P02 — Skeleton loading

### Principle

Skeleton screens show the shape of the content before it arrives. They prevent layout shift and signal to the user that something meaningful is loading.

**No spinner.** No "Loading..." text. Only content-shaped grey pulsing shapes.

### Timing

- Skeleton appears after 200ms delay (CSS `transition-delay: 200ms` on `.skeleton` visibility)
- This prevents a flash on fast loads (< 200ms)
- After 10 seconds of no content, transition from skeleton to error state

### Animation

```css
@keyframes skeleton-pulse {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.4; }
}
.skeleton {
  background-color: var(--color-neutral-stone);
  border-radius: var(--radius-sm);
  animation: skeleton-pulse 1.5s ease-in-out infinite;
}
```

### Skeleton shapes

Skeleton elements represent their corresponding content:

| Content | Skeleton shape |
|---|---|
| Heading | Full-width bar, 24px height |
| Body paragraph | 3 bars: 100%, 100%, 65% width; 14px height each |
| Fixture card | Full card dimensions, 3 inner bars |
| Status pill | Pill shape, 80px × 24px |
| Trust badge | Text-width bar |
| "What's missing" panel | Full panel height and width |
| Form label + input | 80px label bar + full-width input-height bar |

### Aria

```html
<div role="status" aria-live="polite" aria-label="Loading [content name]">
  <!-- skeleton elements -->
</div>
```

When content loads, aria-live region announces "Loaded" (or specific count).

---

## P03 — Error states

### Principle

Error states are practical, not apologetic. Tell the user what to do. Never blame them. Never use "Oops", "Uh-oh", emoji, or exclamation marks.

Errors come in two categories:

1. **System errors** — network failure, server error, timeout
2. **Validation errors** — user input that cannot be processed

### System error template

```
[What failed — plain description]

Check your internet connection and try again.

[Try again]

If this continues: support@pavilion.cricket
```

- Error heading: `type-body`, `--text-primary` — not red, not alarming
- "Try again": Primary button
- Support: `type-caption`, `--text-secondary`
- No error codes shown to users (log to console for debugging)

### Validation error pattern

Inline, below the field that failed:

```
[Label]
┌───────────────────────────────┐
│  [Invalid value]              │  ← red border: 2px --color-error-text
└───────────────────────────────┘
✗ Please select a format.       ← error-text colour, 14px, with ✗ icon
```

Rules:
- Error appears after the user leaves the field (blur) or tries to submit
- Never show errors before the user has interacted with a field
- One error message per field — the most actionable one
- After correction, error clears immediately (live validation on input)
- Form submit button: if form has errors, scroll to first error and move focus to it
- Aria: `aria-describedby` linking input to error message; `aria-invalid="true"` on input

### Error message language

Do not use:
- "Invalid [thing]"
- "Error: [technical message]"
- "This field is required"

Use:
- "Please select a format."
- "Please enter a postcode." (not "Postcode is invalid")
- "Please choose a date in the future."

### Error boundary (system level)

If the entire page fails to load, show the system error template within the content area. Keep the nav intact (sidebar / bottom tabs) so the user can navigate elsewhere.

---

## P04 — Form validation

### When validation triggers

| Trigger | Validation |
|---|---|
| User leaves field (blur) | Validate that field |
| User interacts then clears field | Show error on blur |
| User submits form | Validate all required fields |
| User corrects a field with an error | Clear error immediately on input |

### Required vs optional

- Required fields: no asterisk (*) — it adds visual noise and confuses screen readers. Instead, mark **optional** fields with "(optional)" in the label. Most fields in Pavilion are required; few are optional.
- Exception: the note/message textarea on Send match request is optional. Label: "ADD A NOTE (optional)"

### Character counters

Textareas show a character counter below-right:
- `{n} / {max} characters`
- At 80% of limit: `--color-accent-amber` (caution)
- At 100%: `--color-error-text`, counter reads "0 characters remaining"
- Over limit: disable submit or truncate (prefer: disable submit + highlight error)

### Form completion state

On successful form submit:
- Show success confirmation inline (not a toast for multi-step actions)
- Success copy: plain statement of what happened ("Match request sent.")
- Provide a clear next step

---

## P05 — Confirmation flows

### Principle

Destructive or irreversible actions require explicit confirmation. Never auto-proceed on significant actions. Never auto-dismiss a confirmation dialog.

"Significant" means:
- Creates a binding commitment (Accept match request)
- Destroys data (Cancel fixture, Withdraw availability)
- Affects another party (Decline request)

### Confirmation levels

**Level 1 — Simple ghost link** (lowest stakes)
Used for: "Not now", "Remind me later"
Pattern: ghost link, no dialog

**Level 2 — Confirmation dialog** (medium stakes)
Used for: Accept match request, Decline request, Withdraw availability
Pattern: C08 modal (desktop) or C08 bottom sheet (mobile)
- Primary CTA confirms the action
- Secondary option ("Go back") provides exit
- Initial focus: secondary option (prevents accidental confirm)

**Level 3 — Destructive confirmation dialog** (high stakes)
Used for: Cancel fixture, Block club
Pattern: C08 destructive variant
- Primary CTA: Destructive button (red)
- Secondary: "Go back" — initial focus
- Body copy includes consequence ("Cancellations within 48 hours affect your trust record")
- Escape key does NOT close this dialog

### Accept match request confirmation

Title: "Accept match request"  
Body: "Accepting creates a fixture on [date] with [team]. Cancellations within 48 hours of the match affect your trust record."  
Primary: [Confirm — Accept]  
Secondary: [Go back]  
Initial focus: [Go back]  

### Cancel fixture confirmation

Title: "Cancel this fixture"  
Body: "Cancelling this fixture will notify [team]. [If within 48 hours:] Cancellations within 48 hours of the match affect your trust record."  
Primary: [Confirm — cancel this fixture] (Destructive button)  
Secondary: [Go back]  
Initial focus: [Go back]  

### Decline request confirmation

Title: "Decline this request?"  
Body: "Declining will release your availability for [date]."  
Primary: [Confirm — Decline] (Destructive button)  
Secondary: [Go back]  
Initial focus: [Go back]  

---

## P06 — Navigation and back behaviour

### Back links

All back links use the pattern: `← [Destination name]`

Never: "← Back". Always name the destination.

| From | Back label |
|---|---|
| Fixture detail | ← My fixtures |
| Send match request | ← [Team] availability |
| Match request detail | ← Requests |
| Post availability | ← Dashboard (or ← Search results) |
| Review form | ← [Fixture name] |
| Onboarding step 2 | ← Club details |

### State preservation

- "← Back to search" from Search results: restores the search form with previous parameters intact
- All other back navigation: clears state (start fresh)
- Reason: search form restoration prevents the most common re-do task; all other flows are short enough that re-entry is not burdensome

### Active nav item

The nav item (sidebar or bottom tab) that corresponds to the current section is visually active.

Mapping:
- Dashboard → Home
- Find a game / Search results → Find a game
- My fixtures / Fixture detail → Fixtures (or My fixtures)
- Requests / Request detail → Requests
- Post availability → no specific tab active (is a flow, not a destination)
- Settings / Notifications → not in bottom tabs; in sidebar secondary items

---

## P07 — Toast notifications

Toasts are used only for:
- Auto-save confirmations (Notification preferences saved)
- Non-critical confirmations that don't require acknowledgement

Toasts are NOT used for:
- Errors (use inline error)
- Important confirmations (use confirmation dialog)
- Match request notifications (use in-app notification system)

### Toast specs

```
┌──────────────────────────────────────────┐
│  ✓  [Message text]                       │  ← Forest bg, white text
└──────────────────────────────────────────┘
```

- Position: bottom of screen, centred, `--space-4` above bottom tab bar
- Background: `--color-primary-forest`
- Text: white, 14px, medium
- ✓ icon: white, `aria-hidden="true"`
- Width: fit-content, max 360px, `--radius-md`, `--space-3` padding
- Duration: 3 seconds, then fades out
- aria-live="polite" on toast region
- Does not require user dismissal
- Max 1 toast at a time (queue: previous toast fades before next appears)

---

## P08 — Offline mode (mobile)

When the device loses network connectivity:
1. A notification bar (C19) appears at the top of the screen: "No internet connection. Showing last saved data."
2. All interactive elements (buttons, forms, links) are disabled
3. Content from the most recent successful load is shown as read-only
4. Any review drafts are queued in localStorage and sent on reconnect
5. When connection is restored: notification bar disappears; interactivity resumes; content refreshes silently

No full-page error screen. The user can still see their fixture data.

---

## P09 — Pagination and list behaviour

### My fixtures list

Default view: most recent upcoming fixtures first. Past fixtures below a "Past fixtures" divider.

Load pattern:
- Initial load: most recent 10 upcoming + most recent 5 past
- "Show more" ghost link at the bottom (not infinite scroll — avoids loss-of-position on mobile)
- No pagination numbers

### Search results

All results shown on a single page (search is bounded by distance filter, so results rarely exceed 20).

No pagination. If > 20 results (unlikely), show first 20 with "Show more results" link.

### Requests list

Most recent first. Unread/unactioned requests visually distinguished (no special styling needed beyond the badge count — the requests list is inherently short).

---

## P10 — Compatibility notices

Compatibility notices inform the user of a soft mismatch between their search criteria and the available team's profile. They are not errors — they are information the user needs to have a productive conversation with the other team.

### Principle

Show early; never hide. A user who sends a match request without knowing about a format mismatch wastes both teams' time.

Notices appear:
1. On the search result card (inline, before the user clicks through)
2. On the Send match request form (as a block, requiring acknowledgement)

### Types

| Notice type | Trigger condition |
|---|---|
| Format | User searched T20, available team prefers different format (or vice versa) |
| Tier | Significant tier gap (> 1 tier difference) |
| Age group | Teams' age group criteria differ |
| Gender | Teams' gender categories differ |

### Display on search result card

Inline below the team details line, before the action link:

```
⚠ Format note: Sunday XI matches on T20 by agreement
```

- `type-caption` (14px)
- `--color-accent-amber` for ⚠ icon
- `--text-primary` for message text
- No background (inline card context)

### Display on Send match request form

As a block within the form (see Screen 05 for visual), requiring a checkbox acknowledgement.

Checkbox label: "I understand and will confirm [the format / the details] with [team name]."

The submit button is disabled until this checkbox is ticked.

### What compatibility notices do NOT do

- They do not prevent a match request being sent
- They do not suggest the match is unsuitable
- They do not use alarming language ("Warning: mismatch detected")
- The ⚠ icon is informational, not error-level

If both parties agree on the details, a format mismatch is not a problem. The notice ensures both parties know to discuss it.
