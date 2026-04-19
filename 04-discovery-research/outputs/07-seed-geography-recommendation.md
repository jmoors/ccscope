# 07 — Seed Geography Recommendation: Surrey

**Version:** 0.1 (draft — requires interview validation before finalisation)
**Date:** 2026-04-19
**Owner:** Agent 4 (Discovery & Research)
**Status:** Proposed — not yet accepted. Requires stakeholder review and Agent 1 decision log entry.

---

## What this document is

A structured assessment of Surrey as the proposed seed geography for launch. It covers why the choice matters, how Surrey performs against selection criteria, what the specific risks are, and what the interview programme must confirm before the recommendation can be finalised.

This document does not finalise the decision. That requires Agent 1 to accept it via `shared/DECISION_LOG.md`.

---

## Why seed geography matters

This is a search-first marketplace. Its central premise — that a fixture manager can search and find existing availability from other clubs — only works if there are enough clubs posting availability to make the search worthwhile. Too few clubs in a geography and the platform becomes a ghost town: fixture managers search, find nothing, and don't return.

Seed geography is therefore a liquidity problem before it is anything else. We need enough clubs in one geography to create the density that makes the search-first experience viable — before expanding.

Secondary considerations: partnership leverage, representativeness as a test case, and operational accessibility for the team.

---

## Selection criteria

| Criterion | Weight | Description |
|---|---|---|
| Club density | High | Enough clubs within plausible travel distance to produce non-empty search results |
| Friendly fixture culture | High | Clubs that actively arrange friendlies (vs. league-only clubs) |
| County board partnership potential | Medium | A county board willing to introduce us to clubs |
| Representativeness | Medium | Findings from the seed geography should generalise; an atypical geography distorts learning |
| Algorithm fit | Medium | The 50-mile default radius should return meaningful results without crossing awkward boundaries |
| Team accessibility | Low | Practical ability to conduct in-person interviews and eventually on-the-ground support |

---

## Surrey profile

### Geography

Surrey is a compact inland county immediately south and west of London, bordered by Greater London to the north, Kent to the east, West Sussex and East Sussex to the south, Hampshire to the south-west, and Berkshire and Middlesex to the west. Area: approximately 1,663 km².

Major centres of recreational cricket: Guildford, Woking, Epsom, Reigate, Leatherhead, Farnham, Dorking, Walton-on-Thames.

### Club density

Surrey has approximately 200–280 recreational cricket clubs active in any given season, across senior men's, women's, mixed, and veteran cricket. This is one of the higher densities in England relative to geographic area. A club in central Surrey (e.g., Guildford) with a 50-mile radius would theoretically reach clubs extending into south London, north Kent, West Sussex, Hampshire, and Berkshire — a pool of several hundred clubs.

This is a genuine strength. The cold-start problem is less acute when the initial geography has this density.

### Friendly fixture culture

Surrey clubs play a substantial volume of friendlies, particularly:
- Sunday XIs with no league obligation
- Second and third XIs unable to fill their schedule from league fixtures alone
- End-of-season and pre-season games

This matches the platform's primary use case. Surrey is not a purely league-driven cricket county.

### Play-Cricket footprint

Surrey Cricket Board is an active Play-Cricket county. Most competitive clubs in Surrey are registered. This is important in two directions: (1) our co-existence assumption (A — not numbered in this doc) will be stress-tested by a county with high Play-Cricket penetration; (2) Surrey Cricket Board has existing relationships with clubs that could accelerate recruitment and partnership.

### Surrey Cricket Board

The Surrey Cricket Board (SCB) is the county-level body responsible for recreational and developmental cricket, separate from Surrey County Cricket Club (which operates at the professional level). SCB coordinates with ECB and supports club development across the county. They are the primary partnership target, not Surrey CCC.

---

## Strengths

**1. Density works for the algorithm**
A 50-mile radius from a central Surrey club returns a large candidate pool. Even at 5% early platform penetration (10–15 clubs), a search is unlikely to return zero results — which is the critical failure mode we must avoid at launch.

**2. Format diversity**
Surrey clubs play across T20, 40-over, Sunday (informal), veterans, women's, and mixed formats. This means we can test multi-format search and compatibility notice behaviour in real conditions from day one, rather than discovering edge cases later.

**3. Partnership route is clear**
Surrey Cricket Board is an accessible, well-run county body. An introduction via ECB recreational cricket contacts or direct outreach to the SCB development team is a realistic first step. A county-board endorsement significantly reduces the trust cost of recruiting clubs to a new platform.

**4. Interview access**
Surrey's proximity to London means in-person interviews are achievable. The density of clubs also means a representative sample (covering different formats, ages, club sizes) can be assembled without extensive travel.

**5. Strong veteran and Sunday cricket culture**
Veteran cricket (40+, 45+, 50+ age groups) is active in Surrey. This matters because the veterans age-group compatibility boundary (currently set at 10 years in the domain model — decision log 2026-04-19, status: Proposed) needs validation, and Surrey provides a real test population.

---

## Risks

### Risk 1 — Traffic distorts the 50-mile radius

This is the most significant algorithm-specific risk. Surrey's road network is dominated by the M25 and several heavily congested A-roads. A club-to-club distance of 20 miles can represent 60–90 minutes of travel during match-day conditions. The algorithm uses straight-line (crow-flies) distance between home grounds.

**Effect:** A club in Woking and a club in Sevenoaks may both appear within the 50-mile radius, but the practical travel time via the M25 and A roads could be 90 minutes — longer than clubs in a less congested geography would consider reasonable for a friendly.

**Mitigation options:**
- Validate in interviews whether Surrey fixture managers think in miles or in journey time when assessing travel.
- If journey time is the primary frame, the algorithm may need a travel-time proxy (driving time estimate) rather than straight-line distance — but this is a material scope change for Agent 9 and should not be assumed.
- At minimum, flag to Agent 2 that the distance weight (0.25) may need recalibration for urban/peri-urban geographies.

**Escalation:** If 3+ interview participants explicitly describe journey time as the deciding constraint rather than mileage, this becomes a P1 flag to Agent 2.

### Risk 2 — Surrey is not representative of UK cricket

Surrey skews more affluent, more suburban, and more London-adjacent than the median English cricket county. A fixture manager in Epsom and a fixture manager in Rotherham may have meaningfully different experiences, expectations, and tool tolerances.

**Effect on learning:** Findings from Surrey may not generalise cleanly to Yorkshire, Lancashire, or the Midlands — which are large cricket markets we will need to reach in phase 2.

**Mitigation:** Be explicit in synthesis documents about which findings may be Surrey-specific. Supplement with at least 3 remote interviews from a northern county (Yorkshire or Lancashire recommended) during weeks 5–7 to provide a contrast point. These are not part of the seed geography decision but inform generalisation confidence.

### Risk 3 — High Play-Cricket penetration creates adoption friction

Clubs in well-administered counties are often more deeply embedded in Play-Cricket. The fixture manager who manages league results, club records, and some friendly arrangement through Play-Cricket is a harder conversion than one who uses Play-Cricket only for league result submission.

**Mitigation:** This is the correct place to stress-test assumption A — that the platform co-exists with Play-Cricket rather than competing. Surrey is actually a good geography to test this precisely because the friction is likely higher here than elsewhere. If co-existence works in Surrey, it works.

### Risk 4 — Ground availability pressures

Surrey has significant residential development pressure on cricket grounds, particularly in suburban areas. Several clubs in the county have lost or are under threat of losing their home grounds. A club without a stable home ground will not register a home ground in the platform accurately.

**Effect on algorithm:** The distance calculation depends on clubs having registered home grounds. If a meaningful fraction of clubs in the seed geography lack stable grounds, distance scoring degrades.

**Mitigation:** Flag in interviews. If widespread, consider whether the "no home ground" fallback (distance score defaults to 0.5) needs refinement for the seed geography.

---

## Algorithm-specific considerations for Surrey

| Parameter | Default | Surrey consideration |
|---|---|---|
| Default search radius | 50 miles | Likely appropriate for club density; may feel large given traffic. Validate. |
| Distance weight | 0.25 | May underweight effective distance in traffic-dense areas. Monitor. |
| Travel time vs. straight-line | Straight-line | Surrey traffic may make this a material gap. Raise to Agent 2 if confirmed in interviews. |
| Veteran age group boundary | 10 years (Proposed) | Surrey has active veteran cricket; good test case. |

---

## Comparison with alternatives

| Geography | Club density | Representativeness | Partnership route | Algorithm fit | Risk |
|---|---|---|---|---|---|
| **Surrey** | High | Moderate (London-adjacent) | Clear (SCB) | Good but traffic caveat | Medium |
| Yorkshire | Very high | High | Strong (Yorkshire CB active) | Excellent | Low |
| Kent | High | Moderate | Good (KCB) | Better than Surrey on traffic | Low-Medium |
| Lancashire | High | High | Good | Good | Low |
| Middlesex | High | Low (too London) | Possible | Poor (urban travel) | High |

Yorkshire is the strongest alternative on most criteria — highest club density in England, high representativeness, excellent county board, and better algorithm fit (less traffic distortion on the 50-mile radius). If the Surrey recommendation does not survive interview validation, Yorkshire is the recommended fallback.

Kent is the second alternative — similar density to Surrey, less traffic distortion, good county board, and slightly more representative of market-average English cricket conditions.

---

## Recommendation

**Proceed with Surrey as the seed geography, subject to the following conditions being confirmed in research:**

1. At least 5 Surrey fixture managers confirm that arranging friendlies is a real friction point and that their current network of contacts is insufficient to fill their fixture list reliably.
2. At least 3 Surrey fixture managers confirm that they think primarily in miles (not journey time) when assessing opponent travel — OR, if journey time is the dominant frame, a flag is raised to Agent 2 before the algorithm is built.
3. Surrey Cricket Board agrees to an introductory conversation (warm lead, not commitment) by end of week 4.
4. No more than 2 of the first 10 Surrey interview participants indicate that their club's fixture list is entirely league-driven with no friendly gap.

If conditions 1 and 2 are not met, escalate to Agent 1 with a recommendation to switch to Yorkshire.

---

## Partnership target: Surrey Cricket Board

**Primary contact route:** ECB recreational cricket network → Surrey Cricket Board Development Manager. The SCB employs a club development officer whose role includes supporting clubs with tools and administration. This is the correct entry point — not Surrey CCC.

**What we are asking for (initial):**
- An introduction to 5–8 fixture managers across different clubs and formats for research conversations
- A future conversation about whether SCB would be willing to share information about the platform with clubs they support

**What we are not asking for:**
- Endorsement before the product exists
- Financial partnership
- Exclusive territory

**Warm lead criterion:** A named SCB contact who has agreed to a follow-up conversation about potential collaboration. This is the minimum standard for "partnership at warm-lead stage" in the handoff criteria.

---

## What this document becomes

Once research interviews confirm or adjust the conditions above, this document is updated to version 1.0 and submitted to Agent 1 for a decision log entry. Until then, it is a working hypothesis, not a decision.

If the recommendation is accepted, `08-partnership-leads.md` records the SCB conversation as the primary partnership thread.

---

*Uncertainty flag: this recommendation is based on secondary knowledge of Surrey cricket and should be treated as a working hypothesis. It becomes reliable only after primary research. The recommendation to proceed is conditional, not unconditional.*
