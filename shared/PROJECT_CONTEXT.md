# Cricket Match Coordination Platform — Shared Project Context

**This document is shared by all 10 agents. Read it first. Do not duplicate its contents in your own outputs.**

---

## One-sentence product definition

A calm, reliable system that helps cricket clubs find games and fill gaps — while quietly rewarding good behaviour over time.

## Core product principles

1. **Search before posting.** Users look for existing availability before publishing their own.
2. **Match before creating.** Fixtures are created only when they're needed, not up front.
3. **Reward reliability quietly.** Trust influences ranking but never dominates it.
4. **Never punish new entrants.** New clubs are neutral, not penalised.
5. **Simplicity over cleverness.** Boring, reliable UX beats novel UX.

## Primary users

- **Team / Fixture Manager (primary):** finds games, posts availability, fills gaps
- **Club Administrator:** manages club profile, teams, venues
- **Service Provider:** umpires, scorers, coaches, venues

## Core domain object

A **Fixture** is a partial-or-complete game record that accretes state:
- Draft → Awaiting opponent → Awaiting venue → Awaiting officials → Confirmed → Completed

## MVP scope — in

- Find a game (search availability)
- Post availability (only when search fails)
- Send / receive / accept / decline match requests
- Fixture detail with "what's missing" panel
- Find support (pitch / umpire / scorer) scoped down
- Post-match trust review (3 questions, private)
- Trust badges: New, Reliable, Established (and internally "Needs attention")
- Notifications (email + in-app)

## MVP scope — out (explicitly)

- Payments
- Tours & multi-fixture planning
- Advertising marketplace
- Open chat / messaging
- Rating comments
- Sponsorship tools
- League fixture integration (beyond import)
- Full open umpire marketplace (v1 = club roster only)

## Tone

- Calm, institutional-in-a-good-way, cricket-literate without being nostalgic
- Not: Silicon Valley startup, sports-media loud, betting-adjacent, Strava-for-cricket
- Comparison points: National Trust, Ordnance Survey, a well-run county club's modern website

## Audience realities

- Age range: fixture secretaries often 50–70s, captains often 20s–30s
- Usage split: admin on desktop evenings, match-day actions on phones in car parks
- Low frequency: once or twice a week in season
- Accessibility matters more than average

## Success metrics (leading)

- Empty-search rate (proxy for marketplace density)
- Request-to-confirm conversion rate
- Time from first search to confirmed fixture
- Trust review completion rate
- Fixture-manager return rate within 30 days

## Success metrics (lagging — from original scope)

- Fewer duplicate availability posts
- Faster match confirmations
- Reduced admin effort
- Positive trust signal adoption
- New clubs not buried in rankings

## Non-negotiable constraints

- WCAG 2.2 AA minimum
- Mobile-first design
- UK cricket domain (T20, 40-over, 50-over, timed declarations, Sunday friendlies)
- Works alongside, not against, Play-Cricket (the ECB platform)
- Privacy-respectful review system (no public comments, one-way aggregate visibility)

## Agent roster (for cross-reference)

1. Product Foundations
2. Domain Model & Logic
3. Naming & Verbal Identity
4. Discovery & Research
5. Brand Identity
6. Information Architecture & Flows
7. Design System & Screen Design
8. Content & Microcopy
9. Engineering
10. Launch & Partnerships

---

## How to use this document

- Reference it; don't rewrite it
- If your work contradicts anything here, flag it rather than silently diverging
- Version-control this document; changes propagate to all agents
