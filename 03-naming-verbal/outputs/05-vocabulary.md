# 05 — Product Vocabulary

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 3 (Naming & Verbal Identity)
**Feeds:** `shared/GLOSSARY.md` (merged below; GLOSSARY.md version-bumped to 1.1)

---

## Purpose

This is the single source of truth for every user-facing word in the product. All agents defer to this document for terminology. Changes are proposed by posting to `03-naming-verbal/inbox/`; Agent 3 approves, revises, or rejects with rationale and version-bumps GLOSSARY.md on merge.

---

## Section 1: Product entities

### Canonical terms

| Term | Definition | Never say |
|------|-----------|-----------|
| **Fixture** | A game record, partial or complete. The core domain object. | "match object", "event", "game" (in system text) |
| **Availability** | A published intent to play on a given date or window. | "listing", "post", "ad", "opening" |
| **Match request** | A team-to-team request to play a specific fixture. | "invite", "invitation", "proposal", "challenge", "connection request" |
| **Support request** | A request for pitch / umpire / scorer. | "booking", "hire request", "service booking" |
| **Club** | An organisation with one or more teams. | "organisation" (in product UI), "group", "society" |
| **Team** | A specific playing group within a club (1st XI, 2nd XI, Sunday XI, Colts). | "side" (in UI — fine in copy), "squad", "group" |
| **Service provider** | Umpire, scorer, coach, or venue. V1: umpires via club roster only. | "vendor", "contractor", "professional", "official" (too narrow) |
| **Trust badge** | The public visual indicator of a club's reliability tier. | "rating", "score", "stars", "badge level", "reputation score" |
| **Review** | The post-match 3-question private feedback. | "rating", "testimonial", "feedback" (acceptable in onboarding), "comment" |
| **Season** | The annual playing period. | "year", "campaign", "period" |

### Tricky distinctions

**Fixture vs. game vs. match**
- "Fixture" is the product term and the correct cricket administration term. Use it everywhere in system text and labels.
- "Game" and "match" are natural language that users will use; do not correct users, but do not use either in product UI, button labels, or system messages.
- Exception: "Find a game" is the canonical phrase for the search action. Here "game" is used because that is how fixture managers speak: "I need to find a game." This is the one exception to the fixture-only rule.

**Club vs. Team**
- A club has multiple teams. A match request is between teams, not clubs — but teams are associated with clubs.
- "Blanktown CC" is the club. "Blanktown CC 1st XI" is the team. Both will appear in the UI; the distinction matters.

---

## Section 2: User-facing verbs

These are the canonical action phrases. Use them exactly in button labels, empty states, notifications, and instructions.

| Action | Canonical phrase | Never say |
|--------|-----------------|-----------|
| Search for an opponent | **Find a game** | "search matches", "discover opponents", "find opponents", "browse fixtures" |
| Publish intent to play | **Post availability** | "publish fixture", "list game", "advertise your availability", "go live", "create post" |
| Send a game request | **Send match request** | "invite", "send invite", "propose", "challenge", "connect" |
| Request pitch / official | **Find support** | "book umpire", "hire scorer", "request official" |
| Agree to a match request | **Accept** | "approve", "confirm" (in the context of responding to a request), "agree" |
| Refuse a match request | **Decline** | "reject", "deny", "refuse", "turn down" |
| Submit post-match review | **Leave a review** | "rate", "give stars", "submit feedback", "review this club" |
| Mark fixture as played | **Complete** | "close", "finalise", "archive", "mark done" |
| Withdraw availability | **Remove availability** | "delete post", "take down", "un-post" |
| Cancel a confirmed fixture | **Cancel fixture** | "call off", "abandon", "delete fixture" |

### Notes on verb choices

**"Find a game" not "find a fixture"**
The phrase "find a fixture" sounds like administration; "find a game" is how fixture managers speak. The deliberate inconsistency — "fixture" as noun, "game" in this one phrase — is intentional and cricket-idiomatic. Do not "correct" it to "find a fixture."

**"Accept / Decline" not "Confirm / Reject"**
"Confirm" is reserved for fixture status (see Section 3). Using "confirm" in the response-to-request context creates a false equivalence. "Accept" is the right register — it implies agency, not just rubber-stamping.

---

## Section 3: Status language (user-facing)

All statuses are written as full phrases, not single words. Never abbreviate in UI labels.

| Status | When it applies | Notes |
|--------|----------------|-------|
| **Awaiting opponent** | Fixture has a date but no confirmed opposition | First missing element for most fixtures |
| **Awaiting venue** | Fixture has an opponent but no confirmed ground | May also apply when home/away is unresolved |
| **Awaiting officials** | Fixture needs umpire and/or scorer | V1: umpires only |
| **Awaiting response** | Match request sent; not yet answered | Applied to the requesting team's view |
| **Confirmed** | All required parties confirmed | Do not say "ready to go", "set", "locked in" |
| **Completed** | Fixture date has passed | Applied automatically after date; not user-triggered |
| **Cancelled** | Fixture called off before being played | User-triggered; triggers notification to all parties |

### Notes on status language

**"Awaiting" not "pending"**
"Pending" is system language. "Awaiting" is the language of a patient person who has done their part and is waiting on others. It is more accurate and more respectful of the user's time.

**"Confirmed" is terminal for the coordination flow**
Once a fixture is Confirmed, the UI should not suggest further action beyond noting what else (officials, tea) might still be outstanding as informational items, not blocking statuses.

---

## Section 4: Trust language

### User-facing trust vocabulary

| Term | Definition | Notes |
|------|-----------|-------|
| **Trust badge** | The visual indicator shown publicly on a club's profile | Never say "rating", "score", "stars", "percentage" |
| **New** | Fewer than N completed fixtures on platform | Neutral, not negative. Never "Unverified", "Unknown", "Unrated" |
| **Reliable** | Established positive track record | The first earned tier |
| **Established** | Long-standing positive track record | The senior tier |

### Internal-only trust vocabulary (never surface to users)

| Term | Definition |
|------|-----------|
| Trust score | The numeric aggregate underlying badge assignment |
| Confidence weighting | Bayesian smoothing factor that prevents gaming by volume |
| Ranking contribution | Trust's contribution to search sort order |
| Needs attention | Internal flag for clubs with negative signals — never shown as a public badge |

### Trust communication principles

- Never display a number (score, percentage, count) in the trust context
- Never compare clubs to each other explicitly in the UI ("higher rated than 87% of clubs")
- The review is always described as private: "Your review is private."
- The badge is always described as based on track record, never on individual reviews

---

## Section 5: Cricket domain terms (use accurately)

These terms have specific meaning in cricket. Use them correctly; do not substitute general sports language.

| Term | Correct usage | Notes |
|------|--------------|-------|
| **Format** | T20, 40-over, 50-over, timed declaration, limited-overs | Never "game type", "match type" |
| **Timed declaration** | A format where the result depends on declared innings and time | Not "declaration match" |
| **Tier / ability** | The playing standard of a team | Never "skill level", "division" (unless league-specific), "ranking" |
| **1st XI / 2nd XI / Sunday XI** | Standard team naming | Always caps; the slash is part of the name |
| **Friendly** | A non-league game; the platform's primary use case | "Friendly fixture" is acceptable in context |
| **League fixture** | A fixture fixed by a league; usually not arranged via the platform | Distinguish clearly from friendlies |
| **Rearranged fixture** | A fixture rescheduled after weather or cancellation | Never "postponed match" in user-facing copy |
| **Tea** (or **teas**) | The food break between innings | Plural ("teas" = the meal) acceptable in informal contexts; "tea interval" in formal contexts |
| **Match fees** | Player financial contributions to playing costs | Not "game fees", "player payments" |
| **Home / away** | Which club is hosting | Not "host / visitor" in cricket contexts |

---

## Section 6: Forbidden language

These words and phrases must not appear in any product UI, notification, or system message.

### Forbidden words / phrases (product-wide)

| Forbidden | Reason |
|-----------|--------|
| Marketplace | Implies commercial transaction; this is a coordination tool |
| Algorithm | Never explain the ranking mechanism with this word |
| Rating (as noun) | Use "review" or "trust badge" |
| Stars | Trust is not star-rated |
| Percentage | Trust is not expressed as a percentage |
| Create a fixture | Except in deep admin flows (league import, admin backdating) — never in the primary user journey |
| Oops / Uh-oh | Error states must be direct; not apologetic theatre |
| Emoji in error states | Never. Not even a warning triangle emoji in running product copy |
| Awesome / Amazing / Great / Fantastic | Affirmations; do not appear in system messages |
| Seamless / Effortless | Marketing language that telegraphs sycophancy |
| Powered by | Implied endorsement language |
| Hey [name] / Hi there / Welcome back, friend | Greeting patterns |
| Community | We are a coordination tool, not building a community (that framing creates false expectations) |

### Cricket terms forbidden in branding and naming (not product copy)

| Forbidden | Reason |
|-----------|--------|
| Wicket | Overused in cricket tech naming |
| Stumps | Overused / cliché |
| Googly | Cliché / cute |
| Howzat | Cliché / dated |
| Maiden | Overused |
| Crease | Overused |
| Yorker | Cliché / tactical |
| Silly | Odd / misjudged outside cricket context |
| Slip | Ambiguous; also a catching position that telegraphs the wrong register |

These are prohibited in product naming and brand identity (flagging for Agent 5), not in cricket domain explanations or contextual help content.

---

## Section 7: Notifications vocabulary

Notifications follow the direct/specific voice principle: subject line = the fact; body = what's needed.

### Subject line patterns

| Context | Pattern | Example |
|---------|---------|---------|
| Incoming match request | [Team Name] has sent you a match request for [Date] | "Blanktown CC 1st XI has sent you a match request for 14 June" |
| Request accepted | Match request accepted — fixture on [Date] is confirmed | "Match request accepted — fixture on 14 June is confirmed" |
| Request declined | [Team Name] has declined your match request for [Date] | "Blanktown CC 1st XI has declined your match request for 14 June" |
| Availability posted | Availability posted for [Date] | "Availability posted for 14 June" |
| Fixture reminder | Fixture on [Date] — [what's outstanding] | "Fixture on 14 June — umpire not yet confirmed" |
| Trust review | Post-match review for [Date] fixture | "Post-match review for 14 June fixture" |

**Never use:** "You have a new message on [Product]", "Great news from [Product]", "Don't miss out"

---

## Section 8: Empty state vocabulary

Empty states must state the fact and the action. No metaphor, no encouragement theatre.

| Context | Correct | Never |
|---------|---------|-------|
| No search results | "No availability found for those dates. Post your own availability to be found by other teams." | "Looks like it's quiet around here. Be the first to post!" |
| No fixtures | "No fixtures yet. Start by posting your availability or searching for a game." | "Your fixture list is empty — let's change that!" |
| No umpires on roster | "No umpires in your club's roster yet. Ask your Club Administrator to add them." | "Oops! No umpires found. Try widening your search!" |
| No trust reviews yet | "No reviews yet. Reviews are collected after completed fixtures." | "Be the first to receive a review!" |

---

## Version history

| Version | Date | Change |
|---------|------|--------|
| 1.1 | 2026-04-19 | Vocabulary document produced; GLOSSARY.md expanded from v1.0. Sections added: verbs, status language, notifications, empty states, notification patterns, forbidden language (extended). |
| 1.0 | 2026-04-19 | GLOSSARY.md initial version (product entities, verbs, status, trust, cricket terms baseline) |
