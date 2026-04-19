# 02 — Service Blueprint

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft

---

## How to read this document

A service blueprint maps four layers of activity:
1. **User actions** — what the user does
2. **Frontstage** — what the user sees or touches in the interface
3. **Backstage** — system processes the user doesn't directly see
4. **Support processes** — infrastructure, external services, policies

This document covers the primary service: finding and confirming a fixture. Secondary services (umpire request, trust review) follow the same structure with shorter blueprints.

---

## Blueprint A — Find a Game → Confirmed Fixture

### Phase 1: Search

| Layer | Actions |
|---|---|
| **User action** | Opens platform. Fills in search form: date or date window, format, home/away preference, distance radius. Submits. |
| **Frontstage** | Search form. Progress indicator while results load. Search results list (sorted by relevance). Each result shows: team name, club name, format, distance, trust badge, compatibility status. |
| **Backstage** | Search query assembled from form parameters. Matching algorithm runs: hard-filter exclusions applied first (format incompatibility, gender incompatibility, blocks, age group hard exclusions). Soft-match scoring applied. Results ranked: distance weight × format score × tier score × trust contribution. Results returned in < 2 seconds. |
| **Support** | Postcode-to-coordinates lookup service. Distance calculation (straight-line, km). Fixture availability index (updated on publish/withdraw events). |

**Line of visibility** (above = user sees it; below = user doesn't):

```
[ Search form ] → [ Results list ] → [ Availability detail ]
─────────────────────────────────────────────────────────
[ Matching algorithm ] → [ Ranking algorithm ] → [ Availability index ]
```

---

### Phase 2: Review and select

| Layer | Actions |
|---|---|
| **User action** | Browses results. Clicks through to one or more availability detail pages. Reviews team details: format, age group, home ground location, trust badge. Decides to send a match request. |
| **Frontstage** | Availability detail page: team profile summary, fixture parameters, compatibility notice (if soft match), trust badge, location map (static, shows home ground). "Send match request" call to action. |
| **Backstage** | Availability record fetched. Team and club data joined. Compatibility notices computed from format/age/gender soft match flags. Trust badge computed from trust score record. |
| **Support** | Team profile data. Trust score store. |

---

### Phase 3: Send match request

| Layer | Actions |
|---|---|
| **User action** | Clicks "Send match request." Reviews pre-filled match parameters. Adds a note (optional, 200 char). Confirms and sends. |
| **Frontstage** | Match request form. Pre-filled fields: date, format. Editable: note to receiving team. Compatibility notice shown if soft match (requires user to acknowledge). Submit button. Confirmation state after submit. |
| **Backstage** | Match request record created. Fixture status transitions: `awaiting_opponent` → `awaiting_response`. Availability locked. Notification event `MATCH_REQUEST_RECEIVED` fired → email + in-app to receiving FM. |
| **Support** | Notification delivery service (email + in-app). Fixture state machine. Idempotency check (prevent double-submit on slow connection). |

---

### Phase 4: Waiting for response (sending team's perspective)

| Layer | Actions |
|---|---|
| **User action** | Returns to dashboard. Sees fixture in "Awaiting response" status. May check back. Receives notification if request accepted, declined, or expires. |
| **Frontstage** | Fixture card on dashboard: "Awaiting response — sent to [Team Name]." Time elapsed indicator. Option to withdraw request. |
| **Backstage** | No action unless: (a) 7-day expiry timer fires → T04 transition, (b) receiving team responds. |
| **Support** | Scheduled job: check for expired match requests (runs daily at 09:00). |

---

### Phase 5: Receiving team receives and acts on the request

| Layer | Actions |
|---|---|
| **User action** | Receiving FM gets email notification. Clicks through to match request detail. Reviews: who is requesting, the fixture parameters, note from requesting team. Accepts or declines. |
| **Frontstage** | Match request detail page: requesting team summary, fixture parameters, note, trust badge of requesting team. "Accept" and "Decline" buttons. Both require confirmation step. |
| **Backstage** | On accept: fixture status transitions based on venue/officials state (T05, T06, or T07). Notification `MATCH_REQUEST_ACCEPTED` or `MATCH_REQUEST_DECLINED` fired to sending FM. Receiving team's own availability for that date closed/locked. |
| **Support** | Fixture state machine. Notification service. |

---

### Phase 6: Fixture confirmed (happy path)

| Layer | Actions |
|---|---|
| **User action** | Both FMs receive "Fixture confirmed" notification. View fixture detail. Monitor "What's missing" panel if any gaps remain. |
| **Frontstage** | Fixture detail page: status "Confirmed" (or "Awaiting venue" / "Awaiting officials" if gaps). "What's missing" panel listing open items with action links. |
| **Backstage** | Fixture record updated. Both team availability records updated to `filled`. |
| **Support** | — |

---

### Phase 7: Gaps filled (if needed)

| Layer | Actions |
|---|---|
| **User action** | FM confirms venue (either party). FM sends umpire support request via "Find support" flow. Umpire accepts. |
| **Frontstage** | Venue confirmation: inline edit on fixture detail or separate venue-confirm form. Support request flow: select umpire from club roster, add date/fixture context, send. |
| **Backstage** | Venue confirmation: `venue_confirmed = true`. Transition T08 fires if applicable. Support request: notification to umpire. On acceptance: `officials_confirmed = true`. Transition T09 fires if all officials confirmed → `confirmed`. |
| **Support** | Notification service. |

---

### Phase 8: Match played → mark complete → review

| Layer | Actions |
|---|---|
| **User action** | Post-match, FM marks fixture as complete. Receives review prompt notification. Completes 3-question review within 7 days. |
| **Frontstage** | "Mark as complete" button on fixture detail (enabled when fixture.date < today). Review form: 3 questions, positive framing. Confirmation of submission. |
| **Backstage** | Fixture status `confirmed` → `completed`. `REVIEW_PROMPT` notification fired to both FMs. Review record created on submission. Trust score recalculated. |
| **Support** | Trust calculation service. Review storage (write-once). |

---

## Blueprint B — Post Availability (search-first assumption)

This flow is only initiated when the user has completed a search that returned no useful results. The platform should make this causal link visible.

### Phase 1: Empty search triggers Post Availability

| Layer | Actions |
|---|---|
| **User action** | Completes a search. Sees empty results (or results too distant / incompatible). Decides to post their own availability. |
| **Frontstage** | Empty results state: "No availability found" with explanation and single call to action: "Post your availability." Search parameters are pre-filled into the Post Availability form. |
| **Backstage** | Empty results returned from search. Referral context passed to Post Availability form (pre-populates date, format, home/away from search). |
| **Support** | — |

---

### Phase 2: Post Availability form

| Layer | Actions |
|---|---|
| **User action** | Reviews pre-filled form fields. Adjusts if needed. Sets optional date window (instead of single date). Sets visibility preferences. Submits. |
| **Frontstage** | Post Availability form: date / date window, format, home/away, radius preference, age group, notes (optional). Preview of how availability will appear in search results. Submit. |
| **Backstage** | Availability record created. Fixture record created in `draft` state. Transition T01 fires → fixture moves to `awaiting_opponent`. Availability indexed for search. |
| **Support** | Fixture state machine. Search index update. |

---

### Phase 3: Monitoring availability

| Layer | Actions |
|---|---|
| **User action** | Availability appears in "My availability" list. User monitors for incoming match requests. Receives notifications when a request arrives. |
| **Frontstage** | Availability card: date, format, status ("Awaiting opponent"). Option to edit or withdraw. Link to fixture record. |
| **Backstage** | Availability record in `awaiting_opponent` state. Indexed in search. |
| **Support** | Availability expiry warning at 14 days before expiry (notification T18). |

---

## Blueprint C — Umpire Support Request

### Phase 1: Request initiated

| Layer | Actions |
|---|---|
| **User action** | From fixture detail → "Find support." Selects umpire from club roster. Sends request with fixture context. |
| **Frontstage** | Roster list: umpires available. Select and confirm. Brief message optional (100 char). |
| **Backstage** | Support request record created. Notification `SUPPORT_REQUEST_RECEIVED` to umpire. |

---

### Phase 2: Umpire responds

| Layer | Actions |
|---|---|
| **User action (umpire)** | Receives notification. Views support request detail: fixture date, location, format, requesting club. Accepts or declines. |
| **Frontstage** | Support request detail. Two buttons: Accept / Decline. Decline requires a brief reason (optional). |
| **Backstage** | On accept: `officials_confirmed = true` (if all required officials confirmed). Transition T09 fires if applicable. Notification to FM. On decline: notification to FM; no transition. |

---

## Blueprint D — Trust Review

### Phase 1: Review prompt

| Layer | Actions |
|---|---|
| **User action** | Receives review prompt after fixture marked complete. Clicks through to review form. |
| **Frontstage** | Review prompt in notification. Review form: 3 questions (shown below). |
| **Backstage** | `REVIEW_PROMPT` notification was fired. Review window: 7 days. `REVIEW_REMINDER` fires at 72 hours if not yet submitted. |

**The 3 review questions (Agent 8 to finalise copy — these are structural placeholders):**

1. Did the opposition confirm and attend as agreed? [Yes / Mostly / No]
2. Were communications prompt and reliable throughout? [Yes / Mostly / No]
3. Would you arrange a fixture with this club again? [Yes / Probably / No]

All three use a 3-point scale, not stars. All three are mandatory. The review is private to the platform.

---

### Phase 2: Submission

| Layer | Actions |
|---|---|
| **User action** | Answers 3 questions. Submits. |
| **Frontstage** | Confirmation: "Your review has been recorded. It won't be shared publicly." |
| **Backstage** | Review record stored (write-once; no edits). Trust score recalculated for reviewed team. Trust badge recalculated if threshold crossed. |
| **Support** | Trust calculation service. |

---

## Fail states across all blueprints

| Point of failure | System behaviour | User-facing impact |
|---|---|---|
| Search timeout (> 3s) | Show partial results with "still loading more" indicator | User can act on partial results |
| Match request double-submit | Idempotency key prevents duplicate record | User sees confirmation; second request silently dropped |
| Availability index stale | Fixture may appear available but is already `awaiting_response` | User told "This availability is no longer open" on detail page; redirected back to results |
| Email delivery failure | Retry 3x; fall back to in-app only; alert on persistent failure | User still receives in-app notification; email noted as failed |
| Review submission lost (network) | Client-side draft saved; retry on reconnect | User sees "Saved — submitting when connection restores" |

---

## Timing across the service

| Event | Timing |
|---|---|
| Search results | < 2 seconds |
| Notification delivery (immediate) | < 2 minutes of trigger |
| Notification delivery (digest) | Batched at 08:00 and 18:00 |
| Match request expiry | 7 days; checked daily at 09:00 |
| Review window | 7 days from fixture marked complete |
| Review reminder | 72 hours after REVIEW_PROMPT, if not yet submitted |
| Quiet hours | 22:00–07:00; immediate notifications deferred to 07:00 |
