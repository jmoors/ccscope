# 04 — Success Metrics

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 1 (Product Foundations)  
**Instrumentation owner:** Agent 9 (Engineering)

---

## Leading indicators (weekly / monthly)

These measure whether the core mechanic is working. Track weekly during season (April–September), monthly off-season.

| Metric | Definition | Measurement method | Target (v1 benchmark) |
|---|---|---|---|
| **Empty-search rate** | % of Find a game searches that return zero results | Server-side: count zero-result search events / total search events | < 40% within 3 months of launch |
| **Request-to-confirm rate** | % of sent match requests that result in a confirmed fixture | Event: match_request_sent → fixture_confirmed within 30 days | > 50% |
| **Time to confirmed fixture** | Median days from first search to fixture_confirmed | Timestamp delta: first search session → fixture_confirmed event | < 14 days |
| **Trust review completion rate** | % of completed fixtures where at least one party submits a review | Event: fixture_completed → trust_review_submitted within 7 days | > 60% |
| **Fixture Manager return rate** | % of Fixture Managers who return within 30 days of first fixture confirmed | Cohort analysis: users with ≥ 1 confirmed fixture, active again within 30 days | > 70% |
| **Availability utilisation rate** | % of posted availability records that receive ≥ 1 match request | Event: availability_posted → match_request_received within 14 days | > 40% |

---

## Lagging indicators (quarterly)

These measure structural health of the platform. Review at end of each quarter.

| Metric | Definition | Measurement method |
|---|---|---|
| **Duplicate availability reduction** | Clubs posting multiple availability records for same date window | Count: availability_posted events per club per 14-day window; flag > 2 |
| **Faster confirmation (median)** | Median fixture confirmation time improving quarter-on-quarter | Compare quarterly cohorts of time-to-confirmed |
| **Admin burden reduction** | Self-reported (survey): hours per week spent on fixture admin vs. baseline | Quarterly survey to Fixture Managers, n ≥ 30 |
| **Trust signal adoption** | % of clubs with ≥ 3 completed fixtures who have ≥ 1 review submitted | Count: clubs with fixture_count ≥ 3 AND review_count ≥ 1 |
| **New club activation rate** | % of registered clubs that confirm a fixture within 60 days | Cohort: clubs registered → fixture_confirmed within 60 days |
| **New club ranking parity** | New clubs (< N fixtures) appearing in top 50% of search results | Sample search results monthly; measure new-club position distribution |

---

## Anti-metrics

These are things we explicitly do not optimise for. If any of these are improving at the cost of the leading indicators, something is wrong.

| Anti-metric | Why we refuse to optimise it |
|---|---|
| **Total sessions / DAU** | Optimising for return visits creates dark patterns (artificial friction, notification spam). Low frequency is fine if high value. |
| **Notifications sent** | More notifications ≠ more engagement. Notifications should be triggered by real events only. |
| **Profiles created** | Vanity metric. A club that creates a profile and never confirms a fixture is not a success. |
| **Match requests sent** | Volume without conversion means the request flow is broken or the trust layer isn't working. |
| **Trust badge upgrades** | Gaming the badge system is a failure mode, not a success. |
| **Time on site** | This is a task-completion tool. Fast is better. |

---

## Definition of done for MVP

The MVP is done when all of the following are true:

### Functional
- [ ] A Fixture Manager can complete the full flow: search → no results → post availability → receive match request → accept → fixture confirmed
- [ ] A Fixture Manager can complete the full flow: search → find availability → send match request → receive acceptance → fixture confirmed
- [ ] A Fixture Manager can request an umpire from their club's roster
- [ ] A post-match review can be submitted and the trust badge updates accordingly
- [ ] Email and in-app notifications fire for all defined triggers
- [ ] A Club Administrator can create and manage a club profile and team roster

### Quality
- [ ] WCAG 2.2 AA compliance verified (automated + manual spot check)
- [ ] Core flows tested on mobile (iOS Safari, Android Chrome)
- [ ] All instrumentation events firing and validated in Agent 9's event schema

### Data
- [ ] Leading indicators are measurable from day one of launch
- [ ] No personal data stored beyond what's required for fixture coordination

### Trust
- [ ] Trust review questions finalised (see Agent 8)
- [ ] "Needs attention" flag logic reviewed and approved by Agent 1
