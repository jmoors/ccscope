# 07 — Usability Test Plan

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft — hypotheses written before testing begins

---

## 1. Testing principles

Per `CLAUDE.md`:
- Test hypotheses, not opinions. Hypotheses are written below before any testing happens.
- The empty state is the most important screen to test.
- Watch actual behaviour. Don't rely on what users say they'd do.
- Include 50+ fixture secretaries. Not just tech-comfortable users.
- Minimum 5 participants per key segment.

---

## 2. Participant segments

| Segment | Who | Min. participants | Recruitment source |
|---|---|---|---|
| A — Experienced fixture secretaries (50–70s) | Fixture secretaries who arrange 10+ fixtures per season. Moderate-to-low digital confidence. | 15 | Surrey CC league secretaries, SCB introductions |
| B — Younger fixture managers / captains (20s–30s) | Captains who also manage fixtures. High digital confidence. Smartphone-first. | 10 | Direct club outreach in Surrey |
| C — New clubs (first season of league cricket) | Recently registered clubs with no established fixture network. | 8 | SCB new club registration list |
| D — Multi-team administrators | Club secretaries managing 2+ teams simultaneously. | 7 | Surrey league secretary network |
| E — Service providers (umpires) | ACUS Surrey branch members; experienced umpires aged 50+ | 5 | ACUS Surrey branch introduction |
| F — Women's club fixture managers | Women's team FMs; may have different fixture culture and network challenges. | 5 | Surrey women's cricket coordinator |

**Total minimum: 50 participants**

---

## 3. Session format

**Format:** 1:1 moderated usability test. Think-aloud protocol.  
**Length:** 60 minutes per session.  
**Location:** In-person preferred for Segments A and E (lower digital confidence; in-person allows behavioural observation). Remote (video call, screen share) acceptable for Segments B and C.  
**Prototype:** Clickable prototype built from wireframes (Figma or equivalent). Not a live system.

**Moderator rule:** Do not correct or help the participant. Observe and note. Ask "What would you do next?" not "Did you see the button?"

---

## 4. Test scenarios

Each participant completes up to 4 scenarios. The scenarios are selected per segment based on relevance.

### Scenario 1 — Find a game (primary flow)

"It's mid-April. You're filling your June fixtures. You have a Sunday T20 slot that needs an opponent. Use this platform to find one."

**Relevant segments:** A, B, C, D  
**Prototype state:** Search form → results (4 teams available) → availability detail → send match request form

---

### Scenario 2 — Empty search result → post availability

"You've searched for opponents for the same June date. The search returns nothing. What do you do?"

**Relevant segments:** A, B, C  
**Prototype state:** Search form → empty results → post availability form (pre-filled)

**This is the most important scenario.** The empty state must be tested independently, not as a follow-on from Scenario 1. Participants must feel the empty state as a primary experience, not as a fallback.

---

### Scenario 3 — Receive and act on a match request

"You've posted your availability. You've just received a match request. It's from a club you don't know. What do you do?"

**Relevant segments:** A, B, D  
**Prototype state:** Email notification (shown on screen) → request detail → accept flow → fixture detail (awaiting venue) → confirm venue

---

### Scenario 4 — Cancel a fixture (short notice)

"It's 10pm Friday. Your game is tomorrow. You can't field a team. You need to cancel."

**Relevant segments:** A, B (no Segment C — new clubs may not have confirmed fixtures yet)  
**Prototype state:** Dashboard → fixture detail → cancel flow → warning screen

---

### Scenario 5 — Umpire: receive and respond to a support request

"You're an umpire at Westfield CC. You've received an email asking you to umpire a T20 on Sunday. What do you do?"

**Relevant segments:** E only  
**Prototype state:** Email shown on screen → email accept link → confirmation page  
**Note:** This scenario starts outside the platform (with an email). Bernard-type users must be able to accept without creating a platform account.

---

### Scenario 6 — Club Admin: onboard your club

"Your club has just been invited to join the platform. You're the club secretary. Set up your club and invite your first fixture manager."

**Relevant segments:** A (club secretaries), D  
**Prototype state:** Onboarding flow: 3 steps

---

## 5. Hypotheses (written before testing — these can be falsified)

### H1 — Empty state (primary hypothesis)

> **If** the empty search results page provides a clear pivot to "Post availability" with the form pre-filled,  
> **Then** at least 4 of 5 participants (80%) in Segments A and C will proceed to post availability without help from the moderator.

**Pass criteria:** Participant navigates from empty results → Post Availability form without moderator intervention.  
**Fail criteria:** Participant expresses confusion, gives up, or asks "What do I do now?"

**Why this matters:** This is the core empty-state risk. If participants abandon at the empty state, the product fails the search-first assumption.

---

### H2 — Trust badge comprehension

> **If** the trust badge (New / Reliable / Established) is shown as a text label with a simple indicator,  
> **Then** at least 4 of 5 participants will correctly explain what each badge means without reading a tooltip or help text.

**Pass criteria:** When asked "What does this symbol mean?" participant gives a broadly correct interpretation without assistance.  
**Fail criteria:** Participant cannot describe what the badge means, or mistakes it for a star rating.

---

### H3 — "What's missing" panel clarity

> **If** the "What's missing" panel lists outstanding items with inline action links,  
> **Then** at least 4 of 5 participants will locate the next required action within 30 seconds without moderator help.

**Pass criteria:** Participant finds the "Confirm venue" action within 30 seconds on the fixture detail page.  
**Fail criteria:** Participant looks in navigation, help, or expresses "I don't know what to do next."

---

### H4 — Short-notice cancellation warning comprehension

> **If** the warning screen explains the trust record implication of a short-notice cancellation,  
> **Then** at least 4 of 5 participants will understand that: (a) the note is not public, and (b) repeated cancellations have a consequence.

**Pass criteria:** When asked "What will happen?" participant correctly describes the consequence as private and explains they understand it affects their record.  
**Fail criteria:** Participant thinks the note is public, or does not understand there is any consequence.

---

### H5 — Older segment (50–70s): search form usability

> **If** the search form uses familiar date pickers and dropdown selectors,  
> **Then** at least 4 of 5 Segment A participants will complete a search without error on the first attempt.

**Pass criteria:** Participant fills in all required fields and submits the search successfully on first attempt.  
**Fail criteria:** Participant cannot complete the form, enters wrong data type, or requires moderator help.

---

### H6 — Umpire email-only flow (Bernard)

> **If** the umpire support request can be accepted via a link in an email without requiring platform login,  
> **Then** all 5 Segment E participants will be able to accept the request from the email alone.

**Pass criteria:** Participant clicks email link, reads confirmation page, understands they've accepted.  
**Fail criteria:** Participant is confused by the confirmation page, or doesn't understand they've accepted without logging in.

---

### H7 — Multi-team context switching

> **If** the team context picker is persistent and visible at the top of the page,  
> **Then** at least 4 of 5 Segment D participants will correctly identify which team they are acting for when switching teams.

**Pass criteria:** When asked "Which team are you acting for right now?" participant answers correctly.  
**Fail criteria:** Participant is uncertain which team's data they're looking at, or makes an action on the wrong team.

---

### H8 — New club empty dashboard

> **If** the empty dashboard includes a contextual 4-step explanation and two clear CTAs,  
> **Then** at least 4 of 5 Segment C participants will take an action (find a game or post availability) within 2 minutes of landing on the empty dashboard.

**Pass criteria:** Participant initiates one of the two primary flows within 2 minutes without moderator help.  
**Fail criteria:** Participant reads the screen and does nothing, or asks "Is the platform working?"

---

## 6. Measures

| Measure | Method |
|---|---|
| Task completion rate | Pass / fail per scenario, per participant |
| Time on task | Stopwatch from scenario prompt to task completion |
| Error rate | Count of wrong paths, failed submissions, or recoveries required |
| Comprehension questions | Asked after each scenario: "What did that do?" / "What happens next?" |
| Emotional response | Noted from think-aloud and facial expression (in-person) |
| Verbatim quotes | Captured in real time; attributed to segment (not individual) |

---

## 7. Recruiting specification

**Screening criteria (all participants):**
- Currently active as a fixture manager, club secretary, captain, or umpire at an amateur cricket club in Surrey or within 30 miles of Surrey
- Has arranged at least one friendly fixture in the last 2 seasons
- Not a software developer or UX designer (avoid digital professional bias)

**Segment A specific:**
- Aged 50–70
- Does not describe themselves as "very comfortable with technology"
- Has used email but not necessarily a dedicated fixture management platform

**Segment E specific:**
- Registered umpire on at least one club's roster
- Aged 50+ preferred (this is the primary Bernard demographic)

**Incentive:** £30 Amazon voucher or donation to club cricket charity in participant's name. Either option offered at the start of the session.

---

## 8. Pre-test checklist

- [ ] Prototype is fully clickable for all 6 scenarios
- [ ] Prototype includes empty state, populated state, error states for each screen
- [ ] All real copy used — no lorem ipsum
- [ ] Moderator guide written per scenario (this document)
- [ ] Consent forms drafted (UK GDPR compliant)
- [ ] Recording consent obtained (screen + audio, no video required for remote)
- [ ] Participant screener questionnaire drafted and approved
- [ ] Recruiting started — minimum 8-week runway before testing begins
- [ ] Segment A and E participants confirmed at in-person venues (at least 2 locations: north and south Surrey)
- [ ] Analysis framework agreed (not just "thematic analysis" — specific pass/fail per hypothesis)

---

## 9. Analysis protocol

After testing:

1. **Score each hypothesis H1–H8:** Pass / Fail / Partial
2. **Tally task completion rates** per segment
3. **Tag verbatim quotes** to hypothesis and screen
4. **Surface the top 3 unexpected findings** — things not covered by a hypothesis
5. **Map findings to wireframe revisions** — one specific change per finding where possible
6. **Document null results** — where hypotheses held and no change is needed

**Escalation criteria:**
- If H1 fails (empty state): escalate to Agent 1 immediately. The search-first principle may need reconsideration.
- If H5 fails on 3+ Segment A participants: escalate to Agent 7 for accessibility review before build.
- If H6 fails: escalate to Agent 9 — the email-only flow for service providers may not be technically achievable without redesign.

---

## 10. Usability results location

Results are documented in `09-usability-results.md` after testing. This document (test plan) is preserved unchanged alongside results to demonstrate hypothesis-first discipline.

Revisions to wireframes based on testing findings are versioned in this folder with a `v2` suffix on affected files.
