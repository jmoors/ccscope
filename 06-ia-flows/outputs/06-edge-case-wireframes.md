# 06 — Edge Case Wireframes

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft

This document covers wireframes for states not shown in the primary screen wireframes: error conditions, empty states, boundary conditions, and flows with multiple simultaneous gaps.

---

## EC-01 — Availability already taken (stale search result)

**Context:** User clicks through to availability detail from search results. Between the user loading the results and clicking through, another team sent a match request — locking the availability.

**Trigger:** Availability is in `awaiting_response` when user reaches the detail page.

```
┌────────────────────────────────────────────────────────────┐
│ [← Back to results]                                        │
│                                                            │
│  Thornton CC 1st XI                                        │
│  Sunday 14 June · T20                                      │
│                                                            │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ This availability is no longer open.                 │  │
│  │ Another team has sent a match request                │  │
│  │ and it is currently awaiting their response.         │  │
│  │                                                      │  │
│  │ [Back to results]   [Start a new search]             │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                            │
│  (Team profile summary shown below, in case user wants     │
│   to note the club for future reference.)                  │
│                                                            │
│  Thornton CC 1st XI                                        │
│  T20 · Men's · Open · Tier 3                               │
│  ◆ Reliable                                                │
│  Home ground: Thornton Park                                │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- Do not show a "Send match request" button. It would fail immediately and the user would be confused.
- Show team profile summary anyway — the user may want to note this team for a future search. Frustrating to return empty-handed with no information at all.
- "Back to results" returns to the search results list (preserved). The user does not need to re-search.

---

## EC-02 — Fixture with both venue and officials missing

**Context:** Opponent accepted. Neither team has confirmed a venue. The fixture also requires umpires (non-friendly format). Two gaps must be resolved.

```
┌──────────────────────────────────────────────────────────────┐
│ WHAT'S MISSING                                               │
│                                                              │
│ ✗ Venue        [Confirm venue →]                             │
│   Resolve venue before requesting officials.                 │
│                                                              │
│ ○ Officials    (available after venue confirmed)             │
│   You'll be able to request your umpire once the            │
│   venue is set.                                              │
│                                                              │
│ ✓ Opponent                                                   │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

**Design notes:**
- Two gaps, but the panel shows priority ordering clearly: venue first, then officials.
- The officials row is shown but greyed / marked as "(available after venue confirmed)." This prevents the user from trying to request an umpire before the venue is confirmed — which is a confusing intermediate state.
- This matches the state machine's priority ordering (awaiting_venue before awaiting_officials) but communicates it in plain English.

---

## EC-03 — Multi-team context: ambiguous action

**Context:** Graham manages the 1st XI and the 2nd XI. He receives a notification for an incoming match request but the notification doesn't clearly specify which team. He opens the platform.

**Resolution:** The team context picker always shows which team is active. But on the Requests tab, requests from ALL teams are visible (grouped by team), not filtered to the current context.

```
┌────────────────────────────────────────────────────────────┐
│ [← Dashboard]                   [Graham ▼] [1st XI ▼]    │
│                                                            │
│  Requests                                                  │
│                                                            │
│  THORNTON CC 1st XI                                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Match request from Westfield CC                      │  │
│  │ Sun 14 June · T20                                    │  │
│  │ [View request →]                                     │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                            │
│  THORNTON CC 2nd XI                                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Match request from Redfield CC                       │  │
│  │ Sat 7 June · 40-over                                 │  │
│  │ [View request →]                                     │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- Requests are grouped by team, not filtered by current context. A multi-team FM must see all incoming requests regardless of which team context is active.
- When the user taps through to a 2nd XI request from the 1st XI context, a context-switch happens automatically with a visible confirmation: "Switching to 2nd XI context to view this request."
- This is the only case where context switches happen automatically. All other context switches require explicit user action.

---

## EC-04 — Block flow

**Context:** Graham wants to block Crestview CC after a negative experience (short-notice cancellation, off-platform).

**Access path:** Club profile of Crestview CC → "Block this club" (at bottom, low prominence).

```
┌────────────────────────────────────────────────────────────┐
│ Crestview CC                                               │
│  ─────────────────────────────────────────────────────── │
│  [club profile content above]                              │
│  ─────────────────────────────────────────────────────── │
│                                                            │
│  [Block Crestview CC]    ← text link, low visual weight    │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**On click — confirmation sheet:**

```
┌────────────────────────────────────────────────────────────┐
│                                                            │
│  Block Crestview CC?                                       │
│                                                            │
│  • They will not be able to send you match requests.       │
│  • They will not see your availability in search.          │
│  • They will not be notified that they've been blocked.    │
│                                                            │
│  You can remove the block at any time in your club         │
│  settings.                                                 │
│                                                            │
│  [Block Crestview CC]    [Cancel]                          │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- The block action is intentionally buried — low visual weight, at the bottom of a profile. It is not a common action and should not feel like a featured option.
- The confirmation sheet explains the effect in plain terms and explicitly states that the block is silent ("they will not be notified"). This is intentional per the domain model.
- "You can remove the block at any time" reduces anxiety about the permanence of the action.

---

## EC-05 — Short-notice cancellation warning flow

**Context:** Marcus cancels a confirmed fixture that is 20 hours away (within the 48-hour window).

```
STEP 1 — Initial cancel tapped:

┌────────────────────────────────────────────────────────────┐
│                                                            │
│  Cancel this fixture?                                      │
│                                                            │
│  vs Thornton CC · Saturday 14 June (tomorrow)             │
│                                                            │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ ⚠ This fixture is less than 48 hours away.          │  │
│  │                                                      │  │
│  │ Short-notice cancellations are noted on your         │  │
│  │ team's trust record. This won't show publicly,       │  │
│  │ but repeated short-notice cancellations may          │  │
│  │ affect how your team appears in search results.      │  │
│  │                                                      │  │
│  │ Reason for cancellation:                             │  │
│  │ ┌────────────────────────────────────────────────┐  │  │
│  │ │ Unable to field a team                      ▼  │  │  │
│  │ └────────────────────────────────────────────────┘  │  │
│  │                                                      │  │
│  │ [Cancel fixture]    [Keep the fixture]               │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Reason dropdown options:**
- Unable to field a team
- Ground unavailable
- Opposing team requested cancellation
- Other

**Weather option missing from reason dropdown:**
- If the reason is weather, there is a separate route: "Mark as weather cancellation" (a separate button / option on the fixture detail). This keeps the weather path distinct from the trust-penalty path.

```
STEP 2 — Confirmation (if "Cancel fixture" pressed):

┌────────────────────────────────────────────────────────────┐
│  Fixture cancelled.                                        │
│                                                            │
│  Thornton CC have been notified.                           │
│  A note has been made on your team's trust record.         │
│                                                            │
│  [Back to dashboard]                                       │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- The warning at Step 1 is firm but not shaming. "Won't show publicly" is important — Marcus needs to know this isn't a public penalty.
- "Keep the fixture" is the secondary option, not "Go back." This phrasing makes the consequence more concrete: you're choosing to keep it, not just navigating backwards.
- Reason field is required. It is a structured dropdown, not a free-text box. This prevents the platform from becoming a confessional.

---

## EC-06 — Review form (post-match)

```
┌────────────────────────────────────────────────────────────┐
│  Leave a review for Thornton CC 2nd XI                     │
│  Match on Saturday 14 June                                 │
│                                                            │
│  Your review is private. It helps us maintain              │
│  reliable clubs in the network.                            │
│                                                            │
│  ──────────────────────────────────────────────────────── │
│                                                            │
│  1. Did the opposition confirm and attend as agreed?       │
│                                                            │
│     ○ Yes, everything as planned                           │
│     ○ Mostly — minor issues                                │
│     ○ No — significant problems                            │
│                                                            │
│  ──────────────────────────────────────────────────────── │
│                                                            │
│  2. Were communications prompt and reliable?               │
│                                                            │
│     ○ Yes, always responded quickly                        │
│     ○ Mostly — occasional delays                           │
│     ○ No — hard to reach or unresponsive                   │
│                                                            │
│  ──────────────────────────────────────────────────────── │
│                                                            │
│  3. Would you arrange a fixture with them again?           │
│                                                            │
│     ○ Yes, without hesitation                              │
│     ○ Probably                                             │
│     ○ No                                                   │
│                                                            │
│  ──────────────────────────────────────────────────────── │
│                                                            │
│  All three answers are required.                           │
│                                                            │
│  [Submit review]                                           │
│                                                            │
│  [Not now — I'll do this later]                            │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Post-submission:**

```
┌────────────────────────────────────────────────────────────┐
│  Review submitted.                                         │
│                                                            │
│  Thank you. Your review has been recorded. It will not     │
│  be shared publicly or attributed to you.                  │
│                                                            │
│  [Back to fixture]    [Back to dashboard]                  │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- 3-point scale, not stars. Labels are full phrases, not just "Yes / No" (the nuance in "Mostly" is important for trust calculation accuracy).
- All three required. No optional questions. Keeps the review brief AND meaningful.
- "Not now" is available but the 72-hour reminder will follow. After the reminder, no further prompts.
- Agent 8 must finalise the question wording. These are structural placeholders.
- No open text field. This is intentional per the domain model (no public comments; no comment section).

---

## EC-07 — Fixture Manager leaves club (mid-season)

**Context:** A FM account is deactivated by Club Admin. There are two confirmed fixtures in their name.

**What the remaining Club Admin sees:**

```
┌────────────────────────────────────────────────────────────┐
│  ⚠ ACTION REQUIRED                                         │
│                                                            │
│  Graham Okafor has been removed as Fixture Manager         │
│  for the 2nd XI.                                           │
│                                                            │
│  2 active fixtures need a new Fixture Manager:             │
│                                                            │
│  • vs Westfield CC · 14 June (Confirmed)                   │
│  • Availability posted for 28 June (Awaiting opponent)     │
│                                                            │
│  Assign a new Fixture Manager to the 2nd XI within         │
│  7 days to manage these fixtures.                          │
│                                                            │
│  [Assign Fixture Manager →]                                │
│                                                            │
│  These fixtures remain in their current state until        │
│  reassigned. No match requests will expire during          │
│  this period.                                              │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- The system does not automatically take action. The Club Admin must reassign.
- "No match requests will expire during this period" — this is a grace period guarantee. Prevents the 7-day expiry clock from running out while the admin is scrambling.
- **FLAG for Agent 2:** The grace period behaviour for expired match requests during FM vacancy is not specified in `01-fixture-state-machine.md`. Confirm behaviour before implementing.

---

## EC-08 — Club profile: no Club Admin assigned (emergency state)

This state should never occur in normal operation. But if a Club Admin's account is deleted by platform support, it must be handled.

```
┌────────────────────────────────────────────────────────────┐
│  [PLATFORM ADMIN VIEW ONLY]                                │
│                                                            │
│  Thornton CC has no assigned Club Administrator.           │
│                                                            │
│  Active fixtures: 3                                        │
│  Active Fixture Managers: 1 (Graham Okafor, 2nd XI)        │
│                                                            │
│  Action required:                                          │
│  Assign a Club Administrator manually.                     │
│  No self-service fix available.                            │
│                                                            │
│  [Assign Club Admin] ← platform admin only                 │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Design notes:** This is an admin-only screen. It does not need to be user-facing but must exist in the platform admin interface. The FM-facing experience during this period is unchanged — the FM can still manage fixtures; they just can't access Club Admin functions.

---

## EC-09 — Service Provider: support request already filled

**Context:** Bernard clicks an email link to accept a support request, but another umpire from the roster already accepted (edge case: two umpires both sent requests, both click accept at the same time).

```
┌────────────────────────────────────────────────────────────┐
│  Support request: Westfield Ladies CC, 7 June              │
│                                                            │
│  This request has already been filled.                     │
│  Another official has confirmed for this fixture.          │
│                                                            │
│  No action needed from you.                                │
│                                                            │
│  [Back to your requests]                                   │
└────────────────────────────────────────────────────────────┘
```

**Design notes:** Bernard must not be left confused. "No action needed" is the key phrase. He does not need to know the other umpire's name.

---

## EC-10 — Platform error during match request submission

```
┌────────────────────────────────────────────────────────────┐
│  Send match request to Westfield CC 2nd XI                 │
│                                                            │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Unable to send your request right now.               │  │
│  │                                                      │  │
│  │ Your details have been saved.                        │  │
│  │ Please try again in a moment.                        │  │
│  │                                                      │  │
│  │ [Try again]                                          │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                            │
│  If the problem continues, contact support at              │
│  support@[domain].co.uk                                    │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Design notes:**
- "Your details have been saved" prevents the user from losing their note and re-entering the form.
- No emoji. No "Oops!" No "Something went wrong." Direct statement of the problem and the action.

---

## Summary: all states defined per screen

| Screen | Default | Empty | Loading | Error | Edge cases covered |
|---|:---:|:---:|:---:|:---:|---|
| Dashboard | ✓ | ✓ | ✓ | ✓ | Multi-team requests |
| Find a game | ✓ | n/a | ✓ | n/a | — |
| Search results | ✓ | ✓ | ✓ | n/a | Stale availability (EC-01) |
| Fixture detail | ✓ | n/a | ✓ | n/a | Multi-gap (EC-02), post-date prompt |
| Send match request | ✓ | n/a | n/a | ✓ | Already has pending request; platform error (EC-10) |
| Match request detail | ✓ | n/a | n/a | ✓ | Already expired/withdrawn |
| Review form | ✓ | n/a | n/a | n/a | — |
| Short-notice cancel | n/a | n/a | n/a | n/a | EC-05 |
| Weather cancel | n/a | n/a | n/a | n/a | Map 06 |
| Block flow | n/a | n/a | n/a | n/a | EC-04 |
| FM vacancy | n/a | n/a | n/a | n/a | EC-07 |
| SP stale request | n/a | n/a | n/a | n/a | EC-09 |
