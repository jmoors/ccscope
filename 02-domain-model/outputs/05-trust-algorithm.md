# 05 — Trust Scoring Algorithm

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 2 (Domain Model & Logic)  
**Status:** Draft — badge thresholds provisional; review questions to be validated by Agent 4

---

## 1. Design Principles

1. Trust is a lagging signal, not a real-time score. It reflects a track record, not a single event.
2. New clubs start neutral, not penalised.
3. The algorithm must resist gaming without requiring platform moderation of individual reviews.
4. The score is never shown as a number or percentage — only as a badge. This prevents users from obsessing over marginal differences.
5. Reviews are private. A club cannot see who reviewed them or what individual reviews said.
6. The algorithm errs on the side of caution: it takes more evidence to move a club up than to flag one as needing attention.

---

## 2. Review Dimensions and Questions

Every post-match review asks three questions. Question wording is set by Agent 8 (microcopy); the categories and scoring structure are defined here.

| Dimension | Internal ID | Question intent |
|---|---|---|
| Reliability | `Q_RELIABILITY` | Did the fixture happen as planned? Did the opposing team honour the commitment? |
| Preparedness | `Q_PREPAREDNESS` | Was the opposing team ready? (arrived on time, full squad, correct kit, tea arranged) |
| Recommendation | `Q_RECOMMENDATION` | Would you arrange another fixture with this club? |

**Scoring scale:**

| Answer | Numeric value |
|---|---|
| Yes | 1.0 |
| Mostly | 0.5 |
| No | 0.0 |

A review has a score in the range [0.0, 1.0]:

```
review_score = (Q_RELIABILITY + Q_PREPAREDNESS + Q_RECOMMENDATION) / 3.0
```

A review with Yes/Yes/Yes = 1.0. Yes/Mostly/No = 0.5. No/No/No = 0.0.

**Review constraints:**
- Only one review may be submitted per team per fixture.
- The submitter is the Fixture Manager who managed the fixture.
- Reviews are anonymous to the receiving club. The platform stores the submitter ID but never surfaces it.
- Reviews cannot be edited after submission.
- Review window: 7 days after `fixture.completed_at`. Reviews submitted after 7 days are rejected.

---

## 3. Aggregation Method

### Bayesian Score

The trust score uses Bayesian smoothing to handle sparse data. Without smoothing, a club with 1 perfect review would score 1.0 — indistinguishable from a club with 50 perfect reviews.

```
bayesian_score = (raw_sum + α × μ₀) / (N + α)
```

Where:
- `raw_sum` = sum of all `review_score` values received by this team
- `N` = number of reviews received
- `α` = 3.0 (confidence weight; equivalent to 3 "neutral" phantom reviews)
- `μ₀` = 0.70 (prior mean; we assume new clubs are probably reliable)

**Interpretation:**
- A new club (N = 0): bayesian_score = (0 + 3 × 0.70) / (0 + 3) = 0.70
- A club with 3 perfect reviews: (3.0 + 2.1) / (3 + 3) = 5.1 / 6 = 0.85
- A club with 50 reviews, all perfect: (50 + 2.1) / (53) = 0.983
- A club with 10 reviews averaging 0.4: (4.0 + 2.1) / (13) = 0.469

---

### Short-Notice Cancellation Penalty

Short-notice cancellations (< 48 hours, non-weather) inject a synthetic review with `review_score = 0.0` into the club's review pool. This review is system-generated and cannot be suppressed.

```
synthetic_review_score = 0.0
```

The synthetic review is added to `raw_sum` and `N` as if it were a normal review.

**Why 0.0 and not a partial penalty:** A short-notice cancellation fails all three dimensions: reliability (fixture didn't go ahead), preparedness (presumably not ready), and recommendation (would you fix with a team that cancels?). A 0.0 is the correct representation.

**Weather exemption:** `cancellation.weather = true` suppresses the synthetic injection. Weather cancellations are shared misfortune, not a reliability failure.

---

## 4. Badge Definitions and Thresholds

### Thresholds

| Badge | User-facing | Condition |
|---|---|---|
| **New** | New | `N < 5` (fewer than 5 reviews received) |
| **Reliable** | Reliable | `N ≥ 5` AND `bayesian_score ≥ 0.72` |
| **Established** | Established | `N ≥ 15` AND `bayesian_score ≥ 0.78` AND `last_completed_fixture ≤ 2 seasons ago` |
| **Needs attention** | *(not shown publicly)* | `N ≥ 3` AND `bayesian_score < 0.45` |

**Badge priority (when conditions conflict):**
- If "Needs attention" threshold met, internal flag is set regardless of N.
- Public-facing badge: "New" if N < 5, else "Reliable" or "Established" per score thresholds.
- A club can be "Needs attention" internally and still show "Reliable" publicly during early review period (N ≥ 5 but < 15). The internal flag triggers moderation review; the public badge is not immediately downgraded.

**Badge transitions are hysteretic (require ≥ 3 reviews to downgrade):**
- To prevent oscillation from a single bad review, a badge can only drop after `bayesian_score` has been below threshold for 2 consecutive months (or after 3 reviews push it below threshold). This is implemented by comparing `bayesian_score` at the end of each calendar month.

---

### Worked Threshold Examples

| Scenario | N | raw_sum | bayesian_score | Badge |
|---|---|---|---|---|
| New club | 0 | 0.0 | 0.70 | New |
| 3 perfect reviews | 3 | 3.0 | 0.85 | New (N < 5) |
| 5 reviews, all Yes | 5 | 5.0 | (5 + 2.1) / 8 = 0.888 | Reliable |
| 5 reviews, mixed | 5 | 3.0 | (3 + 2.1) / 8 = 0.638 | New (score < 0.72; N ≥ 5 but score too low) |
| 5 reviews, very poor | 5 | 1.0 | (1 + 2.1) / 8 = 0.388 | New (public); Needs attention (internal) |
| 15 reviews, score 0.79 | 15 | 11.85 | (11.85 + 2.1) / 18 = 0.775 | Reliable (not yet 0.78; misses Established) |
| 20 reviews, score 0.85 | 20 | 17.0 | (17 + 2.1) / 23 = 0.83 | Established |

---

## 5. Decay Rules

### Confidence decay for inactive clubs

If a club has not completed a fixture in > 3 seasons (3 years), the confidence weight α increases, pulling the bayesian_score toward the prior:

```
seasons_inactive = max(0, floor((today - last_completed_fixture) / 365) - 3)
effective_α = α × 2^seasons_inactive
bayesian_score = (raw_sum + effective_α × μ₀) / (N + effective_α)
```

**Effect:**
- After 4 seasons of inactivity: effective_α = 6 (doubles once)
- After 5 seasons: effective_α = 12
- An Established club with perfect reviews slowly drifts toward 0.70 (prior), eventually losing "Established" badge, then "Reliable"

**Why this design:**
- Does not punish clubs for past reliability; it reduces confidence that their past behaviour predicts future behaviour.
- A club that returns after inactivity keeps their accumulated reviews; a few new positive fixtures will quickly restore their badge.

**No negative decay:** The score never goes below the prior (0.70) due to inactivity alone. Inactivity reduces confidence; only actual negative reviews reduce the score below the prior.

---

## 6. Review Submission and Retaliation Mitigation

### Blind submission

Reviews are submitted in a one-way blind window:
- After a fixture is marked complete, both teams have 7 days to submit a review.
- Neither team can see whether the other has submitted a review.
- The platform does not reveal individual review scores to anyone; only the aggregate badge is visible.

**Effect on retaliation:** A club cannot retaliate in response to a negative review because they never know what score they received. If Club A and Club B both review each other after a bad experience, both reviews are genuine (reflecting real impressions) not tactical retaliations.

### Review from a blocked club

If Club A has blocked Club B, and the block is applied after a fixture has been completed, Club B can still submit a review for that fixture. The review is accepted. Blocking affects future interactions only.

### Review by a club that later joins a collusion ring

Reviews are linked to the specific fixture event. Historical reviews cannot be retroactively altered by any user action. If a collusion ring is detected, platform moderation can flag specific reviews as suspect; flagged reviews are excluded from the `raw_sum` and `N` calculation.

---

## 7. Gaming Analysis

### Attack 1: Review bombing (coordinated negative reviews)

**Goal:** Damage a competitor's trust score to push them down in search rankings.

**Method:** A group of colluding clubs each arrange a fixture with the target club, then submit No/No/No reviews after each game.

**Algorithm's resistance:**
- Each negative review requires a completed fixture. The attackers must physically turn up, play the game, and then submit reviews. This means the target club has also completed fixtures — the Bayesian model increases confidence with each data point, meaning the target's score converges faster toward its "true" level.
- Rate limiting: each pair of clubs can only submit one review per fixture event. A club cannot submit multiple reviews for the same game.
- If 5 colluding clubs each play the target once: 5 reviews, all 0.0. bayesian_score = (0 + 2.1) / (5 + 3) = 0.263. This is genuinely damaging. However, it requires 5 real matches. The target will also have other reviews from legitimate partners.

**Residual risk:** A coordinated bombing campaign by 5–10 clubs playing legitimate fixtures could suppress a target's score. Mitigation: platform moderation monitors for unusual review patterns (many 0.0 reviews from clubs that only ever played each other once). High-severity; requires monitoring tooling.

---

### Attack 2: Collusion ring (coordinated positive reviews)

**Goal:** Inflate a club's trust score to reach "Established" badge faster.

**Method:** 5 clubs form a ring, each playing each other in rotation, all submitting Yes/Yes/Yes reviews.

**Algorithm's resistance:**
- Bayesian smoothing has diminishing returns. Moving from "Reliable" to "Established" requires N ≥ 15 AND bayesian_score ≥ 0.78. With perfect reviews, that's achievable with 15 games.
- A club would need to play 15 fixtures with colluding partners in a season to achieve this. A typical club plays 20–30 fixtures per season; 15 collusion-ring games is a large fraction of a club's season.
- Crucially: to play 15 games, you must turn up and play cricket. The behaviour required to game the algorithm (showing up reliably, playing 15 games in a season) is exactly the behaviour we want to reward.

**Residual risk:** Low. A club that plays 15 real fixtures and gets positive reviews deserves a good score regardless of their relationship with the reviewers.

---

### Attack 3: Ghost fixture cancellation (evading negative review)

**Goal:** After a bad performance or no-show, cancel the fixture before it is marked complete, so no review prompt is triggered.

**Method:** After an embarrassing game or no-show, the Fixture Manager cancels the fixture within the platform before marking it complete.

**Algorithm's resistance:**
- Short-notice cancellation (< 48h) triggers a synthetic review_score = 0.0, injected into the cancelling club's record.
- If the club cancels before the game starts (within 48h of the fixture date), the synthetic penalty fires.
- If the club simply never marks the fixture complete, the platform can detect this: fixtures where the date has passed and no "complete" event has been recorded within 7 days are flagged for FM follow-up. After 14 days, the fixture is automatically marked complete.

**Residual risk:** A club might consistently not mark fixtures complete to avoid review prompts. The 14-day auto-complete mitigates this, but there is a 14-day window. Long-term pattern of unresolved fixtures should trigger an internal flag.

---

### Attack 4: New identity reset

**Goal:** A club flagged as "Needs attention" re-registers with a new account to reset their trust to neutral (New badge).

**Method:** Create a new club profile, abandon the old one.

**Algorithm's resistance:**
- "New" badge is neutral (0.70 effective score), not positive. The resetting club gains nothing beyond neutral standing.
- "Needs attention" is internal-only. If a club is fleeing a "Needs attention" flag, they reset to "New" — no advantage over other new clubs.
- The platform should flag duplicate club names and email domains at registration for manual review.

**Residual risk:** Low strategic value. The attack gains neutrality, not advantage. Monitoring for duplicate registrations reduces even this.

---

### Attack 5: Retaliation review

**Goal:** A club that receives (or suspects) a negative review from Club B retaliates with a negative review for Club B.

**Method:** After a contentious fixture, Club A anticipates a negative review from Club B and submits a pre-emptive negative review.

**Algorithm's resistance:**
- Reviews are submitted in the blind window (§6). Club A cannot see Club B's review until after the window closes, and even then, individual scores are never surfaced — only the aggregate badge.
- A pre-emptive negative review is only harmful if Club A's review is dishonest. If the fixture genuinely went badly for both sides, both clubs giving each other poor reviews is an accurate signal.

**Residual risk:** If Club A and Club B have an ongoing rivalry and habitually submit negative reviews for each other regardless of fixture quality, both will accumulate accurate-looking but unfair scores. No algorithmic defence against this pattern; requires moderation escalation if flagged by either party.

---

### Attack 6: Strategic review timing (withholding)

**Goal:** By choosing when to submit reviews, manipulate score calculations.

**Method:** A club submits its review only when the opponent has submitted theirs first (impossible due to blind window), or waits until a fixture goes well to submit a review and skips after bad fixtures.

**Algorithm's resistance:**
- The blind window prevents knowledge of whether the opponent submitted.
- Non-submission is not recorded as a data point in either direction. The club simply has fewer reviews, not worse reviews.
- The RECEIVING club's review for the SUBMITTING club is what matters. A club that never submits reviews receives fewer incoming reviews (partner clubs may reciprocate the lack of engagement), but submitting or not submitting does not directly affect your own score.

**Residual risk:** Low. Selectively not reviewing after bad games means fewer data points for the target club, which leaves them at their prior (0.70) rather than pulling them down. This slightly protects genuinely poor clubs from accurate negative signals, but the effect is bounded.

---

## 8. Review Prompt Lifecycle

```
fixture.completed_at = T

T + 0h: Review prompt sent to both FMs (REVIEW_PROMPT notification)
T + 72h: Reminder sent if no review submitted (REVIEW_REMINDER notification)
T + 7d: Review window closes; unsubmitted reviews can no longer be submitted
```

Reviews submitted after `T + 7d` are rejected with an error. The 7-day window is firm.

---

## 9. Worked Example — Full Trust Calculation

**Club:** Oldwick CC 1st XI

**History:**

| Fixture | Q_RELIABILITY | Q_PREPAREDNESS | Q_RECOMMENDATION | review_score |
|---|---|---|---|---|
| 1 | Yes | Yes | Yes | 1.0 |
| 2 | Yes | Mostly | Yes | 0.833 |
| 3 | Yes | Yes | Yes | 1.0 |
| 4 | Yes | Yes | Mostly | 0.833 |
| 5 | Mostly | Mostly | Yes | 0.667 |
| 6 *(synthetic — short-notice cancel)* | — | — | — | 0.0 |
| 7 | Yes | Yes | Yes | 1.0 |
| 8 | Yes | No | Yes | 0.667 |

```
N = 8
raw_sum = 1.0 + 0.833 + 1.0 + 0.833 + 0.667 + 0.0 + 1.0 + 0.667 = 6.0

bayesian_score = (6.0 + 3 × 0.70) / (8 + 3)
              = (6.0 + 2.1) / 11
              = 8.1 / 11
              = 0.736
```

**Badge check:**
- N = 8 ≥ 5 → not "New"
- bayesian_score = 0.736 ≥ 0.72 → "Reliable" ✓
- N = 8 < 15 → not "Established"

**Result:** Oldwick CC 1st XI shows the **Reliable** badge.

**Why correct:** Despite the short-notice cancellation injecting a 0.0 review, the majority of their history is positive. Bayesian smoothing tempers both the impact of the single bad review (synthetic) and prevents overconfidence from the otherwise-strong reviews. The Reliable badge is accurate.
