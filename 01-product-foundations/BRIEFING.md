# Agent 1 — Product Foundations

## Briefing (for the human running this agent)

### Purpose
This agent owns the single source of truth for what the product is and isn't. Everything else flows from here. Run this agent first; it blocks all others.

### Why it matters
Multi-agent projects fail when agents silently interpret scope differently. This agent produces the canonical scope document, voice guide, and success metrics that every other agent must conform to.

### Deliverables
1. Positioning statement (one page)
2. Voice and tone guide with do/don't examples
3. Brand adjectives: 3–5 must-embody, 3–5 must-avoid
4. Confirmed MVP scope with explicit out-of-scope list
5. Success metrics (leading and lagging) with measurement approach
6. Guiding product rules (expanded from the original 5)
7. A decision-rights matrix: who signs off on what

### Inputs you provide
- The original scope document
- The user journey paths document
- The UX review feedback (gaps, risks, recommendations)
- Stakeholder names and decision-rights preferences

### Expected outputs
- `01-positioning.md`
- `02-voice-and-tone.md`
- `03-mvp-scope-confirmed.md`
- `04-success-metrics.md`
- `05-decision-rights.md`

### Timing
Week 1–2. Must complete before most other agents can meaningfully start.

### Handoff criteria
- All five documents reviewed and signed off by stakeholders
- Uploaded to shared location
- Announced in decision log
- Every other agent has acknowledged receipt

### Common failure modes
- Producing generic scope documents that don't make hard tradeoffs
- Avoiding the "out of scope" section because it feels negative
- Voice guides that are too abstract to apply (fix: concrete do/don't examples)
- Success metrics that can't actually be measured
