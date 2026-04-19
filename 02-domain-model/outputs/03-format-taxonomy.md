# 03 — Format, Age Group, Gender, and Tier Taxonomy

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 2 (Domain Model & Logic)  
**Status:** Draft — awaiting Agent 4 research feedback on tier definitions

---

## 1. Playing Format

### Format Definitions

| Format ID | Label | Description |
|---|---|---|
| `t20` | T20 | 20 overs per innings; no timed element |
| `40over` | 40-over | 40 overs per innings |
| `50over` | 50-over | 50 overs per innings |
| `timed` | Timed declaration | Time-limited game; captain declares; typical of traditional club cricket |
| `sunday` | Sunday friendly | Flexible overs/format agreed on the day; often mixed-ability and shortened; treated as its own category |

**Note on "limited-overs" as a category:** "Limited-overs" is a grouping concept (T20, 40-over, 50-over), not a format a team can select. The glossary uses it as a category label only.

---

### Format Compatibility Rules

Two teams match on format if both are willing to play the requested format. The requesting team's format is the offer; the receiving team must agree.

**Hard compatibility** (will never appear in search results as a match for each other):

| Team A posts | Can match with |
|---|---|
| `t20` | `t20` |
| `40over` | `40over`, `50over`* |
| `50over` | `50over`, `40over`* |
| `timed` | `timed` |
| `sunday` | `sunday`, `t20`, `40over`* |

*\* Soft cross-format match: appears in search results but flagged as "format to be agreed". The match request must include the agreed format before proceeding. If the receiving team's preferred format differs, the request notes this; Fixture Managers agree via the structured request fields.*

**Hard incompatibility** (never shown as a match):
- `timed` with any limited-overs format
- `t20` with `timed`
- `sunday` with `timed` or `50over`

**Rationale for Sunday/T20 soft compatibility:** Sunday XI teams often play T20 or shortened 40-over games; it would be too restrictive to prevent them matching.

---

### Format Compatibility Matrix

| | t20 | 40over | 50over | timed | sunday |
|---|:---:|:---:|:---:|:---:|:---:|
| **t20** | ✓ Hard | ✗ | ✗ | ✗ | ✓ Soft |
| **40over** | ✗ | ✓ Hard | ✓ Soft | ✗ | ✓ Soft |
| **50over** | ✗ | ✓ Soft | ✓ Hard | ✗ | ✗ |
| **timed** | ✗ | ✗ | ✗ | ✓ Hard | ✗ |
| **sunday** | ✓ Soft | ✓ Soft | ✗ | ✗ | ✓ Hard |

Hard = exact match, no negotiation needed. Soft = match, but format must be agreed in the request.

---

## 2. Age Group

### Age Group Definitions

| Age Group ID | Label | Eligibility |
|---|---|---|
| `open` | Open (Senior) | Players aged 18 and over; default for most adult club cricket |
| `vets40` | Veterans 40+ | Majority (minimum 7 of 11) players aged 40+; up to 4 "guests" under 40 permitted |
| `vets45` | Veterans 45+ | Majority aged 45+; same guest rule |
| `vets50` | Veterans 50+ | Majority aged 50+ |
| `vets55` | Veterans 55+ | Majority aged 55+ |

**Junior age groups (U19, U17, U15, U13, etc.) are deferred from MVP** per `shared/DECISION_LOG.md` (safeguarding requirements). These IDs are reserved but not implemented.

**Guest rule:** The platform does not enforce player-level eligibility (no player-level profiles in MVP). The guest allowance is a convention known to cricket administrators; the platform records the age group as a team attribute and trusts clubs to self-declare accurately. Disputes are out of scope.

---

### Age Group Compatibility Rules

| Team A | Can match with |
|---|---|
| `open` | `open` only |
| `vets40` | `vets40`, `vets45` (soft), `vets50` (hard incompatible), `vets55` (hard incompatible) |
| `vets45` | `vets45`, `vets40` (soft), `vets50` (soft), `vets55` (hard incompatible) |
| `vets50` | `vets50`, `vets45` (soft), `vets55` (soft) |
| `vets55` | `vets55`, `vets50` (soft) |

Soft match = appears in search, flagged as "age group differs". Hard incompatible = never shown.

**Rule of thumb:** age groups within 10 years of each other are soft-compatible. Beyond 10 years, hard incompatible.

---

### Age Group Compatibility Matrix

| | open | vets40 | vets45 | vets50 | vets55 |
|---|:---:|:---:|:---:|:---:|:---:|
| **open** | ✓ Hard | ✗ | ✗ | ✗ | ✗ |
| **vets40** | ✗ | ✓ Hard | ✓ Soft | ✗ | ✗ |
| **vets45** | ✗ | ✓ Soft | ✓ Hard | ✓ Soft | ✗ |
| **vets50** | ✗ | ✗ | ✓ Soft | ✓ Hard | ✓ Soft |
| **vets55** | ✗ | ✗ | ✗ | ✓ Soft | ✓ Hard |

---

## 3. Gender

### Gender Category Definitions

| Category ID | Label | Description |
|---|---|---|
| `mens` | Men's | Men's team |
| `womens` | Women's | Women's team |
| `mixed` | Mixed | Open gender; typically Sunday XI |

---

### Gender Compatibility Rules

| Team A | Can match with |
|---|---|
| `mens` | `mens` (hard); `mixed` (soft — needs mutual agreement) |
| `womens` | `womens` (hard); `mixed` (soft — needs mutual agreement) |
| `mixed` | `mixed` (hard); `mens` (soft); `womens` (soft) |

Mixed vs gendered-team matches appear in search with a flag: "Gender category differs — please confirm both teams are comfortable with this arrangement." The match request requires explicit acknowledgement.

---

### Gender Compatibility Matrix

| | mens | womens | mixed |
|---|:---:|:---:|:---:|
| **mens** | ✓ Hard | ✗ | ✓ Soft |
| **womens** | ✗ | ✓ Hard | ✓ Soft |
| **mixed** | ✓ Soft | ✓ Soft | ✓ Hard |

---

## 4. Ability Tier

### Tier Definitions (Self-Declared)

Ability tier is self-declared by the Club Admin when setting up a team. Teams may update it at the start of each season. The platform does not verify it.

| Tier | Label | Description |
|---|---|---|
| 1 | Recreational | Never played league cricket; pub team / first-time organised cricket |
| 2 | Club (lower) | Plays in an organised league, lower divisions; friendly and developmental |
| 3 | Club (mid) | Mid-division league cricket; competitive but not at county-league standard |
| 4 | Club (strong) | Top-division local league; strong county league standard |
| 5 | Elite amateur | Semi-professional; county 2nd XI-level or equivalent |

**Teams are encouraged to declare honestly.** The tier is visible on team profiles. Misrepresentation leads to poor fixture experiences; the platform relies on social incentive rather than enforcement.

---

### Tier Compatibility Rules

Tiers are used as a soft scoring factor in search ranking, not a hard filter. All tiers appear in each other's search results; tier distance affects the ranking score.

| Tier distance | Soft score contribution |
|---|---|
| 0 (same tier) | 1.00 |
| ±1 | 0.70 |
| ±2 | 0.30 |
| ±3 or more | 0.05 |

**There is no hard exclusion by tier.** A Tier 1 recreational team may still appear in results for a Tier 4 team's search, but ranked very low. This allows genuinely unusual matches to be arranged without the system blocking them.

---

## 5. Composite Compatibility

A fixture match passes the hard filter only if ALL of the following are true:

1. Format is hard-compatible OR soft-compatible (soft is allowed through to search)
2. Age group is hard-compatible OR soft-compatible
3. Gender is hard-compatible OR soft-compatible
4. Date window overlaps
5. Distance ≤ requested radius
6. No block in either direction

If any of items 1–3 are soft (not hard), the search result displays a compatibility notice. If all three are hard matches, no notice is shown.

---

## 6. Worked Examples

### Example A: Format hard match, tier mismatch

**Scenario:** Thornton CC 1st XI (T20, Open, Men's, Tier 4) searches for an opponent.

**Candidate:** Redfield CC 3rd XI (T20, Open, Men's, Tier 1)

| Check | Result |
|---|---|
| Format | T20 vs T20 → hard match ✓ |
| Age group | Open vs Open → hard match ✓ |
| Gender | Men's vs Men's → hard match ✓ |
| Tier distance | |4 - 1| = 3 → soft score = 0.05 |

**Output:** Redfield 3rd XI appears in search results but ranked low due to tier distance. No compatibility notice shown (all hard checks passed). Low tier-match score will push it far down the ranking.

**Why correct:** Tier is a soft factor. A Tier 4 team might knowingly want to play a Tier 1 team (e.g., a friendly for new players). The platform shows the option; ranking reflects the mismatch.

---

### Example B: Soft format match — notice triggered

**Scenario:** Merton Sunday XI (Sunday, Open, Mixed, Tier 2) searches for an opponent.

**Candidate:** Oldwick CC Sunday XI (40over, Open, Men's, Tier 2)

| Check | Result |
|---|---|
| Format | Sunday vs 40over → soft match ✓ (notice triggered) |
| Age group | Open vs Open → hard match ✓ |
| Gender | Mixed vs Men's → soft match ✓ (notice triggered) |
| Tier | |2 - 2| = 0 → score = 1.00 |

**Output:** Appears in results. Two compatibility notices displayed: "Format to be agreed (Sunday vs 40-over)" and "Gender category differs — mutual agreement needed."

**Why correct:** Both soft conditions must be resolved in the match request before the fixture proceeds. The search surfaces the option but flags the discussion items clearly.

---

### Example C: Hard incompatibility — not shown

**Scenario:** Hartwell CC 1st XI (Timed declaration, Open, Men's, Tier 3) searches.

**Candidate:** Southbury CC 1st XI (T20, Open, Men's, Tier 3)

| Check | Result |
|---|---|
| Format | Timed vs T20 → hard incompatible ✗ |

**Output:** Southbury CC 1st XI does not appear in Hartwell's search results.

**Why correct:** Timed declaration and T20 are fundamentally different game structures. Showing them as a match option would create fixture confusion.

---

### Example D: Veterans cross-tier, age group soft match

**Scenario:** Redfield CC Veterans 40+ (40over, Vets 40+, Men's, Tier 2) searches.

**Candidate:** Merton CC Veterans 50+ (40over, Vets 50+, Men's, Tier 2)

| Check | Result |
|---|---|
| Format | 40over vs 40over → hard match ✓ |
| Age group | Vets 40+ vs Vets 50+ → gap = 10 years → hard incompatible ✗ |
| Gender | Men's vs Men's → hard match ✓ |

**Output:** Merton Veterans 50+ does not appear in Redfield Veterans 40+ search.

**Why correct:** A 10-year veteran gap is the boundary. 40+ vs 50+ sits exactly at the boundary. The matrix shows this as hard incompatible (not even soft-compatible). If the age groups were 45+ vs 50+, that would be a soft match. This is a conservative rule; Agent 4 research may refine the boundary.

**FLAG FOR AGENT 4:** Is the 10-year veteran gap boundary consistent with how local leagues and friendly schedules actually work? Please validate before finalising.

---

### Example E: New club, no tier set

**Scenario:** Thornton Wanderers CC (newly registered, no tier selected yet) appears in a search.

| Check | Result |
|---|---|
| Tier | Not set → defaults to Tier 3 (mid-range) for ranking purposes |

**Output:** Appears in search with Tier 3 tier-match scoring until the Club Admin sets their tier. A prompt is shown on the club profile asking them to set their tier.

**Why correct:** Defaulting to the mid-range prevents new clubs from being ranked either artificially high (Tier 1 default would match against everyone well) or artificially low (Tier 5 default would rank them near the bottom). Mid-range is the fairest neutral starting point. The Club Admin can correct it immediately.
