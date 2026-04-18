# Agent 9 — Engineering

## Briefing

### Purpose
Build the actual product. Technical architecture, data model implementation, matching and trust algorithm implementation, notification system, API, front-end, instrumentation, closed beta environment.

### Why it matters
This is where every other agent's work becomes real or doesn't. Poor engineering produces a product that contradicts its own scope (chatty when meant to be calm, slow when meant to be trusted, buggy when meant to be reliable). Good engineering makes the restraint elsewhere actually felt by users.

### Deliverables
1. Technical architecture document
2. Auth, user, club, team, permissions system
3. Fixture state machine implementation (matches Agent 2 spec exactly)
4. Matching and search implementation
5. Trust algorithm implementation
6. Notification system (email + in-app, push deferred)
7. API and data model
8. Front-end implementation consuming Agent 7's components
9. Instrumentation for success metrics
10. Closed beta environment
11. Admin tools for internal operations (dispute resolution, support)

### Inputs you provide
- Agent 1 (scope, metrics)
- Agent 2 (data model, state machine, algorithms — implement exactly)
- Agent 5 (design tokens — consumable formats)
- Agent 7 (component library, screens)
- Agent 8 (copy strings, notification templates)
- Agent 4 (seed data if partnership delivers fixture imports)

### Expected outputs
- `01-architecture.md`
- `02-tech-stack-decision.md`
- `03-data-model-implementation.md`
- `04-api-specification.md` (OpenAPI)
- `05-instrumentation-plan.md`
- `06-security-and-privacy.md`
- `07-deployment-and-environments.md`
- `08-admin-tools-spec.md`
- `09-engineering-runbook.md`
- Working software in version control

### Timing
Weeks 5–20. Architecture starts when Agent 2's data model is stable. Full build starts once Agent 7's design system is usable. Continues through beta.

### Handoff criteria
- Closed beta environment live
- All MVP flows implemented
- Instrumentation in place for success metrics
- Admin tools sufficient for launch operations
- Agent 2's algorithms implemented with worked examples passing as tests
- Agent 7's designs implemented with high fidelity

### Common failure modes
- Drifting from Agent 2's spec silently (implementing "close enough" algorithms)
- Using browser localStorage / sessionStorage where persistent storage is needed
- Over-engineering the data model for features deferred to v2
- Notifications system that ignores digest preferences and quiet hours
- Trust algorithm gaming vectors not unit-tested
- Poor instrumentation that leaves success metrics unmeasurable
- Accessibility regressions in implementation that passed in design
- Ignoring mobile performance (the user on a 2018 phone in a car park)
