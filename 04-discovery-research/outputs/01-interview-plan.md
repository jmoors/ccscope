# 01 — Interview Plan

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 4 (Discovery & Research)
**Status:** Active — to be run weeks 1–8

---

## Purpose

This document governs all research activity for Agent 4. It defines what assumptions we are testing, who we are talking to, how we recruit, and how we conduct each interview. It is the reference document for every interviewer and for the synthesis process.

The core question is not "do people like this idea?" It is: **do the specific product assumptions hold under contact with real users?**

---

## Assumptions Under Test

The following assumptions are drawn from Agent 1 (Product Foundations), Agent 2 (Domain Model & Logic), and the shared project context. Each assumption is marked with a priority level.

### P0 — Critical (invalidation stops or redirects the build)

| ID | Assumption | Source |
|---|---|---|
| A01 | Fixture managers currently find opponents via informal channels (WhatsApp, Facebook, personal networks) and find this genuinely frustrating | Project context |
| A02 | There is a real problem of unreliable clubs (no-shows, short-notice cancellations) that causes measurable pain | Project context |
| A03 | Fixture managers would search for existing availability before posting their own — the "search-first" behaviour is natural, not forced | Product principle 1 |
| A04 | A structured match request (vs. a direct WhatsApp message) is acceptable and does not feel cold or impersonal | Core fixture flow |
| A05 | Fixture managers are willing to submit a short post-match review (3 questions) at a meaningful rate | Trust system |

### P1 — High (invalidation requires scope or design adjustment)

| ID | Assumption | Source |
|---|---|---|
| A06 | The three review dimensions (reliability, preparedness, recommendation) map accurately to how FMs think about a good or bad experience | Trust algorithm |
| A07 | A 7-day review window is long enough for FMs to complete it without feeling rushed | Trust algorithm |
| A08 | Badge language (New / Reliable / Established) is legible and trusted — FMs understand what these mean without explanation | Glossary |
| A09 | Distance is the dominant practical constraint when choosing an opponent (weighted 0.25 in algorithm) | Matching algorithm |
| A10 | Tier / ability matching matters enough to influence choice (weighted 0.20) | Matching algorithm |
| A11 | FMs want to find an opponent from within the platform before receiving unsolicited match requests from others | Search-first principle |
| A12 | The 48-hour threshold for "short-notice cancellation" is appropriate — FMs consider cancellations inside 48 hours to be the meaningful category | Trust algorithm |
| A13 | Club-level trust (not team-level) is the right unit — FMs judge clubs, not individual teams within a club | Trust system |

### P2 — Medium (invalidation refines implementation but does not change direction)

| ID | Assumption | Source |
|---|---|---|
| A14 | FMs are the correct primary user — club administrators are secondary | Positioning |
| A15 | Fixture managers are time-poor and will not tolerate feature discovery or setup friction | Positioning |
| A16 | Email + in-app notifications are sufficient; no SMS or WhatsApp integration is needed for MVP | Notification scope |
| A17 | A 50-mile default search radius is appropriate for most clubs | Matching algorithm |
| A18 | FMs access administrative functions on desktop evenings; match-day actions happen on phones | Audience realities |
| A19 | The request expiry of 7 days is an acceptable wait time before a request is treated as unanswered | Match request flow |
| A20 | The "What's missing" panel approach (showing gaps in a fixture) maps to how FMs mentally track fixture progress | Fixture detail view |

---

## Participant Targets

| Group | Target | Minimum for synthesis |
|---|---|---|
| Fixture managers / team secretaries | 20 | 15 |
| League administrators | 5 | 3 |
| Umpires (club-registered) | 5 | 3 |

### Fixture manager selection criteria

**Must include:**
- At least 5 who currently use Play-Cricket actively and are broadly satisfied with it (avoids over-sampling dissatisfied users)
- At least 3 who are 55+ in age (to represent the older end of the demographic)
- At least 3 who manage Sunday XI or social cricket teams (different dynamics from competitive league cricket)
- At least 2 women's / mixed cricket fixture managers
- At least 2 managers from clubs that joined their league in the last 3 seasons (new entrant perspective)
- At least 1 from a club that has experienced a significant no-show or late cancellation from an opponent

**Must not be:**
- All from the same county or league
- All from clubs that have expressed frustration with current tools (survivorship / enthusiasm bias)
- Personal contacts of the product team (social desirability bias)

### League administrator selection criteria

- At least 2 who manage a senior recreational league (not elite)
- At least 1 who administers Play-Cricket for their league
- At least 1 sceptic — someone who has concerns about fragmentation of cricket admin tooling

### Umpire selection criteria

- Registered with a county umpires association OR on a club's internal umpire roster
- Mix of regularly active and occasionally active

---

## Recruitment Channels

In priority order:

1. **County Cricket Boards (CCBs)** — direct approach via club development officers. Ask for introductions to fixture secretaries, not self-selecting volunteers.
2. **League secretaries** — ask to share recruitment notice via their own communication channels; league secretary then forwards, avoiding direct cold-contact of members.
3. **ECB recreational cricket network** — clubs registered with Play-Cricket and active in the last season.
4. **Cricket club social media** — post in club-run Facebook Groups and X accounts, not generic cricket communities (reduces selection bias toward tech-early-adopters).
5. **Club websites** — direct email to "fixtures" or "secretary" contact addresses where publicly listed.

**Do not use:**
- Cricket Twitter/X general community (skews toward engaged enthusiasts)
- Reddit r/Cricket (heavily skewed toward spectators, not administrators)
- Paid panel services (no cricket-specific panels exist; general panels produce low-quality respondents)

### Recruitment message (template — to be adapted per channel)

> We're a small team researching how amateur cricket clubs organise friendly fixtures. We want to understand how it works today — what goes well, what's painful, and what you've tried. We're not selling anything. This is a 45-minute conversation, conducted via video call, and entirely confidential. If you arrange fixtures for your club and would be willing to have a conversation, we'd be glad to hear from you.
>
> [contact email]

Note: do not mention the platform concept in recruitment. We want to understand current behaviour, not filter for people who are already interested in a solution.

---

## Consent and GDPR

### Before the interview

All participants must receive and confirm:

1. **Participant information sheet** explaining: who we are, what the research is for, how data is stored, how long it is kept, their right to withdraw at any time, and that their name will never appear in any output.
2. **Verbal confirmation at the start of the call** that they have read the information sheet and consent to the conversation being recorded for note-taking purposes only.
3. **Explicit consent for recording** — if they decline recording, proceed with written notes only. Do not record without explicit consent.

### Data handling

- Recordings stored in encrypted cloud storage, access restricted to research team only.
- Recordings deleted within 30 days of synthesis being completed.
- Raw notes anonymised before any sharing (replace names, club names, locations with coded identifiers: FM-01, FM-02 etc).
- No individual quote is attributed to a named person or identifiable club in any output.
- Consent records retained as required by GDPR for the duration of the project.

If these conditions cannot be met, interviews do not proceed.

---

## Interview Guides

Three separate guides: fixture manager (primary), league administrator, umpire.

Each guide follows the same structure:
1. Warm-up — establish rapport, confirm role
2. Current state — understand actual workflows (last-specific-instance questions first)
3. Pain and workarounds — what breaks, what they've built around it
4. Reactions — brief concept exposure at the end only
5. Wrap-up — anything they want to add; referrals

**Rule: never ask hypothetical preference questions before you understand actual behaviour.** "Would you use X?" is nearly worthless. "Walk me through the last time you did Y" is gold.

---

### Guide A — Fixture Manager

**Duration:** 40–50 minutes
**Format:** Video call (Zoom / Google Meet — participant's choice)
**Recording:** With consent; notes taken regardless

#### 1. Warm-up (5 min)

- Tell me a bit about your club — what format do you mainly play?
- How long have you been sorting fixtures for the club?
- Roughly how many games do you arrange in a season?

*Goal: calibrate club size, format mix, FM experience level. Do not prompt or suggest answers.*

#### 2. Current workflow — finding opponents (15 min)

Start here, always. This is the most important section.

- Walk me through how you find a game when you have a gap in the fixture list. Take me back to the last time you had to find someone at relatively short notice — what did you actually do?
- Who do you contact first? Why them?
- What happens when that doesn't work?
- How long does it typically take from "we need a game" to "fixture confirmed"?
- How do you keep track of who you've approached and where things stand?
- Is there a time of season when this is harder? Why?

*Probe on: tools used (WhatsApp groups, Facebook, email, Play-Cricket, spreadsheets), who holds the contacts, what happens when the usual contacts can't help.*

*Watch for: mentions of existing tools (note the exact tool and context); signals of workarounds they've built; differences between early-season and last-minute gaps.*

#### 3. Current workflow — filling gaps (venue, officials) (5 min)

- When you've confirmed an opponent but still need a venue or an umpire, how do you handle that?
- Is finding officials harder or easier than finding an opponent?
- What's your club's umpire situation — do you have a roster?

*Note: this section feeds the "find support" scope. Don't overweight it — it's secondary to finding an opponent.*

#### 4. Reliability and trust (10 min)

This is where we test A02, A05, A06, A12.

- Has a game ever fallen through late — opposition didn't show up or cancelled at the last minute? What happened?
- How did that affect how you thought about arranging games with that club in future?
- When you're deciding whether to agree to a game with a club you haven't played before, what do you go on?
- If you played a game that went badly — the other club showed up late, were badly organised — would you tell anyone about it? Who? How?
- Has another club ever warned you off playing someone? How did that work?

*Probe on: informal reputation networks, word-of-mouth, whether people would be willing to formally review after a game, and under what conditions.*

*Watch for: unprompted mentions of cancellations and their emotional weight; whether reputation flows through personal networks or is more widely known.*

#### 5. Play-Cricket and existing tools (5 min)

- Do you use Play-Cricket? What for?
- What does it do well for you?
- What do you end up going around it for?

*Important: do not lead. Do not mention problems we think Play-Cricket has. Let the FM tell you what their experience is.*

*This section is critical for understanding co-existence. We must understand how FMs think about adding a new tool to their stack.*

#### 6. Concept exposure (5 min)

Only after sections 2–5 are complete. Brief, neutral description only.

Read this (do not improvise):

> "We're thinking about a tool specifically for friendly fixture coordination — where you can search to see if other clubs near you have posted that they're available on a given date, and then send a structured match request through the platform. After the game, both clubs would answer three short questions about how it went — nothing public, just private feedback that affects how clubs appear in future searches."

Then ask:
- Does any part of that resonate with what you've described today?
- Is there anything that sounds off or that you can see not working for your situation?
- The trust / review piece — what's your instinct on that?

*Do not defend the concept. If they're sceptical, probe: "What specifically makes you doubtful?" Note sceptics carefully — they are more valuable than enthusiasts.*

#### 7. Wrap-up (2 min)

- Is there anything I haven't asked about that you think is important?
- Do you know anyone else I should talk to — particularly people who have a very different experience from yours?

---

### Guide B — League Administrator

**Duration:** 35–45 minutes

#### 1. Warm-up (5 min)

- Tell me about the league you administer — geography, format, how many clubs?
- How long have you been in this role?
- What does a typical pre-season look like for you administratively?

#### 2. Fixture scheduling and current tools (15 min)

- How are league fixtures generated — central fixture computer, manual, hybrid?
- How do clubs typically arrange their friendlies and rearranged fixtures, in your experience?
- Do clubs coordinate with you when arranging friendlies, or is that entirely separate?
- What's your relationship with Play-Cricket for this league?

#### 3. Problem patterns (10 min)

- What are the most common fixture-related problems you deal with in a season?
- Which clubs in your league tend to be reliable, and how do you know?
- If a club gets a reputation for being difficult to deal with — cancellations, no-shows — how does that information travel?
- Do clubs in your league ever ask you to recommend opponents for friendlies?

#### 4. Concept exposure and partnership framing (10 min)

Same brief description as Guide A, then:
- From a league administrator's perspective, does a tool like this create any complications for you?
- Would you have any interest in recommending it to clubs in your league, or is that not a role you'd play?
- Is there anyone at county board level we should be talking to?

#### 5. Wrap-up (2 min)

- Referrals: are there other league administrators or county officials we should speak to?

---

### Guide C — Umpire

**Duration:** 30–35 minutes

#### 1. Warm-up (5 min)

- Tell me how you got into umpiring — how long have you been doing it?
- Are you registered with a county association, or do you mainly umpire for your own club or local network?
- Roughly how many games do you umpire in a season?

#### 2. Current workflow — getting booked (10 min)

- How do clubs find you when they need an umpire?
- Who contacts you, and how — phone, email, WhatsApp?
- How far in advance are you typically contacted?
- Have you ever been short-noticed — contacted the day before or the morning of?

#### 3. Pain and gaps (10 min)

- Are there times you're not available when clubs need you, and no alternative is obvious?
- Are there clubs you prefer to umpire for, and clubs you avoid? Why?
- Has a fixture ever fallen through because the club couldn't find an umpire?

#### 4. Concept exposure (5 min)

> "We're looking at building a simple way for clubs to request an umpire from a pool of officials connected to their club — nothing like a public marketplace, just a structured way to send a request to umpires in your existing network."

- Does that change anything about how you currently handle requests?
- What would you need to know before accepting a request through a system like that?

#### 5. Wrap-up (3 min)

- Referrals to other umpires, especially those with different experience levels or county associations.

---

## Bias Mitigation Procedures

**Before each interview:**
- Review the participant profile. If you have a personal connection, flag and reassign.
- Re-read the relevant guide. Do not improvise question order unless the conversation demands it.

**During each interview:**
- Last-specific-instance questions before any general-preference questions.
- Never confirm or validate what a participant says with "exactly" or "yes, we think that too."
- If a participant asks what you think, redirect: "I'm more interested in your experience — we're early enough that we don't have strong views yet."
- Do not explain the concept before section 6. If participants ask earlier what the platform would do, defer: "I'll explain what we're working on at the end — first I want to understand how things work for you today."

**After each interview:**
- Write up notes within 24 hours while memory is fresh.
- Separate observation (what they said) from interpretation (what it means) in notes.
- Flag any assumption that took a hit, however small. Don't wait for synthesis.

---

## Analysis Framework

### After each interview

Immediately after note-writing, complete this short template:

```
INTERVIEW [ID] — QUICK IMPRESSIONS
Participant type: FM / League Admin / Umpire
Assumptions supported: [list IDs, e.g. A01, A03]
Assumptions challenged: [list IDs with brief note]
Surprising / unexpected: [anything not anticipated]
Quotes worth preserving (anonymised): [max 3]
Flags for Agent 2 or Agent 1: [any breaking finding]
```

### Mid-research synthesis (at 8 interviews)

Before completing all 15+ FM interviews, produce a provisional synthesis against each P0 and P1 assumption. This triggers any escalation needed before build begins. Feed to Agents 1 and 2.

### Final synthesis

Produce `02-fixture-manager-interviews-synthesis.md` covering:
- Full assumption validation table (supported / partially supported / challenged / invalidated)
- Workflow documentation: what current fixture coordination actually looks like
- Patterns across participants, with illustrative (anonymised) quotes
- Disconfirming evidence — explicitly surfaced, not buried
- Recommended adjustments to product, algorithm, or scope

---

## Escalation Protocol

The following trigger an immediate write-up and message to the relevant agent — do not wait for synthesis:

| Trigger | Action |
|---|---|
| A P0 assumption invalidated by 3 or more participants | Flag to Agent 1 (scope decision) and Agent 2 (model adjustment) |
| A P1 assumption invalidated by 3 or more participants | Flag to Agent 2 for model adjustment |
| Participant reveals a tool or workflow we were not aware of | Log immediately; assess impact on competitive positioning |
| Partnership opportunity identified | Log in `08-partnership-leads.md`; flag to Agent 10 if scope change implied |
| Unable to recruit representative sample after 2 weeks | Escalate to Agent 1 |

---

## Schedule

| Week | Activity |
|---|---|
| 1 | Finalise guides, consent documentation, recruitment outreach begins |
| 2–3 | First FM interviews (target: 6) |
| 4 | Mid-research review: provisional assumption validation; feed to Agents 1 & 2 |
| 5–6 | Remaining FM interviews (target: 9+); league admin and umpire interviews begin |
| 7 | Complete all interviews; begin synthesis |
| 8 | Deliver all synthesis documents; seed geography recommendation; partnership leads warm |

---

## Document Dependencies

| This document informs | When |
|---|---|
| `02-fixture-manager-interviews-synthesis.md` | After 15+ interviews |
| `03-league-admin-interviews-synthesis.md` | After 3+ league admin interviews |
| `04-umpire-interviews-synthesis.md` | After 3+ umpire interviews |
| `05-current-workflow.md` | Mid-research (week 4 draft, week 8 final) |
| `06-assumption-validation.md` | Week 8 |
| `07-seed-geography-recommendation.md` | Week 8 |
| `08-partnership-leads.md` | Rolling updates from week 2 |
| `09-ongoing-research-plan.md` | Week 8 |

Findings that invalidate assumptions feed back to:
- Agent 2 (`02-domain-model/`) for algorithm or model adjustments
- Agent 1 (`01-product-foundations/`) via `shared/DECISION_LOG.md` for scope decisions

---

*No individual will be identified in any output derived from this research. All quotes are anonymised before any internal sharing.*
