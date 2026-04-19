# 03 — MVP Scope (Confirmed)

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 1 (Product Foundations)

---

## In scope

### Core fixture flow

| Feature | Description |
|---|---|
| Find a game | Search for existing team availability by date, format, tier, and location. |
| Post availability | Publish your team's availability when search returns nothing useful. |
| Send match request | Send a structured request to a team whose availability you found. |
| Accept / decline match request | Receive, review, and respond to incoming match requests. |
| Fixture detail view | Full record of a fixture showing confirmed parties and what's missing. |
| "What's missing" panel | At-a-glance view of gaps: opponent, venue, officials, teas. |

### Support

| Feature | Description |
|---|---|
| Find support | Request an umpire or scorer from your own club's roster. |
| Support request flow | Send a structured request; receive accept / decline. |

### Trust

| Feature | Description |
|---|---|
| Post-match review | 3-question private review submitted after a completed fixture. |
| Trust badges | New / Reliable / Established shown on club/team profiles. |
| "Needs attention" internal flag | Never shown publicly; used for internal moderation only. |

### Notifications

| Feature | Description |
|---|---|
| Email notifications | Match requests, acceptances, declines, fixture confirmations, review prompts. |
| In-app notifications | Same triggers as email; visible in notification inbox. |

### Club and team management

| Feature | Description |
|---|---|
| Club profile | Name, home ground, contact, active teams. |
| Team profile | Format, tier, home ground, active players/officials on roster. |
| Club Administrator role | Manages club profile and authorises team managers. |

---

## Out of scope (MVP)

| Feature | Rationale |
|---|---|
| Payments / match fees | Adds regulatory complexity (financial services obligations); different problem from coordination. |
| Tours and multi-fixture planning | Compound fixtures require a different data model; low frequency, high complexity. |
| Advertising marketplace | Commercial layer changes the product's trust relationship with users. |
| Open chat / messaging | Moderation overhead; structured request fields remove the need. |
| Review comments (public) | Public comments create reputation risk and require moderation at scale. |
| Sponsorship tools | Separate product category; not relevant to core fixture coordination. |
| League fixture integration beyond import | Live sync with Play-Cricket requires API agreement we don't have; import is sufficient for v1. |
| Open umpire marketplace | Needs density we don't have at launch; club-roster approach is useful without density. |
| Scorer / coach marketplace | Same rationale as umpire marketplace; deferred. |
| Player-level profiles | Individual profiles add privacy complexity without fixture-coordination benefit. |
| Match statistics | Analysis tool, not a coordination tool; separate product. |
| Cross-club messaging threads | See: open chat. Structured flows are sufficient. |

---

## Explicit edge cases — addressed in MVP

| Edge case | Resolution |
|---|---|
| Weather cancellation | Fixture Manager marks fixture Cancelled; both parties notified; availability is not automatically reposted. |
| Short-notice cancellation (< 48 hours) | Triggers review prompt with a specific cancellation question; feeds "Needs attention" flag internally. |
| Team blocks another team | Block is silent (blocked team is not notified); blocked team cannot send future match requests to blocker. |
| No response to match request | Request expires after 7 days; sending team notified; fixture returns to Awaiting opponent status. |
| Fixture with missing venue confirmed by both teams | Fixture state reflects gap ("Awaiting venue"); both parties can see and act; no automatic hold. |
| Club with no completed fixtures (new entrant) | Shown with "New" badge; not penalised in search ranking. |
| Two teams both post availability for the same date | Both remain in search; either can initiate a match request to the other. |

---

## Explicit edge cases — deferred

| Edge case | Rationale |
|---|---|
| Dispute resolution (e.g., claims of misconduct) | Requires human moderation process; not technically complex but operationally not ready. |
| Rain-affected partial fixtures (review prompt) | Ambiguous status (was the match "completed"?); defer until we have usage data on frequency. |
| Team mergers / club splits | Rare; data model complexity high; handle manually in v1. |
| International or expatriate clubs | UK-only for MVP; geography/timezone handling deferred. |
| Colts / junior fixtures | Safeguarding requirements require separate policy work before we can accommodate. |

---

## Scope change process

1. Any agent who believes a scope change is needed posts a proposal to `shared/DECISION_LOG.md` with status "Proposed".
2. Agent 1 reviews and responds within 48 hours.
3. Changes affecting two or more agents require acknowledgement from all affected agents before status moves to "Accepted".
4. Accepted scope changes propagate: Agent 1 updates this document; affected agents update their own artefacts.
5. No agent unilaterally expands scope. If it isn't in this document, it isn't in scope.
