# 05 — Decision Rights Matrix

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 1 (Product Foundations)

---

## How to read this document

- **Owner** — makes the final call; records outcome in `shared/DECISION_LOG.md`
- **Consulted** — must be heard before decision is made; can raise blockers
- **Informed** — notified of outcome; no blocking right

If an owner is not available within 48 hours of a decision being needed, escalate to the default escalation path below.

---

## Decision matrix

### Product scope

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Add a feature to MVP scope | Agent 1 | Agents 2, 6, 9 | All agents |
| Remove a feature from MVP scope | Agent 1 | Agents 2, 6, 9 | All agents |
| Defer an edge case | Agent 1 | Affected agents | All agents |
| Change the scope change process itself | Agent 1 | All agents | All agents |

### Domain model and data

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Core entity definitions (Fixture, Club, Team, etc.) | Agent 2 | Agent 1, Agent 9 | Agents 6, 7, 8 |
| Fixture state machine (statuses and transitions) | Agent 2 | Agent 1, Agent 6 | All agents |
| Trust score algorithm | Agent 2 | Agent 1 | Agents 7, 8, 9 |
| Data model changes that affect UI flows | Agent 2 | Agents 6, 7 | Agent 9 |

### Naming and language

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Product name | Agent 3 | Agent 1, Agent 5 | All agents |
| Glossary additions or changes | Agent 3 | Agent 1 | All agents |
| Voice and tone rules | Agent 1 | Agent 3, Agent 8 | All agents |
| Screen-level microcopy | Agent 8 | Agent 3, Agent 7 | Agent 6 |

### Research and discovery

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Research scope and methodology | Agent 4 | Agent 1 | All agents |
| Findings that contradict current scope | Agent 4 (flags); Agent 1 (decides) | Agents 2, 6 | All agents |
| User interview recruitment | Agent 4 | Agent 1 | — |

### Brand and visual identity

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Visual identity (colour, type, mark) | Agent 5 | Agent 1, Agent 3 | All agents |
| Design system tokens | Agent 7 | Agent 5 | Agents 6, 8, 9 |
| Accessibility decisions (above WCAG minimum) | Agent 7 | Agent 1, Agent 9 | All agents |
| Brand extension (new context, new format) | Agent 5 | Agent 1 | All agents |

### Information architecture and flows

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Navigation structure | Agent 6 | Agent 1, Agent 7 | Agents 8, 9 |
| Flow design (user journeys) | Agent 6 | Agent 2, Agent 7 | Agents 8, 9 |
| Feature placement (where a feature lives in the IA) | Agent 6 | Agent 1 | Agents 7, 8 |

### Design and components

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Component design | Agent 7 | Agents 5, 6 | Agent 9 |
| Screen-level layout decisions | Agent 7 | Agent 6, Agent 8 | Agent 9 |
| Mobile vs. desktop priority trade-offs | Agent 7 | Agent 1, Agent 6 | Agent 9 |

### Engineering

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Technical architecture | Agent 9 | Agent 2 | Agent 1 |
| Instrumentation schema (event names, properties) | Agent 9 | Agent 1 | Agents 2, 6 |
| Technology choices | Agent 9 | Agent 1 | — |
| Performance budgets | Agent 9 | Agent 7 | Agent 1 |

### Launch

| Decision type | Owner | Consulted | Informed |
|---|---|---|---|
| Launch sequencing | Agent 10 | Agent 1, Agent 9 | All agents |
| Partnership decisions | Agent 10 | Agent 1 | All agents |
| Go / no-go for launch | Agent 1 | Agents 9, 10 | All agents |

---

## Escalation path

When agents disagree and cannot resolve among themselves:

1. Either agent posts the disagreement to `shared/DECISION_LOG.md` with status "Proposed" and a clear statement of the options.
2. Agent 1 reviews within 48 hours and either decides or convenes a structured async discussion.
3. If the disagreement involves a scope question, Agent 1 has final authority.
4. If the disagreement involves a domain model question, Agent 2 has final authority within the scope Agent 1 has confirmed.
5. If the disagreement is between agents 5 and 7 (brand vs. design system), Agent 5 has authority on identity; Agent 7 has authority on component execution.
6. If Agent 1 is the source of the disagreement, the human running the project decides.

No agent implements a disputed decision until it is resolved and recorded.

---

## Scope change authority

Only Agent 1 can approve scope changes. The process is in `03-mvp-scope-confirmed.md`.

Features added by agents without approval will be flagged for removal in Agent 9's code review gate.

---

## Brand change authority

Only Agent 5 can approve changes to visual identity (colour, type, mark). Only Agent 3 can approve changes to naming and core vocabulary. Changes that affect both require both owners to agree.

Agent 1 has veto on brand decisions that contradict the must-embody / must-avoid adjectives in `01-positioning.md`.

---

## Standing delegations

These decisions are delegated to the named agent without requiring Agent 1 sign-off each time:

| Delegation | Delegated to | Scope |
|---|---|---|
| Microcopy for existing flows | Agent 8 | Must conform to voice guide; no new terms |
| Component variants within approved design system | Agent 7 | Must not introduce new patterns |
| Instrumentation event naming | Agent 9 | Must follow naming schema in their own artefact |
| Research recruitment and logistics | Agent 4 | Budget and scope pre-approved by Agent 1 |
