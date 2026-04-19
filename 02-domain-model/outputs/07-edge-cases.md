# 07 — Edge-Case Handling

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 2 (Domain Model & Logic)  
**Status:** Draft — dispute handling marked deferred per Agent 1 decision

---

## Format

Each edge case covers:

- **Trigger** — what causes this situation to arise
- **Flow** — step-by-step system behaviour
- **State changes** — fixture and related record transitions
- **Notifications** — which events fire (reference `06-notification-matrix.md`)
- **Trust implications** — effect on either team's trust record
- **Open questions / escalation** — any flag for Agent 1 or Agent 4

---

## EC-01: Fixture Cancelled by Home Team (> 48h notice)

**Trigger:** The home team's Fixture Manager cancels a fixture while the fixture is in `awaiting_venue`, `awaiting_officials`, or `confirmed` state, with more than 48 hours remaining before the fixture date.

**Flow:**

1. FM selects "Cancel fixture" and provides a reason (optional free text, not surfaced to opponent).
2. Platform records `cancellation.initiating_team_id = home_team_id`, `cancellation.notice_hours > 48`, `cancellation.weather = false`.
3. Fixture transitions to `cancelled`.
4. Both teams' Fixture Managers are notified: `FIXTURE_CANCELLED` (T10).
5. Away team's availability for that date is not automatically restored — away team must manually post new availability if they wish to find a replacement.
6. Home team's availability is not automatically reposted.

**State changes:**

| Record | Change |
|---|---|
| fixture.status | → `cancelled` |
| fixture.cancellation | Created with reason, initiating_team_id, notice_hours |
| Away team's availability | No change (was already `filled`/closed when opponent was confirmed) |

**Notifications:** `FIXTURE_CANCELLED` (T10) → both FMs

**Trust implications:** No trust penalty. Notice period was sufficient. No synthetic review injected.

**Note:** Both teams lose the fixture. If the away team wishes to find a replacement game for that date, they must manually post new availability. The platform could nudge them (digest notification suggesting they post availability) — this is a v2 UX improvement, not required for MVP.

---

## EC-02: Fixture Cancelled by Away Team (> 48h notice)

**Trigger:** The away team's Fixture Manager cancels.

**Flow:** Identical to EC-01 but `cancellation.initiating_team_id = away_team_id`.

**State changes:** As EC-01.

**Notifications:** `FIXTURE_CANCELLED` (T10) → both FMs

**Trust implications:** No trust penalty. Same rule regardless of which party cancels.

**Note on "home team loses their ground booking":** The platform is not responsible for venue booking consequences. The home team must manage their own ground obligations outside the platform.

---

## EC-03: Short-Notice Cancellation (≤ 48h, either team, non-weather)

**Trigger:** Either FM cancels with ≤ 48 hours until the fixture date. Non-weather reason.

**Flow:**

1. FM selects "Cancel fixture". Platform detects `fixture.date - now ≤ 48 hours`.
2. Platform presents a warning: "This is a short-notice cancellation. It will be recorded on your club's trust record."
3. FM confirms cancellation.
4. `cancellation.short_notice = true`, `cancellation.weather = false` recorded.
5. Fixture transitions to `cancelled`.
6. Synthetic review injected for the cancelling team: `review_score = 0.0` (all three dimensions fail).
7. Both FMs notified: `FIXTURE_CANCELLED_SHORT_NOTICE` (T11).
8. Opposing team may optionally submit a review within 7 days (review window is opened, triggered by the `completed` event on a cancelled-short-notice fixture).

**State changes:**

| Record | Change |
|---|---|
| fixture.status | → `cancelled` |
| fixture.cancellation | short_notice = true, weather = false |
| trust record (cancelling team) | Synthetic review_score = 0.0 appended |

**Notifications:** `FIXTURE_CANCELLED_SHORT_NOTICE` (T11) → both FMs

**Trust implications:**

- Cancelling team: synthetic review_score = 0.0 injected. This counts toward their N and raw_sum.
- Receiving team: no trust impact.
- If the receiving team also submits an optional review (choosing to), it is a standard review with their honest scores.

**Second short-notice cancellation in a season:** If the cancelling club has ≥ 2 short-notice cancellations in a 12-month window, internal "Needs attention" threshold review is triggered. Platform moderation team is alerted (out of scope for automated action in MVP).

---

## EC-04: Weather Cancellation (Mutual)

**Trigger:** Either FM marks the fixture as a weather cancellation. This is a special cancellation type.

**Flow:**

1. FM selects "Cancel fixture — weather" from fixture detail. Available within 48h of the fixture date (field is hidden earlier to prevent misuse as a penalty escape).
2. Platform records `cancellation.weather = true`, `cancellation.short_notice = true` (the timing is still short-notice, but the weather flag overrides trust penalties).
3. Fixture transitions to `cancelled`.
4. Both FMs notified: `FIXTURE_CANCELLED_WEATHER` (T12).
5. No synthetic review injected for either team.
6. No review window opened (weather cancellations produce no review prompts — there is nothing to review).

**State changes:**

| Record | Change |
|---|---|
| fixture.status | → `cancelled` |
| fixture.cancellation | weather = true, short_notice = true |
| trust records | No change |

**Notifications:** `FIXTURE_CANCELLED_WEATHER` (T12) → both FMs

**Trust implications:** None. Weather cancellations are shared misfortune.

**Abuse risk:** A team might claim "weather" to escape a short-notice cancellation penalty. Mitigation:

- The weather-cancel option only appears within the 48h window (you can't weather-cancel a week ahead).
- The system does not verify weather — it relies on honesty. Persistent misuse could be flagged by the opposing team via a support contact, but this is a moderation concern, not an algorithm concern.
- The opposing team may note the weather excuse in informal context; the platform does not verify it.

---

## EC-05: Weather Rearrangement to New Date

**Trigger:** A fixture has been cancelled due to weather and both teams wish to reschedule.

**Flow:**

The platform does not have a native "reschedule" action in MVP. Rearrangement is handled as a new availability/match-request flow:

1. Either FM cancels the current fixture as a weather cancellation (EC-04).
2. Either FM posts new availability for a new date.
3. The other team finds the availability (or they exchange details out-of-band and one team sends a match request directly).
4. A new fixture record is created via the standard flow.
5. The two fixture records are not linked in MVP. Linking rearrangements is a v2 feature.

**Notation on the original fixture:** The `cancellation.weather = true` flag is retained. The original fixture record is immutable after cancellation. The new fixture is a standalone record.

**Note for Agent 6/7:** The rearrangement flow is a known friction point. A "suggest a new date" button on the weather cancellation confirmation screen is a viable v2 improvement but out of scope here.

---

## EC-06: No-Show

**Trigger:** A confirmed fixture's date passes and one team does not arrive. The other team marks the fixture complete.

**Definition of no-show:** One or both teams did not attend at all. Captured via the review process, not via a dedicated no-show flag.

**Flow:**

1. Fixture date passes.
2. Attending team's FM marks fixture complete (even though the game did not happen — they were present).
3. Review prompt fires for both FMs.
4. Attending team submits review with No/No/No (all three questions fail for the non-attending team).
5. Non-attending team may or may not submit a review.
6. Trust scores updated based on submitted reviews.

**State changes:**

| Record | Change |
|---|---|
| fixture.status | → `completed` |
| trust record (non-attending team) | Receiving review_score = 0.0 from attending team |

**Notifications:** `REVIEW_PROMPT` (T16) → both FMs

**Trust implications:**

- The no-show team receives a 0.0 review from the attending team. This is a hard hit on their Bayesian score.
- No automatic no-show flag beyond what the review captures. The review is sufficient.
- If the no-show team also cancels within 48h (platform-side) this triggers EC-03 in addition.

**Note:** The platform cannot detect no-shows automatically. It relies on the attending team marking the fixture complete and submitting an honest review. This is consistent with the product principle of trusting human relationships.

---

## EC-07: Partial No-Show (Team Arrived Short)

**Trigger:** A team arrives with fewer than the required number of players (e.g., 6 out of 11).

**Definition:** The fixture was played (or attempted) with a depleted team. This is not a no-show; it is a preparedness failure.

**Flow:**

1. Fixture played (or called off due to numbers). Either FM marks complete.
2. Review prompt fires for both FMs.
3. Opposing FM may score Q_PREPAREDNESS as "No" or "Mostly" to reflect the depleted attendance.
4. All other questions scored honestly.

**State changes:** Fixture transitions to `completed` via normal flow.

**Notifications:** `REVIEW_PROMPT` (T16) → both FMs

**Trust implications:** The partial no-show is captured through Q_PREPAREDNESS in the review. No separate mechanism required. The reviewing FM's discretion applies — "Mostly" may be appropriate if the team made a reasonable effort despite unavoidable absences; "No" if the shortfall was large and unannounced.

---

## EC-08: Abandoned Mid-Match

**Trigger:** A match begins but is abandoned before completion (e.g., light, weather after play starts, safety incident).

**Flow:**

1. Match is abandoned during play.
2. The next day (or same day), either FM marks the fixture complete on the platform. There is no "abandoned" state — the platform does not distinguish between a full game and an abandoned one.
3. Review prompt fires. FMs review honestly — Q_RELIABILITY should be "Yes" (the fixture did go ahead; the abandonment was not a reliability failure by either team) or "Mostly" if one team's behaviour contributed.
4. Standard review flow proceeds.

**State changes:** `confirmed` → `completed` via T10.

**Notifications:** `REVIEW_PROMPT` (T16) → both FMs

**Trust implications:** Determined entirely by the reviews submitted. An abandonment due to weather with no behavioural issues from either team should result in honest positive reviews. An abandonment due to dispute should result in lower scores.

**Deferred:** Rain-affected partial fixtures (where it is ambiguous whether the game "counts") are explicitly deferred per `03-mvp-scope-confirmed.md`. The MVP handling is: if the match started, it's completed; FM marks it complete.

---

## EC-09: Dispute (Conflicting or Concerning Reviews)

**Trigger:** Two teams submit reviews for the same fixture that describe a serious conflict (e.g., one submits No/No/No; the other submits Yes/Yes/Yes, or both submit all No).

**MVP handling:**

Disputes are explicitly deferred from MVP (per `03-mvp-scope-confirmed.md`). The review algorithm handles conflicting reviews purely mathematically — each review is added to the respective club's record. The platform does not adjudicate.

**What the platform does:**

1. Reviews are submitted and scored normally.
2. No dispute notification is sent to either party.
3. No moderation process is triggered automatically.
4. If a club's score drops below the "Needs attention" threshold (bayesian_score < 0.45, N ≥ 3), an internal flag is set and a platform moderation queue entry is created for human review.

**What the platform does NOT do in MVP:**

- No dispute resolution process
- No ability for clubs to contest a review
- No mediation flow
- No notifications to either club that a concern exists

**Escalation trigger for Agent 1:** If post-launch usage reveals that conflicting reviews are common enough to undermine trust in the system, a dispute resolution flow must be scoped. Flag when this pattern emerges in analytics.

---

## EC-10: Club Blocks Another Club

**Trigger:** A Fixture Manager or Club Admin activates a block against another club.

**Flow:**

1. FM or CA navigates to the blocking club's profile (or a fixture where they were involved) and selects "Block this club."
2. A `Block` record is created: `{blocking_club_id, blocked_club_id, created_at}`.
3. No notification is sent to the blocked club (block is silent — per `shared/DECISION_LOG.md`).
4. The blocked club's availability no longer appears in the blocking club's search results.
5. The blocked club cannot send match requests to the blocking club.
6. If the blocked club sends a match request to the blocking club (before the block was created, e.g., a race condition), the request is silently declined server-side with a generic error: "This team is not available for requests." No information about the block is disclosed.

**State changes:**

| Record | Change |
|---|---|
| Block record | Created |
| Search results | Blocked club filtered out for blocking club |
| Match requests | Blocked club cannot initiate toward blocking club |

**Notifications:** None.

**Trust implications:** None. Blocking is a safety and comfort mechanism, not a trust signal.

**Reversibility:** The blocking club may remove the block at any time. Removal is immediate. No log of removed blocks is shown to the previously blocked club.

**Mutual block:** If Club A blocks Club B AND Club B blocks Club A, each club's block record is independent. Both blocks remain even if one is removed.

**Existing in-progress fixture at time of blocking:** If a confirmed fixture exists between two clubs and one then blocks the other, the block does NOT cancel the fixture. The fixture proceeds. The block prevents future interactions only. This is the correct behaviour — retroactively affecting existing fixtures would be confusing and disproportionate.

---

## EC-11: Fixture Manager Leaves Club Mid-Season

**Trigger:** A Fixture Manager's account is removed from the club, or they resign from the role, while they have active fixtures assigned to them.

**Flow:**

1. Club Admin removes the FM's role assignment (or the FM requests removal).
2. Platform checks for active fixtures associated with this FM's team.
3. If active fixtures exist: Platform sends a notification to the Club Admin: "One or more active fixtures are assigned to [Name], who is no longer a Fixture Manager. Please reassign the Fixture Manager role for [Team]."
4. The active fixtures enter a **grace period** of 7 days:
   - Fixtures in `awaiting_opponent` or `awaiting_response`: no action is taken; they remain in their states.
   - Fixtures in `awaiting_venue`, `awaiting_officials`, or `confirmed`: they remain; neither party is notified.
   - Fixture Managers from the opposing teams are NOT notified about the internal role change.
5. After 7 days without reassignment:
   - Match requests in `awaiting_response` expire normally (their own 7-day expiry clock runs independently).
   - Confirmed fixtures remain confirmed; they are not automatically cancelled.
   - Platform sends a second escalation to Club Admin if active fixtures remain unmanaged.
6. Club Admin assigns a new FM to the team.
7. The new FM inherits all active fixtures associated with that team.

**State changes:**

| Record | Change |
|---|---|
| UserRole | FM's role_type changed from `fixture_manager` to removed |
| Active fixtures | No status change; orphaned for up to 7 days |
| New FM assignment | New UserRole record created |

**Notifications:**

- Immediate: notification to Club Admin that a Fixture Manager has been removed with active fixtures.
- Day 7: escalation notification to Club Admin if fixtures still unmanaged.
- Opposing teams: no notification.

**Trust implications:** None. The role change is internal to the club. Fixtures that proceed or are managed by the new FM continue normally.

**Edge case within edge case:** If the leaving FM is also the Club Admin, they cannot remove themselves if they are the last Admin. The platform must prevent this. A Club Admin can only be removed by another Club Admin or by platform support.

---

## EC-12: Duplicate Availability Detected

**Trigger:** A Fixture Manager attempts to post availability for a date when their team already has an active availability record (or a confirmed fixture) for the same date.

**Flow:**

**Case A: Availability already posted for same date**

1. FM attempts to post availability for 14 June.
2. Platform detects an existing `active` availability record for this team on 14 June.
3. Platform shows a warning: "You already have availability posted for this date. Publishing again would create a duplicate."
4. FM is offered: (a) view existing availability, (b) post anyway (if the date is a long window and multiple games are possible — e.g., an all-day festival), (c) cancel.
5. If FM posts anyway, both availability records are visible in search. Note: this is by design for teams that can play twice in a day (rare but valid for festival formats).

**Case B: Confirmed fixture already exists for same date**

1. FM attempts to post availability for 14 June.
2. Platform detects a confirmed fixture for 14 June.
3. Platform shows a warning: "You have a confirmed fixture on this date. Are you sure you want to post availability for another game on the same day?"
4. If FM confirms: availability is posted. (Some clubs field multiple elevens on the same day; the platform does not prevent this.)
5. If FM cancels: no action.

**State changes:** No automatic state change. The warning is informational only; the FM makes the decision.

**Notifications:** None.

**Trust implications:** None. Duplicate posting is a user error or legitimate multi-game scenario; the platform warns but does not penalise.

**Deduplication in search:** When a club appears twice in search results for the same date (two availability records), both are shown. The search results label each with the team name and format. Opposing FMs can see this; they send a request to one availability only.

---

## End-to-End Flow: EC-03 + EC-09 Combination

**Scenario:** Redfield CC cancels 30 hours before a fixture. Opposing team, Thornton CC, submits a No/No/No review. Redfield's FM claims foul play and refuses to submit a review.

| Step | System action |
|---|---|
| 1 | Redfield FM cancels 30h before fixture date → EC-03 fires |
| 2 | Synthetic review_score = 0.0 injected for Redfield |
| 3 | Thornton FM receives `FIXTURE_CANCELLED_SHORT_NOTICE` notification |
| 4 | Review window opened for Thornton FM (optional review) |
| 5 | Thornton FM submits No/No/No → review_score = 0.0 added to Redfield's record |
| 6 | Redfield FM does not submit a review for Thornton (no impact on Thornton's score) |
| 7 | Redfield now has 2 × 0.0 reviews (synthetic + Thornton's); their bayesian_score drops significantly |
| 8 | If this brings Redfield's bayesian_score below 0.45 and N ≥ 3: internal "Needs attention" flag set |

**What Redfield cannot do:** Contest the synthetic review. Moderation escalation is possible if Redfield believes the cancellation was due to exceptional circumstances, but this is a manual moderation action, not an automated appeal flow in MVP.

---

## Summary: Trust Implications Reference Table

| Edge case | Cancelling/failing team | Other team |
|---|---|---|
| EC-01 (cancelled, > 48h) | No impact | No impact |
| EC-02 (cancelled, > 48h) | No impact | No impact |
| EC-03 (short-notice cancel) | Synthetic review_score = 0.0 | Optional review submitted |
| EC-04 (weather) | No impact | No impact |
| EC-05 (rearrangement) | No impact | No impact |
| EC-06 (no-show) | Review_score = 0.0 from attending team | No impact |
| EC-07 (partial no-show) | Q_PREPAREDNESS likely "No" or "Mostly" | No impact |
| EC-08 (abandoned) | Depends on reviews submitted | Depends on reviews submitted |
| EC-09 (dispute) | Depends on reviews submitted | Depends on reviews submitted |
| EC-10 (block) | No impact | No impact |
| EC-11 (FM leaves) | No impact | No impact |
| EC-12 (duplicate posting) | No impact | No impact |
