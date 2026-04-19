# 03 — Notification Templates

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 8 (Content & Microcopy)
**Source:** Agent 2 notification matrix (`02-domain-model/outputs/06-notification-matrix.md`)
**Channels:** Email + in-app (MVP). Push reserved for v2.

**Format note:**
- `{variable}` = dynamic token. Full variable list per template is in the source matrix.
- Subject line: the fact, precisely. No platform cheerfulness.
- Preheader: adds context, does not repeat subject.
- Body: plain text first; HTML rendering handled by Agent 9/platform.
- All copy: UK English, sentence case.
- Sign-off: platform name only, no "The Team" framing.

---

## T01 — Match request received

**Event:** `MATCH_REQUEST_RECEIVED`
**Recipient:** Receiving team's fixture manager
**Priority:** Immediate
**Group:** `match_requests` (mandatory)

**Subject:**
> {requesting_team} has sent you a match request for {fixture_date}

**Preheader:**
> {fixture_format} · Respond by {deadline_date}

**In-app label:**
> Match request from {requesting_team}

**Email body:**
```
{requesting_team} has sent you a match request for {fixture_date}.

Details:
  Format: {fixture_format}
  Date: {fixture_date}
  Home or away: {home_or_away}
  Their note: {note_text}

Respond by {deadline_date}. If you do not respond, the request will expire.

[Accept request]    [Decline request]

Or view the full request: {accept_url}
```

**Platform sign-off:** `[Platform name]`

**Notes:**
- If `{note_text}` is empty, omit the "Their note" line entirely.
- Both CTA links must deep-link without requiring re-login for recipients already signed in.

---

## T02 — Match request accepted

**Event:** `MATCH_REQUEST_ACCEPTED`
**Recipient:** Sending team's fixture manager
**Priority:** Immediate
**Group:** `match_requests`

**Subject:**
> {accepting_team} accepted your match request — fixture on {fixture_date} confirmed

**Preheader:**
> View your fixture for details and next steps.

**In-app label:**
> {accepting_team} accepted your match request

**Email body:**
```
{accepting_team} has accepted your match request for {fixture_date}.

Your fixture is confirmed.

  Date: {fixture_date}
  Format: {fixture_format}
  Venue: {venue_name}
  Opposition: {accepting_team}

View fixture: {fixture_detail_url}
```

---

## T03 — Match request declined

**Event:** `MATCH_REQUEST_DECLINED`
**Recipient:** Sending team's fixture manager
**Priority:** Immediate
**Group:** `match_requests`

**Subject:**
> {declining_team} has declined your match request for {fixture_date}

**Preheader:**
> Search for another team with availability on that date.

**In-app label:**
> {declining_team} declined your match request

**Email body:**
```
{declining_team} has declined your match request for {fixture_date}.

You can search for other teams with availability on that date.

Find a game: {search_url}
```

**Notes:**
- Do not speculate about why. Do not say "unfortunately" or "sorry".
- The search URL should pre-fill the original search date and format.

---

## T04 — Match request withdrawn

**Event:** `MATCH_REQUEST_WITHDRAWN`
**Recipient:** Receiving team's fixture manager (the one who was going to accept or decline)
**Priority:** Immediate
**Group:** `match_requests`

**Subject:**
> {withdrawing_team} has withdrawn their match request for {fixture_date}

**Preheader:**
> No action is needed from you.

**In-app label:**
> {withdrawing_team} withdrew their match request

**Email body:**
```
{withdrawing_team} has withdrawn their match request for {fixture_date}. No action is needed.
```

**Notes:**
- Keep brief. The recipient had no outstanding obligation.

---

## T05 — Match request expired

**Event:** `MATCH_REQUEST_EXPIRED`
**Recipient:** Sending team's fixture manager
**Priority:** Immediate
**Group:** `match_requests`

**Subject:**
> Your match request to {target_team} for {fixture_date} has expired

**Preheader:**
> The 7-day response window has passed.

**In-app label:**
> Match request to {target_team} expired

**Email body:**
```
Your match request to {target_team} for {fixture_date} was not answered within 7 days and has expired.

If you still need a game on that date, search for other teams with availability.

Find a game: {search_url}
```

---

## T06 — Expiry reminder (48 hours)

**Event:** `MATCH_REQUEST_EXPIRY_REMINDER`
**Recipient:** Receiving team's fixture manager
**Priority:** Immediate
**Group:** `reminders`

**Subject:**
> Match request from {requesting_team} — {hours_remaining} hours left to respond

**Preheader:**
> For {fixture_date}. Accept or decline before the request expires.

**In-app label:**
> Match request expires in {hours_remaining} hours

**Email body:**
```
You have a match request from {requesting_team} for {fixture_date} that expires in {hours_remaining} hours.

If you do not respond, the request will expire automatically.

  Format: {fixture_format}
  Date: {fixture_date}
  Their note: {note_text}

[Accept request]    [Decline request]

Or view the request: {accept_url}
```

**Notes:**
- Omit "Their note" if empty.
- `{hours_remaining}` is calculated from the time the reminder fires. Typically 48, but may be less if delivery was deferred by quiet hours.

---

## T07 — Fixture confirmed

**Event:** `FIXTURE_CONFIRMED`
**Recipients:** Both teams' fixture managers
**Priority:** Immediate
**Group:** `fixture_updates` (mandatory)

**Subject:**
> Fixture confirmed — {fixture_date} vs {opponent_team}

**Preheader:**
> At {venue_name}. View your fixture for full details.

**In-app label:**
> Fixture confirmed — {fixture_date}

**Email body:**
```
Your fixture on {fixture_date} is confirmed.

  Date: {fixture_date}
  Format: {fixture_format}
  Venue: {venue_name}
  Opposition: {opponent_team}

View fixture: {fixture_detail_url}
```

---

## T08 — Venue confirmed

**Event:** `VENUE_CONFIRMED`
**Recipients:** Both teams' fixture managers
**Priority:** Digest
**Group:** `fixture_updates`
**Channel:** In-app only

**In-app label:**
> Venue confirmed — {fixture_date}

**In-app body:**
> {venue_name} confirmed for {fixture_date} vs {opponent_team}.

**Notes:**
- Email not sent for this event (digest/in-app only per notification matrix).
- May be batched with T09 if both fire within 60 seconds — see deduplication rule in notification matrix.

---

## T09 — Officials confirmed

**Event:** `OFFICIALS_CONFIRMED`
**Recipients:** Both teams' fixture managers
**Priority:** Digest
**Group:** `fixture_updates`
**Channel:** In-app only

**In-app label:**
> Umpire confirmed — {fixture_date}

**In-app body:**
> {official_name} confirmed as umpire for {fixture_date} vs {opponent_team}.

**Notes:**
- Email not sent for this event.
- May be batched with T08 — combined in-app label: `Venue and umpire confirmed — {fixture_date}`

---

## T10 — Fixture cancelled (standard notice)

**Event:** `FIXTURE_CANCELLED`
**Trigger:** Cancellation with more than 48 hours' notice
**Recipients:** Both teams' fixture managers
**Priority:** Immediate
**Group:** `fixture_updates`

**Subject:**
> Fixture on {fixture_date} has been cancelled

**Preheader:**
> Cancelled by {cancelling_team}.

**In-app label:**
> Fixture cancelled — {fixture_date}

**Email body:**
```
The fixture on {fixture_date} has been cancelled by {cancelling_team}.

If you still need a game on that date, search for other teams with availability.

Find a game: {search_url}
```

---

## T11 — Fixture cancelled (short notice, ≤ 48 hours)

**Event:** `FIXTURE_CANCELLED_SHORT_NOTICE`
**Recipients:** Both teams' fixture managers
**Priority:** Immediate
**Group:** `fixture_updates`

**Subject:**
> Fixture on {fixture_date} has been cancelled — short notice

**Preheader:**
> Cancelled by {cancelling_team} with less than 48 hours' notice.

**In-app label:**
> Fixture cancelled at short notice — {fixture_date}

**Email body:**
```
The fixture on {fixture_date} has been cancelled by {cancelling_team} with less than 48 hours' notice.

Short-notice cancellations are recorded on {cancelling_team}'s trust record.
```

**Notes:**
- Do not editoralise. The short-notice flag is recorded; this message states the fact.
- Do not say "unfortunately". Do not speculate on reason.
- Do not prompt to find another game — there may not be time.

---

## T12 — Fixture cancelled (weather)

**Event:** `FIXTURE_CANCELLED_WEATHER`
**Recipients:** Both teams' fixture managers
**Priority:** Immediate
**Group:** `fixture_updates`

**Subject:**
> Fixture on {fixture_date} has been cancelled — weather

**Preheader:**
> Marked as a weather cancellation. No trust impact.

**In-app label:**
> Fixture cancelled (weather) — {fixture_date}

**Email body:**
```
The fixture on {fixture_date} with {opponent_team} has been cancelled due to weather. Weather cancellations do not affect either team's trust record.
```

**Notes:**
- Explicitly state no trust impact. This is a meaningful distinction from T10/T11.

---

## T13 — Support request received (umpire)

**Event:** `SUPPORT_REQUEST_RECEIVED`
**Recipient:** Umpire (service provider)
**Priority:** Immediate
**Group:** `support_requests`

**Subject:**
> Umpiring request for {fixture_date} from {requesting_team}

**Preheader:**
> {fixture_format} at {venue_name}. Respond by {deadline_date}.

**In-app label:**
> Umpire request for {fixture_date}

**Email body:**
```
{requesting_team} has sent you an umpiring request for {fixture_date}.

  Date: {fixture_date}
  Format: {fixture_format}
  Venue: {venue_name}
  Their note: {note_text}

Respond by {deadline_date}.

[Accept]    [Decline]

Or view the request: {accept_url}
```

**Notes:**
- Omit "Their note" if empty.

---

## T14 — Support request accepted

**Event:** `SUPPORT_REQUEST_ACCEPTED`
**Recipient:** Requesting team's fixture manager
**Priority:** Immediate
**Group:** `support_requests`

**Subject:**
> {official_name} accepted your umpiring request for {fixture_date}

**Preheader:**
> Your fixture on {fixture_date} now has an umpire confirmed.

**In-app label:**
> {official_name} accepted your umpire request

**Email body:**
```
{official_name} has accepted your umpiring request for {fixture_date}.

View fixture: {fixture_detail_url}
```

---

## T15 — Support request declined

**Event:** `SUPPORT_REQUEST_DECLINED`
**Recipient:** Requesting team's fixture manager
**Priority:** Immediate
**Group:** `support_requests`

**Subject:**
> {official_name} is not available for {fixture_date}

**Preheader:**
> You can request another umpire from your club's roster.

**In-app label:**
> {official_name} declined your umpire request

**Email body:**
```
{official_name} is not available for {fixture_date}.

If your club's roster has other umpires, you can send them a request from your fixture detail page.
```

**Notes:**
- "Is not available" rather than "has declined" — preserves the umpire's dignity; they may have a prior commitment.

---

## T16 — Review prompt

**Event:** `REVIEW_PROMPT`
**Recipients:** Both teams' fixture managers
**Priority:** Digest (batched to 18:00)
**Group:** `review_prompts`

**Subject:**
> Post-match review for {fixture_date} — {opponent_team}

**Preheader:**
> Review window closes {window_closes}. Takes about one minute.

**In-app label:**
> Review due — {fixture_date}

**Email body:**
```
Your fixture on {fixture_date} with {opponent_team} has been completed.

Leave a review to contribute to {opponent_team}'s trust record. Your review is private and will never be shown publicly.

Review window closes {window_closes}.

Leave a review: {review_url}
```

---

## T17 — Review reminder

**Event:** `REVIEW_REMINDER`
**Trigger:** 72 hours after T16, no review submitted
**Recipient:** FM who hasn't submitted
**Priority:** Digest
**Group:** `reminders`

**Subject:**
> Reminder: review for {fixture_date} — window closes {window_closes}

**Preheader:**
> Your review of {opponent_team} has not been submitted yet.

**In-app label:**
> Review reminder — {fixture_date}

**Email body:**
```
A reminder that your review of {opponent_team} for the {fixture_date} fixture has not been submitted.

The review window closes on {window_closes}. After that, you will not be able to submit a review for this fixture.

Leave a review: {review_url}
```

**Notes:**
- Only one reminder per fixture. Do not send further reminders.

---

## T18 — Availability expiry warning

**Event:** `AVAILABILITY_EXPIRY_WARNING`
**Trigger:** 14 days before availability expiry
**Recipient:** Publishing team's fixture manager
**Priority:** Digest
**Channel:** In-app only

**In-app label:**
> Availability for {fixture_date} expires in {days_until_expiry} days

**In-app body:**
> Your availability for {fixture_date} will be removed from search results in {days_until_expiry} days. Extend or remove it from My availability.

---

## T19 — Fixture date reminder

**Event:** `FIXTURE_DATE_REMINDER`
**Trigger:** 3 days before confirmed fixture
**Recipients:** Both teams' fixture managers; confirmed umpires
**Priority:** Digest
**Group:** `reminders`

**Subject:**
> Fixture reminder — {fixture_date} vs {opponent_team}

**Preheader:**
> At {venue_name}. Three days to go.

**In-app label:**
> Fixture in 3 days — {fixture_date}

**Email body (fixture manager):**
```
Reminder: your fixture with {opponent_team} is on {fixture_date}.

  Date: {fixture_date}
  Format: {fixture_format}
  Venue: {venue_name}
  Opposition: {opponent_team}

View fixture: {fixture_detail_url}
```

**Email body (umpire variant):**
```
Reminder: you are confirmed as umpire for the fixture on {fixture_date}.

  Date: {fixture_date}
  Format: {fixture_format}
  Venue: {venue_name}
  Home team: {home_team}

View fixture: {fixture_detail_url}
```

**Notes for high-volume FMs (≥ 10 active fixtures):** Per notification matrix section 10, this is batched into a single daily digest listing all fixtures within the 3-day window. The digest subject is:

> `{count} fixtures in the next 3 days`

Body lists each fixture on its own line: `{fixture_date} vs {opponent_team} at {venue_name} — {fixture_detail_url}`

---

## Deduplication (per notification matrix rule)

When `VENUE_CONFIRMED` (T08) and `OFFICIALS_CONFIRMED` (T09) fire within 60 seconds:

**Combined in-app label:**
> Venue and umpire confirmed — {fixture_date}

When `FIXTURE_CONFIRMED` (T07) supersedes a pending T08 or T09 in the same 60-second window, only T07 is sent.

---

*Template IDs T01–T19 match the notification matrix in `02-domain-model/outputs/06-notification-matrix.md`.*
*Agent 9 implements delivery; variables listed per template map to those in the matrix section 11.*
