# 01 — Sitemap & Navigation Model

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft

---

## 1. Site Structure

### 1.1 Public (unauthenticated)

```
/                           Landing
/sign-in                    Sign in
/join                       Join your club (invitation-code entry)
/clubs/:slug                Public club profile (read-only)
/clubs/:slug/teams/:id      Public team profile (read-only)
```

**What's public:** Club name, badge, home ground, active teams, trust badge (New / Reliable / Established). Nothing else.

**What requires authentication:** Everything below.

---

### 1.2 Authenticated — Fixture Manager context

```
/dashboard                  Dashboard (default post-login view)

/find                       Find a game — search form
/find/results               Search results list
/find/results/:avail-id     Availability detail (before sending request)

/availability               My availability — list of published slots
/availability/new           Post availability — form
/availability/:id           Manage a specific published availability

/fixtures                   My fixtures — list
/fixtures/:id               Fixture detail
/fixtures/:id/request       Send match request (from fixture detail)
/fixtures/:id/support       Find support — umpire / scorer request flow
/fixtures/:id/review        Submit post-match review

/requests                   Incoming match requests — list
/requests/:id               Match request detail (accept / decline)

/notifications              Notification inbox — all events

/club                       Club profile (read for FM; edit for Club Admin)
/club/teams                 Team list (read for FM)
/club/teams/:id             Team detail
/club/roster                Club roster — umpires / scorers

/settings                   Settings hub
/settings/notifications     Notification preferences
/settings/account           Account details
```

---

### 1.3 Authenticated — Club Admin additions

Club Admins see all FM screens plus:

```
/club/edit                  Edit club profile
/club/venues                Venue list
/club/venues/new            Add venue
/club/venues/:id            Edit venue
/club/teams/new             Add team
/club/teams/:id/edit        Edit team
/club/roster/add            Add umpire / scorer to roster
/club/roster/:id/edit       Edit roster entry

/club/trust                 Trust summary — aggregate review scores (read-only)
```

---

### 1.4 Authenticated — Service Provider (Umpire / Scorer)

Service providers access a scoped view. They do not see the full fixture management UI.

```
/sp/dashboard               Support requests — incoming and past
/sp/requests/:id            Support request detail (accept / decline)
/sp/fixtures/:id            Fixture detail (read-only; their own only)
/settings                   Shared settings
```

---

## 2. Navigation Model

### 2.1 Primary navigation (authenticated, FM / Club Admin)

Persistent across all pages. On desktop: left sidebar. On mobile: bottom tab bar.

| Tab | Icon label | Route |
|---|---|---|
| Dashboard | Home | /dashboard |
| Find a game | Find | /find |
| My fixtures | Fixtures | /fixtures |
| Requests | Requests | /requests |
| Notifications | [with badge count] | /notifications |

Club admin functions (club profile, roster, team management) are reached via the club name / avatar in the top-right corner (desktop) or via a "Club" item in the mobile nav when the user is a Club Admin.

**Why a dedicated Requests tab rather than collapsing into Fixtures:**  
Incoming match requests arrive at the team level, not the individual fixture level. A fixture manager may have multiple incoming requests simultaneously. Separating "requests to act on" from "fixtures I'm already managing" reduces the risk of missed requests being buried in a longer fixture list.

---

### 2.2 Context-switching (multi-team users)

A user who holds Fixture Manager roles on multiple teams (e.g., 1st XI and 2nd XI) must explicitly select which team context they are acting in. This is enforced at the navigation level.

**Pattern:** Team context picker appears:
- In the top bar, adjacent to the club name, on desktop
- As a persistent label below the page title on mobile

The team context picker is always visible when the user has multiple roles. It is never hidden behind a settings screen.

**Behaviour on context switch:**
- The fixture list, availability list, and requests refresh to show the selected team's data.
- A page transition animation (brief fade) signals the context change.
- The current URL does not include team context — the team context is a session-level state, not a URL parameter. This is acceptable for MVP because deep-linking to a specific team's fixture list is not a required use case.

**FLAG for Agent 9:** Team context state must persist across page loads (session storage minimum, server-side preferred). If a user refreshes mid-session, they should not be returned to their default team unexpectedly.

---

### 2.3 Service provider navigation

Service providers see a simplified nav:

| Tab | Route |
|---|---|
| Requests | /sp/dashboard |
| Notifications | /notifications |

They do not see Find a game, My fixtures, or Requests tabs in the full FM sense.

---

### 2.4 Back-navigation model

**Principle:** The user should always be able to trace their path back. Back = where I came from, not always the parent in the sitemap hierarchy.

| From | Back navigates to |
|---|---|
| /find/results | /find (preserving search form state) |
| /find/results/:avail-id | /find/results (preserving results list and scroll position) |
| /fixtures/:id | /fixtures |
| /fixtures/:id/request | /fixtures/:id |
| /fixtures/:id/support | /fixtures/:id |
| /fixtures/:id/review | /fixtures/:id |
| /requests/:id | /requests |
| /availability/:id | /availability |

**Search form persistence:** When a user navigates from search results to an availability detail and then presses Back, their search parameters and result list position must be preserved. This is the most common navigational loop in the primary flow and must not reset.

---

### 2.5 Deep links

The following URL patterns must be navigable from email notifications without requiring the user to be already logged in. On click, they are prompted to sign in, then redirected to the target URL.

| Notification | Deep link |
|---|---|
| MATCH_REQUEST_RECEIVED | /requests/:id |
| MATCH_REQUEST_ACCEPTED | /fixtures/:id |
| MATCH_REQUEST_DECLINED | /fixtures/:id |
| FIXTURE_CONFIRMED | /fixtures/:id |
| FIXTURE_CANCELLED | /dashboard |
| SUPPORT_REQUEST_RECEIVED | /sp/requests/:id |
| REVIEW_PROMPT | /fixtures/:id/review |

---

## 3. Information Hierarchy

### 3.1 Fixture — hierarchy of concern

The fixture is the central object. Information is organised by urgency of action required.

**Level 1 — What requires action now:**
- Awaiting response (incoming match request to act on)
- Awaiting your confirmation of venue or officials
- Review pending (completed fixture, review window open)

**Level 2 — What's in motion:**
- Awaiting opponent (your availability is published; you can be found)
- Awaiting response from your outgoing request
- Confirmed fixtures in the next 14 days

**Level 3 — Background state:**
- Confirmed fixtures beyond 14 days
- Past fixtures (completed or cancelled)

**Implication for fixture list:** Sort by urgency (Level 1 first), then by date within each level.

---

### 3.2 Dashboard hierarchy

The dashboard is a dispatch surface. It shows:

1. Immediate action items (match requests to act on, reviews due, short-notice cancellations)
2. Upcoming confirmed fixtures (next 2 weeks)
3. Published availability with no match request yet (passive monitoring)
4. A prompt if the user has no fixtures or availability (empty state — most important screen)

The dashboard does not show a news feed, announcements, or any non-fixture content in MVP.

---

## 4. URL conventions

- Slugs for clubs: `{club-name}-cc` format, e.g., `thornton-cc`
- Fixture IDs: opaque UUID in URL, not sequential integers (prevents enumeration)
- No session IDs or auth tokens in URLs
- Query parameters used only for search state on `/find` and `/find/results`

**Search query parameters:**

| Param | Example | Notes |
|---|---|---|
| `date` | `2026-06-14` | ISO 8601 |
| `format` | `t20` | Format ID from taxonomy |
| `age` | `open` | Age group ID |
| `gender` | `mens` | Gender category ID |
| `radius` | `30` | Miles; integer |
| `home` | `true` | Home/away preference |

These params make search results shareable and bookmarkable. If a user copies a results URL, it loads the same search pre-filled.

---

## 5. Escalation flags

| Flag | Target |
|---|---|
| Team context URL strategy (session vs. URL) may affect deep-link behaviour — clarify with Agent 9 before implementation | Agent 9 |
| Service provider onboarding flow is not fully scoped — how does an umpire get their /sp/ account? | Agent 1 |
| Public club profile scope: what exactly is public without login? Trust badge visibility affects positioning. | Agent 1 |
