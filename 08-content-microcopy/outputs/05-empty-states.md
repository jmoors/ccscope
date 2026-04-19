# 05 — Empty States

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 8 (Content & Microcopy)
**Feeds:** Agent 7 (Figma, screen-level copy)

**Structure:** Each empty state has:
- Screen / context
- Heading (states the fact — one line)
- Body (why it's empty and/or what to do — one or two sentences)
- CTA label (specific action — no "Get started")
- No CTA if no meaningful action exists

**Rules applied:**
- No apology ("Sorry, nothing here")
- No chirpiness ("Be the first to post!")
- No "Looks like", "Seems like", "It appears that"
- Teach the product through the empty state — explain what the screen is for

---

## Dashboard

### New user — no fixtures, no availability

| Part | Content |
|---|---|
| Heading | `No fixtures yet` |
| Body | `Start by searching for a game. If no availability matches your dates, post your own and other teams will find you.` |
| CTA primary | `Find a game` |
| CTA secondary | `Post availability` |

### Returning user — no action items

| Part | Content |
|---|---|
| "Needs your attention" section | `Nothing requires action right now.` |

*(No CTA — this is a status note, not an empty state requiring action.)*

### Returning user — no upcoming fixtures

| Part | Content |
|---|---|
| "Upcoming fixtures" section | `No confirmed fixtures in the next 14 days.` |
| CTA (inline) | `Find a game` |

### Returning user — no availability posted

| Part | Content |
|---|---|
| "My availability" section | `No availability posted.` |
| CTA (inline) | `Post availability` |

---

## Find a game — search results

### No results for search

| Part | Content |
|---|---|
| Heading | `No availability found for {fixture_date}` |
| Body | `No teams have posted availability that matches your search. Post your own availability and you will appear in searches by other teams.` |
| CTA primary | `Post availability` |
| CTA secondary | `Change search` |

*Note: "Post availability" CTA must pre-fill date and format from the failed search.*

### No results — broader search suggestion

*(Shown if the search was narrowly filtered — e.g., specific format, short radius)*

| Part | Content |
|---|---|
| Inline notice | `No results for {fixture_format} within {radius} miles. Widen your search or post your availability.` |

---

## My fixtures list

### New user — no fixtures at all

| Part | Content |
|---|---|
| Heading | `No fixtures yet` |
| Body | `Fixtures appear here once a match request has been accepted. Find a game or post your availability to get started.` |
| CTA | `Find a game` |

### Filter: Upcoming — no upcoming fixtures

| Part | Content |
|---|---|
| Heading | `No upcoming fixtures` |
| Body | `No confirmed fixtures in the diary. Check your availability or search for a game.` |
| CTA | `Find a game` |

### Filter: Past — no past fixtures

| Part | Content |
|---|---|
| Heading | `No past fixtures` |
| Body | `Completed and cancelled fixtures will appear here.` |
| CTA | — |

### Filter: Needs action — nothing to action

| Part | Content |
|---|---|
| Heading | `Nothing requires action` |
| Body | `All fixtures are either confirmed or awaiting the other team.` |
| CTA | — |

---

## My availability list

### No availability posted

| Part | Content |
|---|---|
| Heading | `No availability posted` |
| Body | `Post your availability for dates you need a game. Other teams searching for opponents on those dates will find you.` |
| CTA | `Post availability` |

---

## Requests

### Incoming tab — no incoming requests

| Part | Content |
|---|---|
| Heading | `No incoming requests` |
| Body | `When a team sends you a match request, it will appear here.` |
| CTA | — |

### Sent tab — no sent requests

| Part | Content |
|---|---|
| Heading | `No sent requests` |
| Body | `Find availability and send a match request to start arranging a fixture.` |
| CTA | `Find a game` |

---

## Notifications

### No notifications

| Part | Content |
|---|---|
| Heading | `No notifications` |
| Body | `Notifications appear here when there is activity on your fixtures or requests.` |
| CTA | — |

---

## Club profile (public)

### Club has no teams listed

| Part | Content |
|---|---|
| Inline | `No teams listed.` |
| CTA | — *(public profile — no action available to viewer)* |

---

## Club administration

### Team list — no teams added

| Part | Content |
|---|---|
| Heading | `No teams added yet` |
| Body | `Add your club's teams to allow fixture managers to post availability and receive match requests.` |
| CTA | `Add team` |

### Roster — no one on the roster

| Part | Content |
|---|---|
| Heading | `No one on the roster yet` |
| Body | `Add umpires and scorers to your club's roster. Fixture managers can then request them for specific fixtures.` |
| CTA | `Add person` |

### Venue list — no venues added

| Part | Content |
|---|---|
| Heading | `No grounds added yet` |
| Body | `Add your club's home grounds so they can be selected when posting availability or confirming fixtures.` |
| CTA | `Add ground` |

### Trust summary — no reviews yet

| Part | Content |
|---|---|
| Heading | `No reviews yet` |
| Body | `Reviews are collected after completed fixtures. They are always private.` |
| CTA | — |

---

## Service provider (umpire) portal

### No incoming requests

| Part | Content |
|---|---|
| Heading | `No incoming requests` |
| Body | `When a fixture manager sends you a request, it will appear here.` |
| CTA | — |

### No upcoming fixtures

| Part | Content |
|---|---|
| Heading | `No upcoming fixtures` |
| Body | `Fixtures you have accepted will appear here.` |
| CTA | — |

### No past fixtures

| Part | Content |
|---|---|
| Heading | `No past fixtures` |
| Body | `Fixtures you have umpired will appear here once completed.` |
| CTA | — |

---

## Find support — umpire request

### No umpires on roster

| Part | Content |
|---|---|
| Heading | `No umpires on your club's roster` |
| Body | `Ask your Club Administrator to add umpires to the roster. Once added, you can send them requests from here.` |
| CTA | — *(FM cannot add umpires — Club Admin action required)* |

---

## Fixture detail — "What's needed" panel (all resolved)

*(Not a standard empty state, but a positive-completion state)*

| Part | Content |
|---|---|
| Panel content | `Everything confirmed.` |

---

## Notes on rendering empty states

1. Empty states must be visually part of the product, not afterthoughts. Agent 7 should give them the same design care as populated states.
2. Every empty state is an onboarding opportunity for new users — the body copy explains what the screen is for and what will appear there.
3. CTAs in empty states should be styled as secondary buttons (or text links), not prominent primary buttons, except on the dashboard where the primary empty state CTA is the highest-priority action.
4. Do not use illustration assets that make empty states feel like a marketing moment.

---

*Maintained by: Agent 8 (Content & Microcopy)*
*Agent 7: use these strings as final copy in Figma; replace all placeholder empty-state text in wireframes.*
