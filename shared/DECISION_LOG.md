# Decision Log

**Every significant cross-agent decision recorded here. Format: date, owner, decision, rationale, affects.**

---

## Template

```
### YYYY-MM-DD — [Title]
**Owner:** Agent N
**Decision:** [What was decided]
**Rationale:** [Why]
**Affects:** [Which agents/artefacts]
**Status:** Proposed / Accepted / Superseded
```

---

## Decisions

### 2026-04-19 — Name recommendation: Pavilion (awaiting stakeholder approval)
**Owner:** Agent 3
**Decision:** Pavilion recommended as primary name. FixtureDesk as runner-up. Neither finalised — stakeholder approval required before domain purchase or handoff to Agent 5/10.
**Rationale:** Pavilion matches the institutional, calm, cricket-literate register; it is the architectural heart of every cricket ground and evokes the right comparison points (National Trust, well-run county club). FixtureDesk retained as runner-up if domain strategy proves unworkable or stakeholders prefer explicit function telegraphing.
**Affects:** Agent 5 (Brand Identity — blocked until name locked), Agent 10 (Launch — domain purchase pending approval)
**Status:** Proposed

### 2026-04-19 — Glossary version-bumped to 1.1
**Owner:** Agent 3
**Decision:** `shared/GLOSSARY.md` updated to v1.1 with expanded vocabulary. Full canonical vocabulary in `03-naming-verbal/outputs/05-vocabulary.md`.
**Rationale:** Baseline glossary (v1.0) covered entities and verbs only. V1.1 adds status rationale, notification patterns, empty state rules, forbidden language (extended), cricket domain term usage guidance.
**Affects:** All agents — canonical terminology reference updated
**Status:** Accepted

### 2026-04-19 — Product Foundations deliverables complete
**Owner:** Agent 1
**Decision:** All five Product Foundations documents published to `01-product-foundations/outputs/`. Agents 2, 3, 4, 5, 6, 7, 8, 9, 10 may now begin work subject to their own dependency chains.
**Rationale:** Blocking deliverable; all other agents depend on scope, voice, and decision rights being canonical.
**Affects:** All agents
**Status:** Accepted

### 2026-04-19 — Colts/junior fixtures deferred from MVP
**Owner:** Agent 1
**Decision:** No junior or colts fixture coordination in v1.
**Rationale:** Safeguarding requirements need separate policy work before we can responsibly accommodate under-18 users.
**Affects:** Agents 2, 6, 9
**Status:** Accepted

### 2026-04-19 — Match request expires after 7 days (no response)
**Owner:** Agent 1
**Decision:** Unanswered match requests expire at 7 days. Sending team notified; fixture reverts to Awaiting opponent.
**Rationale:** Prevents fixture limbo; creates a predictable flow for both parties.
**Affects:** Agent 2 (state machine), Agent 8 (notifications), Agent 9 (engineering)
**Status:** Accepted

### 2026-04-19 — Block is silent (non-disclosure to blocked party)
**Owner:** Agent 1
**Decision:** When a club blocks another, the blocked club is not notified and cannot see the block.
**Rationale:** Public blocking creates conflict; silent blocking achieves the safety goal without confrontation.
**Affects:** Agent 2, Agent 9
**Status:** Accepted

### 2026-04-19 — Platform scope excludes chat in MVP
**Owner:** Agent 1
**Decision:** No open messaging between users in MVP. Structured request fields only.
**Rationale:** Avoids moderation load; forces clarity in request/accept flow.
**Affects:** Agents 2, 6, 7, 8, 9
**Status:** Accepted (per original scope)

### 2026-04-19 — Service provider marketplace scoped down
**Owner:** Agent 1
**Decision:** v1 = request umpire from own club's roster only. Open umpire marketplace deferred.
**Rationale:** Half-built marketplaces produce bad UX. Defer until team-side has density.
**Affects:** Agents 2, 6, 7, 9
**Status:** Accepted

---

### 2026-04-19 — Trust score uses Bayesian smoothing with α=3, prior μ₀=0.70
**Owner:** Agent 2
**Decision:** Trust aggregation uses `bayesian_score = (raw_sum + 3 × 0.70) / (N + 3)`. New clubs start at 0.70 (neutral-positive). Badge thresholds: Reliable ≥ 0.72 with N ≥ 5; Established ≥ 0.78 with N ≥ 15 and activity within 2 seasons.
**Rationale:** Bayesian smoothing prevents single-review outliers dominating scores and ensures new clubs start neutral rather than at zero. Prior of 0.70 embeds the assumption that most clubs are probably reliable.
**Affects:** Agents 7 (badge display), 8 (review prompts), 9 (implementation)
**Status:** Accepted

### 2026-04-19 — Short-notice cancellation injects synthetic review_score = 0.0
**Owner:** Agent 2
**Decision:** Any non-weather cancellation within 48 hours of the fixture date injects a synthetic review with score 0.0 into the cancelling team's trust record, regardless of whether reviews are subsequently submitted.
**Rationale:** Prevents the gaming vector of cancelling to escape review consequences. Weather cancellations are exempt.
**Affects:** Agents 8 (notification copy), 9 (implementation)
**Status:** Accepted

### 2026-04-19 — Matching algorithm uses 6-factor weighted score; new clubs receive neutral priors
**Owner:** Agent 2
**Decision:** Matching composite score = 0.25×distance + 0.20×tier + 0.20×trust + 0.15×response_rate + 0.10×home_away + 0.10×activity. New clubs (< 5 reviews) receive trust, response_rate, and activity priors of 0.70 each.
**Rationale:** Multi-factor ranking prevents any single signal (e.g., proximity) from dominating. Neutral priors for new clubs implement the "never punish new entrants" principle.
**Affects:** Agent 9 (implementation), Agent 4 (weight validation from research)
**Status:** Accepted — weights provisional pending Agent 4 research

### 2026-04-19 — Ability tier is self-declared; no hard exclusion by tier
**Owner:** Agent 2
**Decision:** Tier (1–5) is self-declared by Club Admin. All tiers appear in each other's search results; tier distance is a soft score only (±2 = 0.30; ±3+ = 0.05). No tier-based hard filter.
**Rationale:** Hard tier exclusion would require verification the platform cannot provide, and would block legitimate unusual match arrangements. Social incentive (poor fixture experience) is sufficient enforcement for honest self-declaration.
**Affects:** Agents 3 (tier label copy), 7 (tier display), 9
**Status:** Accepted

### 2026-04-19 — Veterans age-group compatibility boundary set at 10-year gap
**Owner:** Agent 2
**Decision:** Veterans age groups within 10 years of each other are soft-compatible; beyond 10 years, hard incompatible. (e.g., 40+ vs 50+: hard incompatible; 45+ vs 50+: soft-compatible.)
**Rationale:** Provisional; needs validation from Agent 4. The 10-year boundary is a conservative default. Edge: 40+ vs 50+ sits exactly at the boundary and is excluded.
**Affects:** Agent 4 (validation), Agent 9 (filter implementation)
**Status:** Proposed — pending Agent 4 research validation

### 2026-04-19 — Brand identity deliverables complete; tokens ready for Agent 7
**Owner:** Agent 5
**Decision:** All seven brand identity deliverables published to `05-brand-identity/outputs/`. Design tokens in W3C DTCG format (`08-design-tokens.json`) ready for Agent 7 review and sign-off.
**Rationale:** Primary colour: Forest `#1d3a2b` (deep green — institutional, not heritage-cliché). Accent: Amber `#8a5c1a` (warm, WCAG AA on white). Typefaces: Source Serif 4 (headings/wordmark) + Source Sans 3 (UI), both SIL OFL 1.1. Wordmark: "Pavilion" in Source Serif 4 Medium. Anti-cliché checklist cleared. WCAG 2.2 AA audit passed.
**Affects:** Agent 7 (Design System — must review and sign off on `08-design-tokens.json`). Agent 9 (Engineering — font loading and token CSS variables). Contingent on Pavilion name approval.
**Status:** Proposed (pending Agent 7 token sign-off; name decision also Proposed)

*Add decisions in reverse chronological order.*
