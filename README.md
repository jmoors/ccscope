# Cricket Match Coordination Platform — Agent Briefing Package

Complete briefing materials for 10 AI agents handling the design and build of a cricket match coordination platform.

## Structure

```
cricket-platform-agents/
├── README.md                     ← You are here
├── shared/
│   ├── PROJECT_CONTEXT.md        ← Read by every agent
│   ├── GLOSSARY.md               ← Canonical vocabulary
│   └── DECISION_LOG.md           ← Cross-agent decisions
├── 01-product-foundations/
├── 02-domain-model/
├── 03-naming-verbal/
├── 04-discovery-research/
├── 05-brand-identity/
├── 06-ia-flows/
├── 07-design-system/
├── 08-content-microcopy/
├── 09-engineering/
└── 10-launch-partnerships/
```

Each agent folder contains:
- `BRIEFING.md` — for the human running the agent. Purpose, why it matters, deliverables, timing, failure modes.
- `PROMPT.md` — the prompt you paste into the agent to kick it off.
- `CLAUDE.md` — the agent's operating instructions (identity, hard rules, collaboration protocol, done criteria).

Each agent also needs a scratch `outputs/` and `inbox/` subfolder, which you create when running them.

## How to use

### For human project leads

1. Read `shared/PROJECT_CONTEXT.md` first. This is the one-pager every agent works from.
2. Read `README.md` in each agent folder (the BRIEFING) to understand what that agent does and where it sits in the sequence.
3. Sequence the agents according to the dependency map below — don't start Agent 5 before Agent 3 is done.

### For running each agent

1. Open the agent's folder.
2. Ensure the shared files and upstream agent outputs are in place.
3. Paste `PROMPT.md` as the user message to the agent.
4. Attach `CLAUDE.md` as the system/operating instructions.
5. Let the agent produce its deliverables into `outputs/`.
6. Review, accept, or request revisions.

## Dependency order

```
Week 1–2:   Agent 1 (Foundations)
            │
            ├─→ Agent 3 (Naming)
            ├─→ Agent 4 (Research)  ─────┐
            └─→ Agent 2 (Domain)  ───┐   │
                                     │   │
Week 3–4:                            ↓   │
            Agent 6 (IA) starts  ←───┤   │
            Agent 5 (Brand) waits for Agent 3
                                         │
Week 5–8:                                │
            Agent 5 (Brand) ──→ Agent 7 (Design System)
            Agent 8 (Content) runs parallel with Agent 7
            Agent 9 (Engineering) starts architecture
                                         │
Week 8–16:                               │
            Full build (Agent 9)         │
            Agent 7, 8 support build     │
            Agent 4 continues research ──┘
            Agent 10 (Launch) developing partnerships throughout

Week 15–20: Closed beta launch
            Agent 10 runs launch
            All other agents support as needed
```

## Decision log protocol

Any decision that affects another agent's work gets an entry in `shared/DECISION_LOG.md`. Template is in the file.

## Glossary protocol

`shared/GLOSSARY.md` is owned by Agent 3 but used by all. Agents propose additions via their agent's `inbox/`. Agent 3 approves and merges with a version bump.

## Collaboration protocol

- Questions to another agent go in that agent's `inbox/` folder
- Responses expected within 24–48 hours depending on criticality
- Silent deviation from a specification is the primary failure mode to guard against — when in doubt, flag it

## Realistic team mapping

This is 10 agents. It is not 10 humans. In practice:

- A solo founder or tiny team: one person wears most hats but uses the agent structure to keep thinking clear
- A small team (3–4 people): roughly Product/Design/Engineering/Ops splits, with agents mapped to phases of each
- A larger team: closer to 1:1 mapping, though Agents 5, 8 often consolidate

The value is not in the headcount match. It is in each artefact having a clear owner, clear inputs, clear outputs, and clear handoff criteria.

## A few notes on agent behaviour

- Every agent has explicit "not your job" boundaries to prevent scope creep between agents
- Every agent has escalation triggers to prevent stuck silent disagreements
- Every agent has done criteria to prevent endless iteration
- Every agent references `shared/` documents rather than duplicating them

## What's deliberately missing

- Analytics / BI specialist — Agent 9 owns instrumentation in MVP
- Legal — flagged for external engagement by Agent 8 and Agent 1
- Finance / monetisation — out of MVP scope per Agent 1
- Customer success at scale — Agent 10 handles beta; scale is post-MVP

## Maintenance

This package is a starting position. Expect to revise:
- After Agent 4's initial research findings
- After Agent 6's usability testing
- At beta launch
- After 3 months of real usage

Version the shared files. Update agents' prompts if scope changes.

---

**Package version:** 1.0
**Date:** April 2026
