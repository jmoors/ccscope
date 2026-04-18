# Agent 2 — Domain Model & Logic

## Briefing

### Purpose
Owns the invisible structure of the product: data model, state machine, permissions, matching algorithm, trust algorithm, notification matrix, edge-case handling.

### Why it matters
Everything else is wrapping around this. If the state machine is wrong, every screen is wrong. If the trust algorithm has a gaming vector, the whole product's credibility dies. This is the most consequential agent after Product Foundations.

### Deliverables
1. Fixture state machine (states, transitions, triggers, permissions)
2. Role and permissions matrix
3. Format / age / gender compatibility taxonomy
4. Matching algorithm specification with worked examples
5. Trust scoring algorithm with worked examples and edge cases
6. Notification matrix (event → channel → recipient → template reference)
7. Edge-case handling: cancellation, no-show, dispute, weather rearrangement, blocking
8. Data model ERD

### Inputs you provide
- Agent 1's outputs (scope, principles, metrics)
- Original scope document
- Domain research from Agent 4 (feeds in as it lands)
- Cricket-specific domain expertise (you'll need to ask or research)

### Expected outputs
- `01-fixture-state-machine.md`
- `02-roles-permissions.md`
- `03-format-taxonomy.md`
- `04-matching-algorithm.md`
- `05-trust-algorithm.md`
- `06-notification-matrix.md`
- `07-edge-cases.md`
- `08-data-model.md` (with ERD diagram)

### Timing
Weeks 2–6. Overlaps with Agent 4 research; expect to revise trust and matching based on research findings.

### Handoff criteria
- State machine has 100% transition coverage
- Every matching/trust rule has a worked example including edge cases
- Every edge case has a specified flow
- Data model reviewed by Agent 9 (engineering) for feasibility

### Common failure modes
- Treating format compatibility as a single flag
- Writing trust algorithms without simulating gaming vectors
- Missing the "fixture cancelled and needs rearrangement" flow
- Permissions models that don't handle one-person-manages-multiple-teams
- Notification matrix that ignores quiet hours and digest preferences
