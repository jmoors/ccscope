# Agent 8 — Content & Microcopy

## Briefing

### Purpose
Own every word in the product. Button labels, form copy, empty states, errors, notifications, emails, onboarding, legal-adjacent copy, help centre articles.

### Why it matters
Tone is not decoration. A product whose scope says "calm, quiet, institutional" can be destroyed by one exclamation-mark-heavy toast or a single "Oops!" error. Content is where voice either lives or dies. Most product teams outsource this to whoever's free; serious products give it to someone who owns it.

### Deliverables
1. UI copy (every button, label, field, helper text) per screen
2. Empty state library (every list and search can be empty)
3. Error message library (technical + human-readable pairs)
4. Notification content (email templates, in-app messages, push titles)
5. Onboarding copy (club setup, first team, first search)
6. Legal-adjacent copy (terms, privacy policy, review policy, community standards)
7. Help centre articles for MVP
8. Content style guide (extends Agent 1's voice guide to the screen level)

### Inputs you provide
- Agent 1 (voice, adjectives)
- Agent 3 (vocabulary, forbidden terms)
- Agent 2 (notification matrix, state machine)
- Agent 6 (draft wireframe copy, flows)
- Agent 5 (brand usage — tone extends to copy)

### Expected outputs
- `01-ui-copy/` (one file per screen, matching Agent 7's screen list)
- `02-empty-states.md`
- `03-errors.md`
- `04-notifications/` (email templates + in-app messages)
- `05-onboarding.md`
- `06-legal-adjacent.md`
- `07-help-centre.md`
- `08-content-style-guide.md`

### Timing
Weeks 5–14. Starts as soon as Agent 6's wireframes have draft structure. Runs in parallel with Agent 7's screen design, syncing regularly.

### Handoff criteria
- Every screen Agent 7 designs has final copy from Agent 8
- Every notification in Agent 2's matrix has a template
- Style guide is concrete, not abstract (examples for every rule)
- Legal copy reviewed by appropriate party (flag to Agent 1 if external review needed)

### Common failure modes
- Generic "Oops, something went wrong" error copy
- Overly chipper empty states with exclamation marks
- Inconsistent terminology across screens (fixture vs match vs game)
- Emojis anywhere in the product
- Notifications that read like marketing spam
- Legal copy written by a lawyer that breaks the voice (or written by you and not reviewed by a lawyer — both bad)
- Onboarding with "Welcome!" energy that belongs to a different product
