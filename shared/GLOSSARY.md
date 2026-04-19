# Shared Glossary

**Canonical terms. Use these exact words across all artefacts. If you need a new term, add it here first.**

**Full vocabulary reference:** `03-naming-verbal/outputs/05-vocabulary.md`

---

## Product entities

- **Fixture** — a game record, partial or complete. Never "match object" or "event".
- **Availability** — a published intent to play on a given date/window. Never "listing", "post", or "opening".
- **Match request** — a team-to-team request to play a specific fixture. Never "invite", "proposal", "challenge", or "connection request".
- **Support request** — a request for pitch / umpire / scorer.
- **Club** — an organisation with one or more teams.
- **Team** — a specific playing group within a club (1st XI, 2nd XI, Sunday XI, Colts).
- **Service provider** — umpire, scorer, coach, or venue (v1 scoped to umpires via club roster only). Never "vendor", "contractor".
- **Review** — the post-match 3-question private feedback. Never "rating", "testimonial", "stars".
- **Season** — the annual playing period. Never "year", "campaign".

## User-facing verbs (use these exactly)

- **Find a game** — not "search matches", "discover opponents", "find opponents", "browse fixtures"
- **Post availability** — not "publish fixture", "list game", "advertise", "go live"
- **Send match request** — not "invite", "propose", "challenge"
- **Find support** — not "book umpire", "hire scorer"
- **Accept / Decline** — not "approve / reject", "confirm / deny" (in the context of responding to a request)
- **Leave a review** — not "rate", "give stars", "submit feedback"
- **Complete** — not "close", "finalise", "archive" (for marking a fixture as played)
- **Cancel fixture** — not "call off", "abandon", "delete fixture"

**Note on "Find a game" vs "find a fixture":** "Find a game" is the canonical phrase for the search action. The word "game" is used here because that is how fixture managers speak. This is the one deliberate exception to using "fixture" as the primary noun. Do not "correct" it.

## Status language (user-facing)

- **Awaiting opponent** — fixture has date but no confirmed opposition
- **Awaiting venue** — fixture has opponent but no confirmed venue
- **Awaiting officials** — fixture needs umpire/scorer
- **Awaiting response** — match request sent, not yet answered (not "pending")
- **Confirmed** — all required parties confirmed
- **Completed** — fixture date has passed
- **Cancelled** — fixture called off before being played

## Trust language (user-facing)

- **Trust badge** — the public visual indicator. Never "rating", "score", "stars", "percentage".
- **New** — fewer than N completed fixtures on platform. Neutral, not negative. Never "Unverified".
- **Reliable** — established positive track record
- **Established** — long-standing positive track record
- Internal only: **Needs attention** — never shown as a public badge

## Trust language (internal only — never surface)

- **Trust score** — the numeric aggregate
- **Confidence weighting** — Bayesian smoothing factor
- **Ranking contribution** — trust's effect on sort order

## Never use in product

- "Marketplace"
- "Algorithm"
- "Rating" (as a noun — use "review" or "trust badge")
- "Stars" / "percentage" (in any trust context)
- "Community" (we are a coordination tool, not a community platform)
- "Create a fixture" (except in deep admin flows)
- "Oops", "Uh-oh", emoji in error states
- "Awesome", "Amazing", "Great", "Fantastic" as affirmations
- "Seamless", "effortless", "powered by"
- "Hey there", "Welcome back, friend", "Hi there"
- "Pending" (use "Awaiting" in status labels)

## Cricket domain terms (use accurately)

- **Format** — T20, 40-over, 50-over, timed declaration, limited-overs. Never "game type".
- **Tier / ability** — not "skill level", "ranking"
- **1st XI / 2nd XI / Sunday XI** — standard team naming (always caps, slash included)
- **Friendly** — non-league game (our primary use case)
- **League fixture** — fixed by league, usually not arranged via the platform
- **Rearranged fixture** — rescheduled after weather/cancellation. Never "postponed match".
- **Tea, teas** — the food break between innings
- **Match fees** — player contributions
- **Home / away** — not "host / visitor" in cricket contexts

## Cricket terms to avoid in branding/naming

- Wicket, stumps, googly, howzat, maiden, crease, yorker, silly, slip (all overused/dated)
- Crossed-bat iconography
- Red + cream colour scheme (MCC-coded unless deliberate)

---

**Maintained by:** Agent 3 (Naming & Verbal Identity)
**Full vocabulary document:** `03-naming-verbal/outputs/05-vocabulary.md`
**Version:** 1.1
**Changed:** 2026-04-19 — Expanded with verbs, status rationale, trust rules, notification patterns, empty state rules, forbidden language. Full vocabulary in `05-vocabulary.md`.
