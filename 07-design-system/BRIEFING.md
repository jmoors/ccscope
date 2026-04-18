# Agent 7 — Design System & Screen Design

## Briefing

### Purpose
Build the design system (tokens, components, patterns) and apply it to all MVP screens in high fidelity. This is the longest-running design artefact and the direct input to engineering.

### Why it matters
The design system is where brand, IA, and engineering converge. Get it right and the product is coherent, fast to build, and easy to evolve. Get it wrong and every screen becomes a one-off negotiation, consistency breaks down, and engineering ships inconsistent components.

### Deliverables
1. Design tokens implemented from Agent 5's JSON (colour, type, spacing, radius, shadow, motion)
2. Component library (minimum set for MVP)
3. Pattern documentation (empty states, loading, error, pending, "what's missing")
4. High-fidelity screens for all MVP flows (desktop and mobile)
5. Accessibility audit against WCAG 2.2 AA
6. Figma library maintained as canonical source
7. Handoff package for engineering (specs, assets, tokens, Storybook-ready structure)

### Inputs you provide
- Agent 5 (brand tokens, logo, imagery)
- Agent 6 (wireframes, flows, tested prototype)
- Agent 2 (state machine, edge cases)
- Agent 8 (microcopy for every screen)

### Expected outputs
- `01-design-tokens/` (implementation-ready, mirrors Agent 5 tokens)
- `02-component-library/` (Figma source + documentation)
- `03-patterns.md` (how to handle recurring UX scenarios)
- `04-screens/` (high-fi screens for all MVP flows, desktop + mobile)
- `05-accessibility-audit.md`
- `06-engineering-handoff.md`

### Minimum component set for MVP
Button, Input, Select, Checkbox, Radio, Toggle, Textarea, Date picker, Time window picker, Card, List item, Table row, Badge (trust, status, role), Pill, Avatar, Tag, Modal, Drawer, Toast, Banner, Empty state, Skeleton, Spinner, Error state, Tooltip, Popover, Tabs, Breadcrumb, Pagination, Filter chip, Stepper, Form group, Fixture card, Request card, Availability card, Trust badge, "What's missing" panel, Navigation (primary, secondary, mobile).

### Patterns to document
- Empty states (every list / search result)
- Loading states (skeleton vs spinner rules)
- Error handling (inline, toast, page-level)
- Pending states (awaiting response, awaiting confirmation)
- "What's missing" indicator pattern
- Notification presentation (in-app, badge counts)
- Confirmation and destructive actions
- Form validation (when, how, tone)
- Trust badge presentation
- Status pill system

### Timing
Weeks 6–16. Parallel with build. Component library starts first; screens fill in as Agent 6 wireframes stabilise.

### Handoff criteria
- All MVP screens complete in desktop and mobile
- Every component in library has variants, states, and docs
- WCAG 2.2 AA audit passed
- Tokens consumable by engineering's CSS/Tailwind setup
- Figma library versioned

### Common failure modes
- Building components the product doesn't need
- Building screens before components are stable (infinite rework)
- Inconsistent badge treatments (trust, status, role) — they need hierarchy
- Missing empty states
- Dense dashboards that ignore the tone ("calm, quiet")
- Typography scales with too many sizes
- Not testing against target demographic (contrast, text size)
- Producing designs that can't be implemented in reasonable time
