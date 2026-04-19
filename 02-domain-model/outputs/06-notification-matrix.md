# 06 — Notification Matrix

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 2 (Domain Model & Logic)  
**Note:** Template copy and subject lines are Agent 8's responsibility. This document defines events, channels, recipients, and priority — not the words.

---

## 1. Channels

| Channel | ID | Description |
|---|---|---|
| Email | `email` | Sent to the user's registered email address |
| In-app | `in_app` | Displayed in the notification inbox within the platform |
| Push | `push` | Mobile push notification (future; reserved in schema but not implemented in MVP) |

MVP delivers: email + in-app. Push is a v2 concern.

---

## 2. Priority Levels

| Priority | Delivery | Description |
|---|---|---|
| `immediate` | Sent within 2 minutes of event | Time-sensitive; requires prompt action or involves a fixed deadline |
| `digest` | Batched at 08:00 or 18:00 local time | Informational; no action required within hours |

---

## 3. Opt-Out Groups

Users may opt out of notification groups. Some are mandatory (cannot be opted out).

| Group ID | Label | Opt-outable? |
|---|---|---|
| `match_requests` | Match requests and responses | No — mandatory for Fixture Managers |
| `fixture_updates` | Fixture status changes | No — mandatory |
| `support_requests` | Support request activity | Yes |
| `review_prompts` | Post-match review prompts | Yes (but platform will prompt to opt back in after 3 skips) |
| `digest_summary` | Weekly digest of activity | Yes |
| `reminders` | Deadline and expiry reminders | Yes |

---

## 4. Quiet Hours

| Rule | Value |
|---|---|
| Default quiet hours | 22:00 – 07:00 (user's local timezone) |
| Immediate notifications during quiet hours | Deferred to 07:00; not dropped |
| Digest notifications during quiet hours | Not affected (already batched) |
| User can adjust quiet hours | Yes, in notification preferences |

A notification that fires at 23:30 will be delivered at 07:00 the next morning, not at 23:30. The platform stamps `scheduled_for` on deferred notifications.

---

## 5. Digest vs Real-Time Logic

A user with > 10 active fixtures receives digest-mode by default for `review_prompts` and `digest_summary` groups. They can switch to immediate if preferred.

Users with ≤ 10 active fixtures receive immediate notifications for all `immediate` priority events.

---

## 6. Notification Event Table

| Event ID | Trigger | Priority | Group | Channel | Recipient(s) | Template ID |
|---|---|---|---|---|---|---|
| `MATCH_REQUEST_RECEIVED` | Match request sent | immediate | match_requests | email, in_app | Receiving team's FM | `T01` |
| `MATCH_REQUEST_ACCEPTED` | Match request accepted | immediate | match_requests | email, in_app | Sending team's FM | `T02` |
| `MATCH_REQUEST_DECLINED` | Match request declined | immediate | match_requests | email, in_app | Sending team's FM | `T03` |
| `MATCH_REQUEST_WITHDRAWN` | Sending FM withdraws request | immediate | match_requests | email, in_app | Receiving team's FM | `T04` |
| `MATCH_REQUEST_EXPIRED` | 7-day expiry fires | immediate | match_requests | email, in_app | Sending team's FM | `T05` |
| `MATCH_REQUEST_EXPIRY_REMINDER` | 5 days since request sent (48h before expiry) | immediate | reminders | email, in_app | Receiving team's FM | `T06` |
| `FIXTURE_CONFIRMED` | All required slots filled | immediate | fixture_updates | email, in_app | Both teams' FMs | `T07` |
| `VENUE_CONFIRMED` | Venue slot filled | digest | fixture_updates | in_app | Both teams' FMs | `T08` |
| `OFFICIALS_CONFIRMED` | Officials slot filled | digest | fixture_updates | in_app | Both teams' FMs | `T09` |
| `FIXTURE_CANCELLED` | FM cancels > 48h notice | immediate | fixture_updates | email, in_app | Both teams' FMs | `T10` |
| `FIXTURE_CANCELLED_SHORT_NOTICE` | FM cancels ≤ 48h notice | immediate | fixture_updates | email, in_app | Both teams' FMs | `T11` |
| `FIXTURE_CANCELLED_WEATHER` | Weather cancellation | immediate | fixture_updates | email, in_app | Both teams' FMs | `T12` |
| `SUPPORT_REQUEST_RECEIVED` | FM sends support request to umpire | immediate | support_requests | email, in_app | Umpire (SP) | `T13` |
| `SUPPORT_REQUEST_ACCEPTED` | Umpire accepts | immediate | support_requests | email, in_app | Requesting team's FM | `T14` |
| `SUPPORT_REQUEST_DECLINED` | Umpire declines | immediate | support_requests | email, in_app | Requesting team's FM | `T15` |
| `REVIEW_PROMPT` | Fixture marked complete | digest | review_prompts | email, in_app | Both teams' FMs | `T16` |
| `REVIEW_REMINDER` | 72h after REVIEW_PROMPT, no review submitted | digest | reminders | email, in_app | FM who hasn't submitted | `T17` |
| `AVAILABILITY_EXPIRY_WARNING` | 14 days before availability expiry date | digest | reminders | in_app | Publishing team's FM | `T18` |
| `FIXTURE_DATE_REMINDER` | 3 days before confirmed fixture | digest | reminders | email, in_app | Both teams' FMs, Umpires | `T19` |

**Total events: 19**

---

## 7. Per-Recipient Breakdown

### Fixture Manager (own team)

Receives: T01 (if receiving), T02 (if sent), T03 (if sent), T04 (if receiving), T05 (if sent), T06 (if receiving), T07, T08, T09, T10, T11, T12, T13 (sent), T14, T15, T16, T17, T18, T19

### Fixture Manager (opposing team)

Receives: T07, T08, T09, T10, T11, T12, T16, T17, T19

### Service Provider (umpire)

Receives: T13, T19 (for fixtures they are confirmed on)

---

## 8. Event Lifecycle: Full Match Request Sequence

A complete lifecycle for one match coordination, from search to completed review, showing every notification triggered:

```
Day 0, 14:22 — Thornton FM sends match request to Redfield FM
  → MATCH_REQUEST_RECEIVED (T01) → Redfield FM [immediate]

Day 5, 14:22 — 5 days elapsed, no response yet
  → MATCH_REQUEST_EXPIRY_REMINDER (T06) → Redfield FM [immediate]
    ("You have 48 hours to respond to this match request before it expires.")

Day 6, 10:15 — Redfield FM accepts
  → MATCH_REQUEST_ACCEPTED (T02) → Thornton FM [immediate]
  → FIXTURE_CONFIRMED (T07) → both FMs [immediate]
    (Venue already set as Thornton home ground; no officials required for friendly)

Day N-3 (3 days before fixture)
  → FIXTURE_DATE_REMINDER (T19) → both FMs [digest]

Day N — Match played. That evening, Thornton FM marks fixture complete.
  → REVIEW_PROMPT (T16) → both FMs [digest, batched to 18:00]

Day N+3, 18:00 — Redfield FM has not submitted a review
  → REVIEW_REMINDER (T17) → Redfield FM [digest]

Day N+7 — Review window closes. No further notifications.
```

Total notifications in this scenario: 7 events across 2 recipients.

---

## 9. Deduplication Rules

If multiple events fire within 60 seconds for the same recipient, they are batched into a single notification where possible. Specifically:

- `VENUE_CONFIRMED` and `OFFICIALS_CONFIRMED` firing in quick succession → sent as one: "Venue and officials confirmed for your fixture on [date]."
- `FIXTURE_CONFIRMED` supersedes any pending `VENUE_CONFIRMED` or `OFFICIALS_CONFIRMED` in the same 60-second window.

---

## 10. Clubs with ≥ 10 Active Fixtures (High-Volume FMs)

A Fixture Manager managing ≥ 10 simultaneously active fixtures receives:

- `REVIEW_PROMPT` and `REVIEW_REMINDER`: digest only (cannot opt out; only mode changes)
- `AVAILABILITY_EXPIRY_WARNING`: digest only
- `FIXTURE_DATE_REMINDER`: single digest email per day listing all upcoming fixtures within 3 days

`immediate` priority notifications (match requests, cancellations, confirmations) are never digested regardless of volume. These require prompt action.

---

## 11. Template Reference (for Agent 8)

| Template ID | Event | Key variables |
|---|---|---|
| T01 | Match request received | `{requesting_team}`, `{fixture_date}`, `{fixture_format}`, `{deadline_date}`, `{accept_url}`, `{decline_url}` |
| T02 | Match request accepted | `{accepting_team}`, `{fixture_date}`, `{fixture_detail_url}` |
| T03 | Match request declined | `{declining_team}`, `{fixture_date}`, `{search_url}` |
| T04 | Match request withdrawn | `{withdrawing_team}`, `{fixture_date}` |
| T05 | Match request expired | `{target_team}`, `{fixture_date}`, `{search_url}` |
| T06 | Expiry reminder (48h) | `{target_team}`, `{fixture_date}`, `{hours_remaining}`, `{accept_url}`, `{decline_url}` |
| T07 | Fixture confirmed | `{fixture_date}`, `{opponent_team}`, `{venue}`, `{fixture_detail_url}` |
| T08 | Venue confirmed | `{fixture_date}`, `{venue}`, `{fixture_detail_url}` |
| T09 | Officials confirmed | `{fixture_date}`, `{official_name}`, `{fixture_detail_url}` |
| T10 | Fixture cancelled (normal) | `{fixture_date}`, `{cancelling_team}`, `{search_url}` |
| T11 | Fixture cancelled (short notice) | `{fixture_date}`, `{cancelling_team}` |
| T12 | Fixture cancelled (weather) | `{fixture_date}`, `{opponent_team}` |
| T13 | Support request received | `{requesting_team}`, `{fixture_date}`, `{fixture_format}`, `{accept_url}`, `{decline_url}` |
| T14 | Support request accepted | `{official_name}`, `{fixture_date}`, `{fixture_detail_url}` |
| T15 | Support request declined | `{official_name}`, `{fixture_date}` |
| T16 | Review prompt | `{opponent_team}`, `{fixture_date}`, `{review_url}`, `{window_closes}` |
| T17 | Review reminder | `{opponent_team}`, `{fixture_date}`, `{review_url}`, `{window_closes}` |
| T18 | Availability expiry warning | `{fixture_date}`, `{days_until_expiry}`, `{availability_url}` |
| T19 | Fixture date reminder | `{fixture_date}`, `{opponent_team}`, `{venue}`, `{fixture_detail_url}` |
