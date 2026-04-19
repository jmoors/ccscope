# 03 — Journey Maps

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft

---

## How to read these maps

Each map covers: **Persona → Context → Steps → Emotional arc → Design implications**.

Emotional arc uses: ▼ Frustration / ○ Neutral / △ Relief / ▲ Satisfaction

These are hypotheses about emotional states. They are testable. The usability test plan (`08-usability-test-plan.md`) documents hypotheses before testing.

---

## Map 01 — Fixture Manager: Successful search, match found, fixture confirmed

**Persona:** Graham, 54, 2nd XI captain & fixture secretary, plays T20 and 40-over. Does admin on laptop Sunday evenings.

**Context:** It's mid-April. Graham needs to fill a Friday evening T20 in June. His usual contacts haven't replied on WhatsApp yet.

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Arrives at platform | Logs in to familiar dashboard | Upcoming fixtures, one published availability from last week | ○ Comfortable |
| 2 | Initiates search | Clicks "Find a game." Selects 13 June, T20, home, within 20 miles | Search form with familiar fields | ○ Routine |
| 3 | Sees results | Search returns 4 teams | Four availability cards: club name, distance, format, trust badge | △ Mild optimism — better than the WhatsApp group |
| 4 | Reviews a candidate | Clicks Thornton CC 2nd XI (8 miles, Reliable badge) | Team detail: T20, open age group, home ground confirmed, 3 compatible formats | ▲ Recognition — knows Thornton, they're good |
| 5 | Sends match request | Clicks "Send match request." Adds a brief note. Confirms. | Confirmation: "Match request sent to Thornton CC 2nd XI." | ▲ Satisfaction — action taken, back to the sofa |
| 6 | Waiting | Checks dashboard two days later | "Awaiting response — Thornton CC 2nd XI (sent 2 days ago)" | ○ Patient |
| 7 | Gets notification | Receives email: "Thornton CC 2nd XI have accepted your match request" | Email with link to fixture detail | △ Relief |
| 8 | Views confirmed fixture | Clicks through to fixture detail | Status: Confirmed. Both teams, home ground venue confirmed, no officials needed (friendly). | ▲ Job done |

**Emotional arc summary:** Calm → Routine → Mild optimism → Recognition → Satisfaction → Patience → Relief → Done

**Design implications:**
- Trust badge on search results is doing real work here. Graham recognised Thornton and felt confident. Badge must be visible and legible at result-card size.
- The "familiar" feel on dashboard and search form is important. This is not a high-excitement product. Graham doesn't want to be impressed; he wants it to work.
- Waiting state (step 6) must be visible on dashboard without the user having to dig for it. "Awaiting response" as a distinct fixture status card is important.

---

## Map 02 — Fixture Manager: Search returns empty (most important journey)

**Persona:** Graham (same as above). Different context.

**Context:** March. Pre-season. He's trying to fill several dates. Searches for a Sunday fixture in late May. Platform is thin on availability (early adopter phase, Surrey seed geography, low density).

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Searches | Date, Sunday format, 25-mile radius | Loading indicator | ○ |
| 2 | Gets empty results | Waits 2 seconds | "No availability found for Sunday 31 May within 25 miles. Try widening your search." | ▼ Familiar frustration — this happens on Facebook groups too |
| 3 | Tries wider radius | Adjusts to 40 miles. Re-runs. | Still no results. | ▼ Slight dip. "Is this platform even used?" |
| 4 | Prompted to post availability | Sees clear call to action: "Post your availability — let other teams come to you." Form is pre-filled with his search parameters. | Pre-filled form: 31 May, Sunday, away preference. | ○ Shift in expectation — not "search failed" but "now I'm visible" |
| 5 | Posts availability | Reviews pre-filled form. Adds a date window (31 May or 7 June). Submits. | Confirmation: "Your availability is published. Teams searching for a Sunday XI will find you." | △ Small satisfaction — has done something useful |
| 6 | Gets notified (days later) | Receives email: "Redfield CC Sunday XI has sent you a match request." | Email with link to request detail | ▲ Happy surprise — it worked |

**Emotional arc summary:** Neutral → Frustration → Slight dip → Shift → Small satisfaction → Happy surprise

**Design implications:**
- **Empty state is the most important screen in the product.** It must not feel like a failure message. It must feel like a transition from "search mode" to "post mode."
- The empty state must not use language like "No results" or "Nothing here." The copy is critical — Agent 8 should treat this as a priority.
- Pre-filling the Post Availability form from search parameters is essential. Graham should not have to re-enter what he just searched for. This reduces friction at the most vulnerable moment in the flow.
- The confirmation message (step 5) must communicate the mechanism: "Teams will find you." Not just a generic "Success."

---

## Map 03 — Fixture Manager: Receives and accepts a match request

**Persona:** Priya, 38, fixture secretary for a women's T20 team. Works during lunch breaks on her phone.

**Context:** A Thursday lunchtime in May. Priya has published availability for the first Sunday of June. She gets a notification while eating lunch.

| # | Step | What she does | What she sees | Emotional arc |
|---|---|---|---|---|
| 1 | Receives notification | Phone buzzes. Opens email. | "Westfield Ladies CC have sent you a match request for Sunday 7 June." Link to request. | △ Mild excitement |
| 2 | Clicks through on phone | Taps link. Lands on match request detail. | Request detail: Westfield Ladies CC (T20, Women's, open, 12 miles away, New badge), date, note from their FM: "Would love a game, we're a similar level." | ○ Sizing them up — New badge, but the note is reassuring |
| 3 | Checks her team's calendar | Switches to another app briefly to check WhatsApp / email for any conflicts | — | ○ Standard admin |
| 4 | Returns to platform | Comes back to request detail | Same view | ○ |
| 5 | Accepts | Taps "Accept." Sees confirmation dialog. Confirms. | "Match confirmed with Westfield Ladies CC — Sunday 7 June. Fixture created." | ▲ Clean satisfaction |
| 6 | Views fixture | Taps "View fixture." | Fixture detail: "Awaiting venue — both teams to confirm playing venue." What's missing panel shows: venue. | ○ One more thing to do — expected |
| 7 | Confirms her home ground | Taps "Confirm venue." Selects club's home ground from saved list. Confirms. | Fixture updates: "Confirmed — Sunday 7 June, Priya's club home ground." | ▲ Done |

**Emotional arc summary:** Mild excitement → Sizing up → Routine → Return → Satisfaction → Expected → Done

**Design implications:**
- Phone-first flow. The accept/confirm actions must be completable on a 375px viewport without pinching or horizontal scrolling.
- The "New badge" creates mild uncertainty. The note from the requesting FM (the optional 200-char note) is doing important trust-building work in this scenario. The note field should be visible and prominent on the request detail, not tucked below the fold.
- "What's missing" panel must be scannable at a glance. Priya is on a 20-minute lunch break; she doesn't have time to read a full fixture summary to understand what's left to do.
- Venue confirmation from a saved list (not re-entering an address) is essential for repeat users. Pre-saved club venues must be the default.

---

## Map 04 — Fixture Manager: Declines a match request

**Persona:** Graham (same as Map 01).

**Context:** Graham posted availability for a date in July. He receives a request from a club he's played against and had a poor experience with (they cancelled short notice last season). He's not sure they're in the platform's trust system yet, or whether it will show.

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Receives request | Email notification. | "Crestview CC have sent you a match request for Sunday 20 July." | ○ Cautious |
| 2 | Views request detail | Opens request on laptop. | Crestview CC: T20, Men's, Open. Trust badge: New (they joined the platform this year). | ▼ Disappointed — badge doesn't show their history. He knows they've been unreliable. |
| 3 | Declines | Clicks "Decline." Sees confirmation. | "Match request declined. Crestview CC will be notified. Your availability remains open." | ○ Fine |
| 4 | Returns to availability | Back to "My availability." | Date still showing as "Awaiting opponent." | ○ Still visible; can receive another request |

**Emotional arc summary:** Cautious → Disappointed → Fine → Neutral

**Design implications:**
- The "New" badge is honest: Crestview genuinely is new to the platform. But it leaves Graham with no recourse for off-platform history. This is a known limitation and must not be papered over.
- The decline action must not require a reason. This is intentional (it's low friction, like declining a calendar invite). No mandatory reason field.
- After declining, the user must be reassured that their availability is still live. This is important for trust in the system: "I declined; am I now invisible?" The answer is no, and the UI must make that clear.
- **Implication for trust design:** Graham represents a segment who will adopt the platform's trust system once Crestview has enough history. The patient path (New → Reliable) must feel coherent to experienced fixture managers who already have mental models of club reliability.

---

## Map 05 — Fixture Manager: Cancels a fixture (short notice)

**Persona:** Marcus, 29, 1st XI captain, also manages fixtures. Fit and active user. Gets a call Friday evening.

**Context:** Friday, 18:00. The game is tomorrow at 14:00. Marcus's opening batsman has broken his foot. They're down to 8 players and can't field a proper side. He has to cancel.

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Opens platform | Finds fixture on dashboard. | Confirmed fixture: Saturday, 14:00 vs Thornton CC. | ▼ Already stressed |
| 2 | Initiates cancellation | Taps "Cancel fixture." | Warning: "This fixture is in less than 24 hours. Cancellations with less than 48 hours notice affect your trust record." | ▼ Sees the penalty — feels bad, but accepts it's fair |
| 3 | Confirms (not weather) | Confirms cancellation. Sees reason dropdown: "Unable to field a team" selected. | Confirmation: "Fixture cancelled. Thornton CC have been notified. A note has been made on your record." | ○ Resigned acceptance |
| 4 | Feels the sting | Views dashboard | Short-notice cancellation note visible on his own team's profile summary | ▼ Small sting |

**Emotional arc summary:** Stressed → Feels the penalty → Resigned → Small sting

**Design implications:**
- The warning step (step 2) is important. It must be clear without being punitive in tone. "Affects your trust record" — not "you will be penalised." The difference matters to users who feel the cancellation is unavoidable.
- The reason dropdown provides a structured way to record the cause. It is not used to make a judgement — it is recorded internally for moderation context. Visible to user as a confirmation that the context was noted.
- Short-notice cancellation must not be buried. If Marcus is on mobile in a car park making this call, the flow must be completable in under 90 seconds.
- The "sting" at step 4 (note on team profile) is intentional trust mechanics. It must be visible to the FM (so they understand the consequence) but must not be surfaced publicly in a shaming way.

---

## Map 06 — Fixture Manager: Weather cancellation (no penalty)

**Persona:** Priya (same as Map 03).

**Context:** Sunday morning of the confirmed fixture. It's been raining since 5am. The outfield at her ground is waterlogged. Both captains have agreed: no game.

| # | Step | What she does | What she sees | Emotional arc |
|---|---|---|---|---|
| 1 | Opens platform | Finds fixture. | Confirmed fixture: today. | ▼ Disappointed about the weather; determined about the admin |
| 2 | Initiates cancellation | Taps "Cancel fixture." | Warning step appears. | ○ Reads it |
| 3 | Selects weather | Cancellation reason: "Weather / pitch conditions." | Additional confirmation: "Weather cancellations are noted without trust impact." | ▲ Small relief — system is fair |
| 4 | Confirms | Submits. | "Fixture cancelled — weather. Both teams notified." | ○ Accepted |

**Design implications:**
- The weather cancellation path must be visible on the reason dropdown and must provide the "no trust impact" reassurance during the flow, not after.
- The distinction between "Unable to field a team" and "Weather" must not require the user to read fine print. The UI must surface the consequences of each choice at the point of selection.

---

## Map 07 — Fixture Manager: Match request expires (7 days, no response)

**Persona:** Graham (same as Map 01).

**Context:** Graham sent a match request to Redfield CC 2nd XI 7 days ago. No response.

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Gets notified | Receives email. | "Your match request to Redfield CC 2nd XI has expired (no response after 7 days). Your availability for 14 June is open again." | ▼ Mild annoyance at Redfield; mild relief that the date isn't lost |
| 2 | Returns to availability | Opens platform. Checks dashboard. | Availability card: "Awaiting opponent" (unlocked; available again). | ○ Back to square one but not stuck |
| 3 | Searches again | Re-runs search with same parameters. | Different results — new availability from another club posted in the last week. | △ Small upside of waiting |

**Design implications:**
- The expiry notification must do two things simultaneously: tell Graham his request expired AND tell him his availability is still live. Both pieces of information are critical and must not require him to navigate to find the second piece.
- "Your availability for [date] is open again" is the reassurance. It must be in the notification, not just on the dashboard.
- Step 3 — searching again — suggests the search results state should surface "new since your last search" signals if technically feasible. Not in scope for MVP but worth flagging for v2.

---

## Map 08 — Club Admin: Onboards club, sets up team, assigns Fixture Manager

**Persona:** Helen, 62, club secretary, Thornton CC. She's been managing the club's admin for 15 years. Not a confident digital user but very organised.

**Context:** March. Pre-season. Helen has been asked to register Thornton CC on the new platform. She does admin on a Windows desktop PC.

| # | Step | What she does | What she sees | Emotional arc |
|---|---|---|---|---|
| 1 | Receives invitation | Gets an email (from the platform, prompted by a league contact) with a sign-up link. | Welcome email: "Register your club in 3 steps." Clear, low-pressure. | ○ Sceptical but willing |
| 2 | Step 1: Club details | Enters club name, home ground (postcode lookup), contact email. | Simple form. Postcode autocomplete. Real-time validation. | ○ Manageable |
| 3 | Step 2: Add first team | Selects: 1st XI, T20 + 40-over, Men's, Open, Tier 3. | Team form with dropdown selections. Tooltip explaining tiers. | ○ Slightly uncertain about tier — reads tooltip |
| 4 | Step 3: Assign Fixture Manager | Enters email of the 1st XI captain (Marcus). Platform sends him an invitation. | "Invitation sent to marcus@example.com. He'll receive an email to join as Fixture Manager for the 1st XI." | △ Feels like progress — delegates appropriately |
| 5 | Finishes onboarding | Sees club profile summary. | "Thornton CC is registered. Your 1st XI will appear in search once Marcus completes his sign-up." | ▲ Done for now |
| 6 | Adds second team (later) | Returns next week. Adds 2nd XI. | Same form. | ○ Familiar |

**Emotional arc summary:** Sceptical → Manageable → Slight uncertainty → Progress → Done → Familiar

**Design implications:**
- Helen is the most critical onboarding user — she's the gatekeeper. If she can't get through setup, the club never appears in search.
- 3-step onboarding is the right frame. Not a wizard with 8 screens; not a single overwhelming form.
- Tier selection is a known uncertainty point. The tooltip must be visible and non-intimidating. Not: "Select your tier based on the algorithm's scoring criteria." Just: "How would you describe your standard? Competitive vs recreational."
- The "will appear in search once FM completes sign-up" message sets correct expectations. Helen will wonder if the club is live; this pre-empts that question.
- **Desktop-first for this flow.** Helen uses a desktop PC. The onboarding flow should be optimised for this context. Mobile support still required but it's not the primary viewport for this persona.

---

## Map 09 — Service Provider (Umpire): Receives and responds to support request

**Persona:** Bernard, 68, retired, umpires for fun. On a club roster at Westfield CC. Gets a text-like notification.

**Context:** A Wednesday afternoon. Bernard gets an email from the platform. He's never used it before — he was added to the roster by Helen (the club admin) last week and told "you might get requests through here."

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Receives email | Opens email. | "Westfield Ladies CC have requested your umpiring services for Sunday 7 June, 13:00, Westfield ground. T20 format." Accept / Decline links. | ○ Reads it. Familiar enough to parse. |
| 2 | Checks diary | Puts down phone / closes laptop. Checks paper diary. | — | ○ Normal |
| 3 | Accepts via email link | Clicks "Accept" link in email. | Simple confirmation page: "You've confirmed as umpire for Westfield Ladies CC vs [Opponent] on Sunday 7 June. The fixture contact is Priya [surname]." | ▲ Clear and done |
| 4 | Receives day-before reminder | Email the day before the fixture. | "Reminder: umpiring for Westfield Ladies CC tomorrow, Sunday 7 June, 13:00." | ○ Helpful |

**Emotional arc summary:** Reads it → Normal → Clear and done → Helpful

**Design implications:**
- Bernard may not want to log in to a platform at all. The email-only flow (accept/decline via link without logging in) must work for service providers. This is a critical usability accommodation for this demographic.
- The confirmation page (step 3) must show the relevant contact (Priya) so Bernard knows who to call if needed. The platform should not be the intermediary for on-the-day logistics.
- **Escalation to Agent 1:** Email-action links without login require a secure token-in-URL pattern. This is a security / implementation question for Agent 9 but the user experience of Bernard confirms the requirement is real.

---

## Map 10 — New club: First-time empty dashboard (new entrant experience)

**Persona:** New club, first fixture manager (any persona), platform installed this week.

**Context:** First login. No fixtures. No availability. No connections. The platform is completely empty for this user.

| # | Step | What they see | What they need to feel | Design response |
|---|---|---|---|---|
| 1 | Dashboard (first time) | Completely empty dashboard. | Not: "This platform is pointless." | Empty state must communicate: "The platform works when you use it. Start here." |
| 2 | No search results | First search returns empty (inevitable at low density). | Not: "I wasted my time." | Empty state must pivot to "Post your availability — be found." |
| 3 | First notification (days later) | Receives first match request. | "It works." | First interaction notification must be warm without being sycophantic. |

**Design implications:**
- This is the most important UX challenge in the product. Identified as a critical test hypothesis in `08-usability-test-plan.md`.
- The first-login dashboard empty state is a dedicated design problem, not a default "no content" placeholder.
- **Do not show example/demo data.** Showing fake fixtures to paper over emptiness is dishonest and will create confusion when the user tries to interact with them.
- Instead: contextual guidance ("Your first step is...") with direct action links.
- The empty state must feel like an onboarding prompt, not an error state.

---

## Map 11 — Fixture Manager: Marks fixture complete, submitted review

**Persona:** Marcus (same as Map 05 — but a different, successful fixture).

**Context:** Sunday evening after a completed game. Marcus is in the pub. On his phone.

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Gets review prompt | Evening notification: "How did today's game go? Leave a short review for Thornton CC." | Email or in-app notification. | ○ Slightly tired but happy after the game |
| 2 | Opens review | Clicks through. 3-question form. | Clear questions, 3-point scale each. No comment box. | ○ Fast to complete |
| 3 | Submits | Answers all three. Submits. | "Review recorded. It won't be shared publicly." | ○ Satisfied with the brevity |

**Emotional arc summary:** Tired-happy → Fast → Satisfied

**Design implications:**
- Sunday evening, post-match, on mobile. The review form must be completable in under 60 seconds. Three required questions with a 3-point scale — that is the correct scope. No open text box. No stars. No "How would you rate this experience out of 10."
- The confirmation message must reassure Marcus that his review is private. This is a trust-in-the-platform moment. He must not wonder if he's publicly shaming or praising Thornton.
- Do not use the word "rating" or "stars" anywhere on this screen.

---

## Map 12 — Fixture Manager: Fixture confirmed, venue still missing

**Persona:** Graham (same).

**Context:** Match request accepted. Opponent is away, so Graham's club is hosting. But the home ground is a shared facility — Graham needs to confirm their booking before the venue is "confirmed" on the system.

| # | Step | What he does | What he sees | Emotional arc |
|---|---|---|---|---|
| 1 | Views fixture | Checks fixture. Opponent confirmed. | Status: "Awaiting venue." "What's missing" panel: "Confirm your home ground for this fixture." | ○ Clear |
| 2 | Confirms venue | Clicks "Confirm venue." Selects home ground from saved list. Confirms. | Fixture updates. "What's missing" panel updates or disappears if all gaps resolved. | ▲ Small satisfaction |
| 3 | Views updated fixture | If officials were also missing, "What's missing" panel now shows officials gap only. | Status: "Awaiting officials." | ○ One thing at a time |

**Design implications:**
- "What's missing" panel must handle multi-gap states cleanly. If venue and officials are both missing, the panel must prioritise and sequence actions clearly — not present two competing calls to action simultaneously.
- Confirm venue from a saved list (not re-entering an address) is the primary path. The "Add new venue" path exists but should not be the default for established clubs.
