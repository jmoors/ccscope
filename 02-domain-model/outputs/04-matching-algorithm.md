# 04 — Matching Algorithm

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 2 (Domain Model & Logic)  
**Status:** Draft — weights provisional; to be validated against Agent 4 research

---

## 1. Algorithm Overview

The matching algorithm ranks available teams in response to a search query. It has two stages:

1. **Hard filter** — eliminates candidates that cannot be matched (binary inclusion/exclusion)
2. **Soft scoring** — ranks surviving candidates by weighted factors

The output is an ordered list of availability records (not clubs; a club may have multiple teams posting availability on the same date).

---

## 2. Hard Filters

All filters must pass for a candidate to appear in results. Any single failure removes the candidate from results entirely.

| Filter | Rule | Source |
|---|---|---|
| **Format compatibility** | Candidate format is hard- or soft-compatible with searcher's format (see `03-format-taxonomy.md`) | Fixture record |
| **Age group compatibility** | Candidate age group is hard- or soft-compatible with searcher's age group | Fixture record |
| **Gender compatibility** | Candidate gender category is hard- or soft-compatible with searcher's gender | Fixture record |
| **Date window overlap** | Candidate's availability date (or window) overlaps with searcher's requested date (or window) | Availability record |
| **Geographic radius** | Distance between candidate's home ground and searcher's home ground ≤ `search.radius_miles` (default 50; user may set 10–100) | Venue lat/lng |
| **Block filter** | Neither club has blocked the other | Block records |
| **Availability lock** | Candidate's availability is not locked by an existing pending match request | Match request record |
| **Not same club** | Candidate is not a team within the searcher's own club | Club ID |

---

## 3. Soft Scoring Factors

Each surviving candidate receives a composite score `S` between 0.0 and 1.0:

```
S = w₁ × distance_score
  + w₂ × tier_score
  + w₃ × trust_score
  + w₄ × response_rate_score
  + w₅ × home_away_score
  + w₆ × activity_score
```

### Factor weights (provisional)

| Factor | Weight (wₙ) | Rationale |
|---|---|---|
| Distance | 0.25 | Proximity is the single most practical constraint for most clubs |
| Tier match | 0.20 | Competitive balance matters for fixture quality |
| Trust | 0.20 | Reliability signal is core to the product's value |
| Response rate | 0.15 | Responsiveness predicts whether the request will be answered promptly |
| Home/away balance | 0.10 | Fairness; prevents a club always being asked to travel |
| Activity recency | 0.10 | Active clubs are more likely to follow through |

Weights sum to 1.00. These are the initial defaults; they should be calibrated against user behaviour data after launch.

---

### 3.1 Distance Score

```
distance_score = max(0, 1 - (distance_miles / radius_miles))
```

- At 0 miles (same ground): score = 1.0
- At the radius edge: score = 0.0
- Linear decay between 0 and radius

**Home/away asymmetry note:** Distance is calculated from the SEARCHER's home ground to the CANDIDATE's home ground. This is a proxy for travel burden. The actual fixture may be at either ground; the algorithm does not penalise a candidate because their ground is far from the searcher's — it simply reflects that both clubs may need to travel.

**If the searcher has no home ground set:** Distance filter is disabled; distance_score defaults to 0.5 for all candidates. A prompt is shown to set a home ground.

---

### 3.2 Tier Score

```
tier_distance = abs(searcher.tier - candidate.tier)

tier_score = {
  0  → 1.00
  1  → 0.70
  2  → 0.30
  ≥3 → 0.05
}
```

If either team has no tier set, `tier_score = 0.50` (neutral).

---

### 3.3 Trust Score

```
trust_score = candidate.bayesian_trust_score
```

Bayesian trust score is in [0, 1] range (see `05-trust-algorithm.md`). New clubs (fewer than 5 reviews) have a trust score equal to the prior: 0.70. This means new clubs rank at trust_score = 0.70, equivalent to a club with a reasonable but not excellent track record.

**Explicit principle:** New clubs are not penalised. Their trust_score of 0.70 is equal to a club with a neutral-to-good history. Only clubs with demonstrated negative signals score below 0.70.

---

### 3.4 Response Rate Score

```
response_rate = (requests_responded_within_48h / total_requests_received)
             where total_requests_received ≥ 1

response_rate_score = response_rate
```

If a team has received zero match requests, `response_rate_score = 0.70` (same neutral prior as trust). Expiries count as non-responses and reduce this score.

Response rate is calculated over the last 24 calendar months (rolling window) to avoid old inactivity penalising currently active clubs.

---

### 3.5 Home/Away Balance Score

This factor rewards candidates who would typically host, if the searcher would typically travel (or vice versa). It reduces the chance of every fixture being at one club's ground.

```
candidate_home_ratio = (candidate_home_fixtures / candidate_total_fixtures)
searcher_home_ratio  = (searcher_home_fixtures / searcher_total_fixtures)
```

If `candidate_home_ratio > 0.70` (this club usually plays at home), and `searcher_home_ratio < 0.50` (this club often travels), the fixture would likely be at the candidate's ground, which aligns with what the candidate prefers and means the searcher travels. Score is lower in this case because the searcher may not want to travel further.

```
home_away_score = 1 - abs(candidate_home_ratio - 0.50)
```

This rewards candidates whose home/away balance is closest to 50:50. Clubs that always host score 0.5; clubs with perfect balance score 1.0.

If insufficient data (< 3 fixtures), `home_away_score = 0.50`.

---

### 3.6 Activity Recency Score

```
days_since_last_fixture = (today - candidate.last_completed_fixture_date)

activity_score = max(0.10, 1 - log10(max(1, days_since_last_fixture)) / log10(365))
```

- Active today: score ≈ 1.0
- Active 30 days ago: score ≈ 0.76
- Active 1 year ago: score = 0.0 (floored at 0.10)
- No completed fixtures: score = 0.70 (same neutral prior; new clubs are not penalised for having no history)

**New club rule:** If `candidate.completed_fixtures = 0`, activity_score = 0.70 (neutral prior), not the time-decay calculation.

---

## 4. Composite Score Calculation

```
S = 0.25 × distance_score
  + 0.20 × tier_score
  + 0.20 × trust_score
  + 0.15 × response_rate_score
  + 0.10 × home_away_score
  + 0.10 × activity_score
```

Results are sorted by S descending.

---

## 5. Tie-Breaker Hierarchy

When two candidates have identical composite scores S (to 4 decimal places), apply these in order:

1. **Trust score** — higher bayesian_trust_score wins
2. **Response rate** — higher response_rate wins
3. **Platform join date** — earlier join date wins (longer-established clubs are marginally preferred)
4. **Availability ID** — lower (earlier-created) ID wins — deterministic, prevents sort instability

---

## 6. Soft Match Compatibility Notice

When a candidate passes only via soft compatibility (see `03-format-taxonomy.md`), a compatibility notice is attached to the result:

```json
{
  "compatibility_notices": [
    "format_agreement_needed",
    "gender_agreement_needed"
  ]
}
```

These notices do not affect ranking but are displayed to the user. The match request flow requires the sending FM to acknowledge them before the request is submitted.

---

## 7. New Clubs: Fair Surfacing

New clubs (fewer than 5 completed fixtures on platform) receive the following neutral priors in place of computed scores:

| Factor | New club default score |
|---|---|
| Trust | 0.70 |
| Response rate | 0.70 |
| Activity recency | 0.70 |

These priors are equal to a club with a moderate but not outstanding track record. A new club with nearby location, matching tier, and compatible format will rank **comparably to an average established club**. It will not rank at the top (reserved for clubs with demonstrated reliability and activity), but it will rank above inactive or poorly-reviewed established clubs.

This directly implements the product principle: "Never punish new entrants."

---

## 8. Algorithm Pseudocode

```
function search(query, searcher_team):
  candidates = []
  
  for each availability record in system:
    if availability.status != 'active': continue
    if fails_any_hard_filter(availability, query, searcher_team): continue
    
    candidate = availability.team
    
    d_score = distance_score(searcher_team.home_ground, candidate.home_ground, query.radius)
    t_score = tier_score(searcher_team.tier, candidate.tier)
    tr_score = trust_score(candidate)
    rr_score = response_rate_score(candidate)
    ha_score = home_away_score(candidate)
    ac_score = activity_score(candidate)
    
    S = 0.25*d_score + 0.20*t_score + 0.20*tr_score
      + 0.15*rr_score + 0.10*ha_score + 0.10*ac_score
    
    candidates.append({
      availability: availability,
      score: S,
      compatibility_notices: get_notices(availability, query, searcher_team)
    })
  
  candidates.sort(by=score desc, then by tie_breakers)
  return candidates
```

---

## 9. Worked Examples

### Example A: Nearby, matching tier and format — top result

**Searcher:** Thornton CC 1st XI (T20, Open, Men's, Tier 3; home ground: Thornton, 0 miles reference)

**Candidate:** Redfield CC 1st XI (T20, Open, Men's, Tier 3; distance: 8 miles; 50 completed fixtures; bayesian trust = 0.88; response rate = 0.90; home_ratio = 0.55; last fixture: 5 days ago)

| Factor | Calculation | Score |
|---|---|---|
| Distance | 1 - (8/50) = 1 - 0.16 | 0.84 |
| Tier | \|3-3\| = 0 | 1.00 |
| Trust | 0.88 | 0.88 |
| Response rate | 0.90 | 0.90 |
| Home/away | 1 - \|0.55 - 0.50\| | 0.95 |
| Activity | 1 - log10(5)/log10(365) | 0.87 |

```
S = 0.25×0.84 + 0.20×1.00 + 0.20×0.88 + 0.15×0.90 + 0.10×0.95 + 0.10×0.87
  = 0.21 + 0.20 + 0.176 + 0.135 + 0.095 + 0.087
  = 0.903
```

**Result:** S = 0.903 — likely top of results. No compatibility notices.

**Why correct:** All hard filters pass; all factors favour this candidate. Strong trust and response rate, nearby, matching tier. This is the ideal match the algorithm should surface first.

---

### Example B: New club — neutral ranking

**Candidate:** Westgate CC (new club, 0 completed fixtures; T20, Open, Men's, Tier 3; distance: 12 miles)

| Factor | Score |
|---|---|
| Distance | 1 - (12/50) = 0.76 |
| Tier | 1.00 (same tier) |
| Trust | 0.70 (prior) |
| Response rate | 0.70 (prior) |
| Home/away | 0.50 (no data) |
| Activity | 0.70 (new club prior) |

```
S = 0.25×0.76 + 0.20×1.00 + 0.20×0.70 + 0.15×0.70 + 0.10×0.50 + 0.10×0.70
  = 0.19 + 0.20 + 0.14 + 0.105 + 0.05 + 0.07
  = 0.755
```

**Result:** S = 0.755 — mid-range ranking. Appears above a poorly-reviewed club, below a well-established nearby club.

**Why correct:** New clubs score at neutral priors, placing them in the middle of the pack — not penalised, not artificially elevated. Fixture Managers can still choose them.

---

### Example C: Distant club, high trust

**Candidate:** Southbury CC 1st XI (T20, Open, Men's, Tier 3; distance: 45 miles; bayesian trust = 0.94; response rate = 0.95; last fixture: 10 days ago; home_ratio = 0.50)

| Factor | Score |
|---|---|
| Distance | 1 - (45/50) = 0.10 |
| Tier | 1.00 |
| Trust | 0.94 |
| Response rate | 0.95 |
| Home/away | 1.00 |
| Activity | 1 - log10(10)/log10(365) | ≈ 0.61 |

```
S = 0.25×0.10 + 0.20×1.00 + 0.20×0.94 + 0.15×0.95 + 0.10×1.00 + 0.10×0.61
  = 0.025 + 0.20 + 0.188 + 0.1425 + 0.10 + 0.061
  = 0.716
```

**Result:** S = 0.716 — appears in results, but distance heavily penalises. A Fixture Manager actively looking for a challenge match with a highly reliable team might select them regardless of rank.

**Why correct:** Extreme distance suppresses the score even for an excellent team. The platform shows them; the Fixture Manager decides. The algorithm does not hide good options, just ranks them appropriately.

---

### Example D: Tier mismatch, poor trust — ranked low

**Candidate:** Old Trafford Wanderers (T20, Open, Men's, Tier 1; distance: 5 miles; bayesian trust = 0.40; response rate = 0.45; last fixture: 200 days ago)

| Factor | Score |
|---|---|
| Distance | 1 - (5/50) = 0.90 |
| Tier | \|3-1\| = 2 → 0.30 |
| Trust | 0.40 |
| Response rate | 0.45 |
| Home/away | 0.50 (insufficient data) |
| Activity | 1 - log10(200)/log10(365) ≈ 0.13 |

```
S = 0.25×0.90 + 0.20×0.30 + 0.20×0.40 + 0.15×0.45 + 0.10×0.50 + 0.10×0.13
  = 0.225 + 0.06 + 0.08 + 0.0675 + 0.05 + 0.013
  = 0.496
```

**Result:** S = 0.496 — near the bottom of results despite proximity. Poor trust, poor responsiveness, inactive, large tier gap.

**Why correct:** The algorithm correctly down-ranks a nearby but unreliable team. The searcher still sees them if they scroll far enough — the platform does not hide options — but the ranking protects most users from picking them first.

---

### Example E: Soft format match — compatibility notice

**Searcher:** Merton Sunday XI (Sunday, Open, Mixed, Tier 2)

**Candidate:** Oldwick 2nd XI (40over, Open, Men's, Tier 2; distance: 7 miles; bayesian trust = 0.80; response rate = 0.80; last fixture: 14 days ago; home_ratio = 0.48)

Format: Sunday vs 40over → soft match. Gender: Mixed vs Men's → soft match.

| Factor | Score |
|---|---|
| Distance | 1 - (7/50) = 0.86 |
| Tier | 1.00 |
| Trust | 0.80 |
| Response rate | 0.80 |
| Home/away | 1 - \|0.48-0.50\| = 0.98 |
| Activity | 1 - log10(14)/log10(365) ≈ 0.54 |

```
S = 0.25×0.86 + 0.20×1.00 + 0.20×0.80 + 0.15×0.80 + 0.10×0.98 + 0.10×0.54
  = 0.215 + 0.20 + 0.16 + 0.12 + 0.098 + 0.054
  = 0.847
```

**Result:** S = 0.847 — near the top of results. Two compatibility notices attached: "Format to be agreed" and "Gender category differs — mutual agreement needed."

**Why correct:** A good nearby match with matching tier and solid trust. The soft compatibility flags mean the Fixture Managers must discuss and agree format and gender before the request is sent. The algorithm ranks based on the match quality; the compatibility notice handles the outstanding agreements.
