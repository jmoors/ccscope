# 02 — Screen Copy

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 8 (Content & Microcopy)
**Consumes:** Agent 6 wireframes (`04-wireframes-desktop.md`, `05-wireframes-mobile.md`, `06-edge-case-wireframes.md`)
**Feeds:** Agent 7 (Figma copy), Agent 9 (translation strings)

**Format note:** Each screen section lists strings by slot. Variable tokens use `{curly_brace}` notation. All strings are UK English, sentence case unless noted.

---

## Navigation

### Primary nav labels (desktop sidebar / mobile tab bar)

| Slot | String |
|---|---|
| nav.dashboard | `Dashboard` |
| nav.find | `Find a game` |
| nav.fixtures | `My fixtures` |
| nav.requests | `Requests` |
| nav.notifications | `Notifications` |
| nav.club | `Club` |
| nav.settings | `Settings` |

### Back-navigation labels

Always labelled with destination, never generic "Back".

| From screen | Back label |
|---|---|
| /find/results | `← Search` |
| /find/results/:id | `← Results` |
| /fixtures/:id | `← My fixtures` |
| /fixtures/:id/request | `← Fixture detail` |
| /fixtures/:id/support | `← Fixture detail` |
| /fixtures/:id/review | `← Fixture detail` |
| /requests/:id | `← Requests` |
| /availability/:id | `← My availability` |

### Team context switcher

| Slot | String |
|---|---|
| context.acting_as | `Acting as:` |
| context.switch_prompt | `Switch team` |
| context.switcher.label | `{team_name}` |

---

## Dashboard

### Page heading

`Good morning, {first_name}` / `Good afternoon, {first_name}` / `Good evening, {first_name}`

*Note to Agent 9: time of day mapping — morning 06:00–11:59, afternoon 12:00–17:59, evening 18:00–23:59. Use the system clock in the user's timezone.*

---

### Section: Needs your attention

| Slot | String |
|---|---|
| section.attention.heading | `Needs your attention` |
| section.attention.empty | `Nothing requires action right now.` |

**Match request card (in Needs your attention):**

| Slot | String |
|---|---|
| card.request.incoming.label | `Match request` |
| card.request.incoming.from | `From {team_name}` |
| card.request.incoming.detail | `{fixture_date} · {fixture_format}` |
| card.request.incoming.note_label | `Their note:` |
| card.request.incoming.trust | `Trust badge: {trust_badge_label}` |
| card.request.incoming.cta | `View request` |

**Review due card:**

| Slot | String |
|---|---|
| card.review_due.label | `Review due` |
| card.review_due.detail | `{fixture_date} vs {opponent_team}` |
| card.review_due.body | `Your review is private. It contributes to trust badges but is never shown publicly.` |
| card.review_due.cta | `Leave a review` |

---

### Section: Upcoming fixtures

| Slot | String |
|---|---|
| section.upcoming.heading | `Upcoming fixtures` |
| section.upcoming.empty | `No confirmed fixtures in the next 14 days.` |

**Fixture card:**

| Slot | String |
|---|---|
| card.fixture.status.awaiting_opponent | `Awaiting opponent` |
| card.fixture.status.awaiting_venue | `Awaiting venue` |
| card.fixture.status.awaiting_officials | `Awaiting officials` |
| card.fixture.status.awaiting_response | `Awaiting response` |
| card.fixture.status.confirmed | `Confirmed` |
| card.fixture.status.completed | `Completed` |
| card.fixture.status.cancelled | `Cancelled` |
| card.fixture.date | `{fixture_date}` |
| card.fixture.opponent | `vs {opponent_team}` |
| card.fixture.no_opponent | `No opponent yet` |
| card.fixture.venue | `at {venue_name}` |
| card.fixture.no_venue | `Venue not confirmed` |
| card.fixture.format | `{fixture_format}` |
| card.fixture.cta | `View fixture` |

---

### Section: My availability

| Slot | String |
|---|---|
| section.availability.heading | `My availability` |
| section.availability.empty_short | `No availability posted.` |
| section.availability.cta_post | `Post availability` |

**Availability card:**

| Slot | String |
|---|---|
| card.availability.date | `{fixture_date}` |
| card.availability.format | `{fixture_format}` |
| card.availability.home_away | `{home_or_away}` |
| card.availability.requests | `{count} request` / `{count} requests` |
| card.availability.cta | `Manage` |

---

### Dashboard empty state (new user, no fixtures)

| Slot | String |
|---|---|
| empty.dashboard.heading | `No fixtures yet` |
| empty.dashboard.body | `Start by searching for a game. If no availability matches your dates, post your own and other teams will find you.` |
| empty.dashboard.cta_primary | `Find a game` |
| empty.dashboard.cta_secondary | `Post availability` |

---

## Find a game

### Page heading and subheading

| Slot | String |
|---|---|
| page.find.heading | `Find a game` |
| page.find.subheading | `Search for teams with availability that matches your dates and format.` |

### Search form

| Slot | String |
|---|---|
| form.find.date.label | `Date` |
| form.find.date.hint | `Use the format Saturday 12 July.` |
| form.find.date.placeholder | `Saturday 12 July` |
| form.find.format.label | `Format` |
| form.find.format.default_option | `Any format` |
| form.find.format.options | `T20`, `40-over`, `50-over`, `Timed declaration`, `Any format` |
| form.find.home_away.label | `Home or away` |
| form.find.home_away.options | `Either`, `Home`, `Away` |
| form.find.radius.label | `Distance` |
| form.find.radius.hint | `Maximum distance from your home ground.` |
| form.find.radius.options | `10 miles`, `20 miles`, `30 miles`, `50 miles`, `Any distance` |
| form.find.age.label | `Age group` |
| form.find.age.default_option | `Open age` |
| form.find.gender.label | `Gender` |
| form.find.gender.default_option | `All` |
| form.find.submit | `Search` |

---

## Search results

### Results list (populated)

| Slot | String |
|---|---|
| page.results.heading | `{count} result` / `{count} results` |
| page.results.for | `for {fixture_date}` |
| page.results.sort.label | `Sort by` |
| page.results.sort.options | `Best match`, `Nearest first`, `Most recently posted` |

**Availability result card:**

| Slot | String |
|---|---|
| card.result.team | `{team_name}` |
| card.result.club | `{club_name}` |
| card.result.date | `{fixture_date}` |
| card.result.format | `{fixture_format}` |
| card.result.home_away | `{home_or_away} — {ground_name}` |
| card.result.trust | `{trust_badge_label}` |
| card.result.compatibility_format | `Format mismatch: you prefer {your_format}, they prefer {their_format}` |
| card.result.cta | `View availability` |

### Search results empty state

| Slot | String |
|---|---|
| empty.results.heading | `No availability found for {fixture_date}` |
| empty.results.body | `No teams have posted availability that matches your search. Post your own availability and you will appear in searches by other teams.` |
| empty.results.cta_primary | `Post availability` |
| empty.results.cta_secondary | `Change search` |

*Note to Agent 7: "Post availability" CTA must pre-fill date and format from the failed search. This is specified in Agent 6 wireframes as a critical usability mechanism.*

---

## Availability detail (before sending a match request)

### Page heading

`{team_name}` (the team whose availability is being viewed)

### Content slots

| Slot | String |
|---|---|
| detail.avail.date | `{fixture_date}` |
| detail.avail.format | `{fixture_format}` |
| detail.avail.home_away | `{home_or_away} at {ground_name}` |
| detail.avail.trust.label | `Trust badge` |
| detail.avail.trust.value | `{trust_badge_label}` |
| detail.avail.trust.explain_link | `How trust badges work` |
| detail.avail.club.label | `Club` |
| detail.avail.club.value | `{club_name}` |
| detail.avail.note.label | `Their note` |
| detail.avail.cta_primary | `Send match request` |
| detail.avail.cta_secondary | `Back to results` |

**Compatibility notices (shown inline, informational — not errors):**

| Slot | String |
|---|---|
| compat.format.notice | `Format note: your team usually plays {your_format}. This availability is for {their_format}. You can still send a request.` |
| compat.age.notice | `Age group note: this availability is for {their_age_group}. Your team is listed as {your_age_group}.` |

---

## Send match request

### Page heading

`Send match request to {team_name}`

### Form

| Slot | String |
|---|---|
| form.request.fixture_date.label | `Date` |
| form.request.fixture_date.value | `{fixture_date}` *(pre-filled, read-only)* |
| form.request.format.label | `Format` |
| form.request.format.value | `{fixture_format}` *(pre-filled, read-only)* |
| form.request.home_away.label | `Home or away` |
| form.request.home_away.hint | `Indicate which team would be hosting.` |
| form.request.note.label | `Note (optional)` |
| form.request.note.hint | `Visible to the receiving team. Keep it brief — a sentence or two at most.` |
| form.request.note.char_limit_hint | `{remaining} characters remaining` |
| form.request.expiry.info | `This request expires if not answered within 7 days.` |
| form.request.submit | `Send match request` |
| form.request.cancel | `Cancel` |

### Confirmation screen (after sending)

| Slot | String |
|---|---|
| confirm.request.heading | `Match request sent` |
| confirm.request.body | `Your request has been sent to {team_name}. They have until {deadline_date} to respond. You will be notified as soon as they do.` |
| confirm.request.cta_primary | `Back to fixture` |
| confirm.request.cta_secondary | `Back to results` |

---

## Match request detail (receiving team)

### Page heading

`Match request from {requesting_team}`

### Content slots

| Slot | String |
|---|---|
| detail.request.date | `{fixture_date}` |
| detail.request.format | `{fixture_format}` |
| detail.request.home_away | `{home_or_away} at {ground_name}` |
| detail.request.from.label | `From` |
| detail.request.from.value | `{requesting_team}, {club_name}` |
| detail.request.trust.label | `Trust badge` |
| detail.request.trust.value | `{trust_badge_label}` |
| detail.request.trust.explain_link | `How trust badges work` |
| detail.request.note.label | `Their note` |
| detail.request.expiry.label | `Respond by` |
| detail.request.expiry.value | `{deadline_date}` |
| detail.request.cta_accept | `Accept` |
| detail.request.cta_decline | `Decline` |

### Accept confirmation dialog

| Slot | String |
|---|---|
| dialog.accept.heading | `Accept match request` |
| dialog.accept.body | `Accepting confirms a fixture on {fixture_date} with {requesting_team}. Both teams will be notified.` |
| dialog.accept.cta_confirm | `Accept` |
| dialog.accept.cta_cancel | `Cancel` |

### Decline confirmation dialog

| Slot | String |
|---|---|
| dialog.decline.heading | `Decline match request` |
| dialog.decline.body | `{requesting_team} will be notified that you have declined. You do not need to give a reason.` |
| dialog.decline.cta_confirm | `Decline` |
| dialog.decline.cta_cancel | `Cancel` |

### Post-accept confirmation

| Slot | String |
|---|---|
| confirm.accept.heading | `Fixture confirmed` |
| confirm.accept.body | `Your fixture on {fixture_date} with {requesting_team} is confirmed. Both teams have been notified.` |
| confirm.accept.cta | `View fixture` |

### Post-decline confirmation

| Slot | String |
|---|---|
| confirm.decline.heading | `Request declined` |
| confirm.decline.body | `{requesting_team} has been notified.` |
| confirm.decline.cta | `Back to requests` |

---

## Post availability

### Page heading

`Post availability`

### Form

| Slot | String |
|---|---|
| form.avail.date.label | `Date` |
| form.avail.date.hint | `Use the format Saturday 12 July.` |
| form.avail.format.label | `Format` |
| form.avail.format.hint | `Select the format your team is looking to play.` |
| form.avail.home_away.label | `Home or away` |
| form.avail.home_away.hint | `Home means you would host at your ground. Away means you would travel.` |
| form.avail.home_away.options | `Home`, `Away`, `Either` |
| form.avail.venue.label | `Ground` *(shown if Home or Either selected)* |
| form.avail.venue.hint | `Select from your club's registered grounds.` |
| form.avail.expiry.label | `Available until` |
| form.avail.expiry.hint | `Your availability will be removed from search results after this date if no match is arranged.` |
| form.avail.note.label | `Note (optional)` |
| form.avail.note.hint | `Visible to teams who find your availability. Keep it brief.` |
| form.avail.submit | `Post availability` |
| form.avail.cancel | `Cancel` |

### Confirmation

| Slot | String |
|---|---|
| confirm.avail.heading | `Availability posted for {fixture_date}` |
| confirm.avail.body | `Your availability is now visible to teams searching for a game on that date. You will be notified when a team sends you a match request.` |
| confirm.avail.cta_primary | `Back to dashboard` |
| confirm.avail.cta_secondary | `Post another date` |

---

## Fixture detail

### Page heading

`{fixture_date} vs {opponent_team}` *(confirmed)*
`{fixture_date}` *(awaiting opponent)*

### Status panel — "What's missing"

| Slot | String |
|---|---|
| panel.missing.heading | `What's needed` |
| panel.missing.item.opponent.pending | `Opponent — not confirmed` |
| panel.missing.item.opponent.done | `Opponent — {opponent_team}` |
| panel.missing.item.venue.pending | `Venue — not confirmed` |
| panel.missing.item.venue.done | `Venue — {venue_name}` |
| panel.missing.item.officials.pending | `Umpire — not confirmed` |
| panel.missing.item.officials.done | `Umpire — {official_name}` |
| panel.missing.item.officials.deferred | `Umpire — confirm venue first` |
| panel.missing.all_done | `Everything confirmed.` |

### CTAs by status

| Status | CTA label |
|---|---|
| Awaiting opponent | `Find a game` |
| Awaiting response | `View sent request` |
| Awaiting venue | `Confirm venue` |
| Awaiting officials | `Find an umpire` |
| Confirmed | `Cancel fixture` |
| Completed | `Leave a review` *(if review window open)* |
| Completed, reviewed | `View fixture summary` |
| Cancelled | — *(no CTA)* |

### Fixture detail fields

| Slot | String |
|---|---|
| detail.fixture.date | `{fixture_date}` |
| detail.fixture.format | `{fixture_format}` |
| detail.fixture.home_away | `{home_or_away} at {venue_name}` |
| detail.fixture.opponent.label | `Opposition` |
| detail.fixture.opponent.value | `{opponent_team}, {opponent_club}` |
| detail.fixture.trust.label | `Their trust badge` |
| detail.fixture.trust.value | `{trust_badge_label}` |
| detail.fixture.officials.label | `Umpire` |
| detail.fixture.officials.value | `{official_name}` |
| detail.fixture.officials.not_set | `Not confirmed` |
| detail.fixture.status.label | `Status` |
| detail.fixture.cancel.link | `Cancel fixture` |

### Cancel fixture flow

| Slot | String |
|---|---|
| dialog.cancel.heading | `Cancel this fixture` |
| dialog.cancel.body | `Both teams will be notified. This cannot be undone.` |
| dialog.cancel.reason.label | `Reason (optional)` |
| dialog.cancel.reason.options | `Weather`, `Player numbers`, `Ground unavailable`, `Mutual agreement`, `Other` |
| dialog.cancel.cta_confirm | `Cancel fixture` |
| dialog.cancel.cta_back | `Keep fixture` |

---

## Find support (umpire request)

### Page heading

`Find an umpire for {fixture_date}`

### Form

| Slot | String |
|---|---|
| form.support.intro | `Requests go to umpires on your club's roster. Your Club Administrator can add umpires to the roster.` |
| form.support.roster.label | `Umpires available` |
| form.support.roster.empty | `No umpires on your club's roster. Ask your Club Administrator to add them.` |
| form.support.note.label | `Note (optional)` |
| form.support.note.hint | `Visible to the umpire. Include format, start time, or anything relevant.` |
| form.support.submit | `Send request` |
| form.support.cancel | `Cancel` |

### Confirmation

| Slot | String |
|---|---|
| confirm.support.heading | `Request sent to {official_name}` |
| confirm.support.body | `They have been notified and will respond directly. You will be notified when they accept or decline.` |
| confirm.support.cta | `Back to fixture` |

---

## Post-match review form

### Page heading

`Review: {fixture_date} vs {opponent_team}`

### Intro

| Slot | String |
|---|---|
| form.review.intro | `Your review is private. It is never shown publicly. It contributes to trust badges over time.` |
| form.review.window_closes | `Review window closes {window_close_date}.` |

### Questions (3-point scale: each question has 3 options — do not add more)

**Question 1 — Reliability**

| Slot | String |
|---|---|
| form.review.q1.label | `Did the fixture go ahead as arranged?` |
| form.review.q1.option_1 | `Yes, without any issues` |
| form.review.q1.option_2 | `Yes, but there were last-minute changes` |
| form.review.q1.option_3 | `No, the fixture was cancelled or disrupted` |

**Question 2 — Conduct**

| Slot | String |
|---|---|
| form.review.q2.label | `How would you describe the conduct of the opposing team?` |
| form.review.q2.option_1 | `Good — played in the right spirit` |
| form.review.q2.option_2 | `Acceptable` |
| form.review.q2.option_3 | `Concerning — I would not arrange a fixture with them again` |

**Question 3 — Would you play again?**

| Slot | String |
|---|---|
| form.review.q3.label | `Would you arrange a fixture with this team again?` |
| form.review.q3.option_1 | `Yes` |
| form.review.q3.option_2 | `Possibly` |
| form.review.q3.option_3 | `No` |

### Submission

| Slot | String |
|---|---|
| form.review.submit | `Submit review` |
| form.review.skip.link | `Skip for now` |
| form.review.skip.confirm | `You can submit your review until {window_close_date}. After that, the window closes.` |

### Review confirmation

| Slot | String |
|---|---|
| confirm.review.heading | `Review submitted` |
| confirm.review.body | `Your review has been recorded. It is private and will never be shown publicly.` |
| confirm.review.cta | `Back to fixture` |

---

## My fixtures list

### Page heading

`My fixtures`

### Filters

| Slot | String |
|---|---|
| filter.fixtures.all | `All` |
| filter.fixtures.upcoming | `Upcoming` |
| filter.fixtures.past | `Past` |
| filter.fixtures.needs_action | `Needs action` |

### Empty states

| Context | Heading | Body | CTA |
|---|---|---|---|
| All fixtures, new user | `No fixtures yet` | `Find a game or post your availability. Fixtures appear here once a match request has been accepted.` | `Find a game` |
| Upcoming filter, no results | `No upcoming fixtures` | `No confirmed fixtures in the diary. Check your availability or search for a game.` | `Find a game` |
| Past filter, no results | `No past fixtures` | `Completed fixtures will appear here.` | — |

---

## My availability list

### Page heading

`My availability`

### Empty state

| Slot | String |
|---|---|
| empty.availability.heading | `No availability posted` |
| empty.availability.body | `Post your availability for dates you need a game. Other teams searching for opponents on those dates will find you.` |
| empty.availability.cta | `Post availability` |

---

## Requests list

### Page heading

`Requests`

### Tabs

| Slot | String |
|---|---|
| tab.requests.incoming | `Incoming` |
| tab.requests.sent | `Sent` |

### Empty states

| Context | Heading | Body | CTA |
|---|---|---|---|
| No incoming requests | `No incoming requests` | `When a team sends you a match request, it will appear here.` | — |
| No sent requests | `No sent requests` | `Find availability and send a match request to start a fixture.` | `Find a game` |

---

## Notifications

### Page heading

`Notifications`

### Empty state

| Slot | String |
|---|---|
| empty.notifications.heading | `No notifications` |
| empty.notifications.body | `Notifications appear here when there is activity on your fixtures or requests.` |

### Notification item labels

| Event | Label |
|---|---|
| Match request received | `Match request from {team_name}` |
| Match request accepted | `{team_name} accepted your match request` |
| Match request declined | `{team_name} declined your match request` |
| Match request withdrawn | `{team_name} withdrew their match request` |
| Match request expired | `Your match request to {team_name} has expired` |
| Fixture confirmed | `Fixture confirmed — {fixture_date}` |
| Fixture cancelled | `Fixture cancelled — {fixture_date}` |
| Review prompt | `Review due for {fixture_date}` |
| Fixture reminder | `Fixture tomorrow — {fixture_date}` *(or `in {N} days`)* |
| Support request received | `Umpire request for {fixture_date}` |
| Support request accepted | `{official_name} accepted your umpire request` |
| Support request declined | `{official_name} declined your umpire request` |

---

## Club profile (public, unauthenticated)

### Page heading

`{club_name}`

### Sections

| Slot | String |
|---|---|
| club.home_ground | `Home ground: {ground_name}` |
| club.teams_heading | `Teams` |
| club.no_teams | `No teams listed.` |
| club.trust.label | `Trust badge` |
| club.trust.value | `{trust_badge_label}` |
| club.trust.explain_link | `How trust badges work` |

---

## Club administration

### Club profile edit

| Slot | String |
|---|---|
| page.club_edit.heading | `Edit club profile` |
| form.club.name.label | `Club name` |
| form.club.name.hint | `Use your club's full name as registered. Example: Thornton CC.` |
| form.club.home_ground.label | `Home ground` |
| form.club.contact.label | `Contact email` |
| form.club.contact.hint | `Used for official correspondence only. Not shown publicly.` |
| form.club.submit | `Save changes` |
| confirm.club_edit.body | `Club profile updated.` |

### Team management

| Slot | String |
|---|---|
| page.teams.heading | `Teams` |
| page.teams.add_cta | `Add team` |
| empty.teams.heading | `No teams added yet` |
| empty.teams.body | `Add your club's teams to allow fixture managers to post availability and receive match requests.` |
| empty.teams.cta | `Add team` |
| form.team.name.label | `Team name` |
| form.team.name.hint | `Use standard format: 1st XI, 2nd XI, Sunday XI, Colts U18.` |
| form.team.format.label | `Usual format` |
| form.team.tier.label | `Playing tier` |
| form.team.submit | `Save team` |

### Roster management (umpires/scorers)

| Slot | String |
|---|---|
| page.roster.heading | `Club roster` |
| page.roster.subheading | `Umpires and scorers available through your club.` |
| page.roster.add_cta | `Add person` |
| empty.roster.heading | `No one on the roster yet` |
| empty.roster.body | `Add umpires and scorers to your club's roster. Fixture managers can then request them for specific fixtures.` |
| empty.roster.cta | `Add person` |
| form.roster.name.label | `Name` |
| form.roster.role.label | `Role` |
| form.roster.role.options | `Umpire`, `Scorer` |
| form.roster.email.label | `Email address` |
| form.roster.email.hint | `Used to send them support requests. Not shown to other clubs.` |
| form.roster.submit | `Add to roster` |

---

## Onboarding — club setup (3 steps)

### Step 1: Club details

| Slot | String |
|---|---|
| onboarding.step1.heading | `Set up your club` |
| onboarding.step1.subheading | `Your club profile is visible to other teams. Add your club's details to get started.` |
| onboarding.step_indicator | `Step {current} of {total}` |
| onboarding.step1.cta | `Continue` |

### Step 2: Add your first team

| Slot | String |
|---|---|
| onboarding.step2.heading | `Add your first team` |
| onboarding.step2.subheading | `A club needs at least one team before you can find games or post availability.` |
| onboarding.step2.cta | `Continue` |
| onboarding.step2.skip | `I'll add teams later` |

### Step 3: Notification preferences

| Slot | String |
|---|---|
| onboarding.step3.heading | `Notification preferences` |
| onboarding.step3.subheading | `You will be notified when match requests arrive, fixtures change, and reviews are due. You can change these later.` |
| onboarding.step3.cta | `Go to dashboard` |

---

## Settings

### Page heading

`Settings`

### Sections

| Slot | String |
|---|---|
| settings.section.notifications | `Notification preferences` |
| settings.section.account | `Account` |

### Notification preferences

| Slot | String |
|---|---|
| settings.notif.heading | `Notification preferences` |
| settings.notif.group.match_requests.label | `Match requests and responses` |
| settings.notif.group.match_requests.note | `Required. Cannot be turned off.` |
| settings.notif.group.fixture_updates.label | `Fixture status changes` |
| settings.notif.group.fixture_updates.note | `Required. Cannot be turned off.` |
| settings.notif.group.support_requests.label | `Umpire and scorer requests` |
| settings.notif.group.review_prompts.label | `Post-match review prompts` |
| settings.notif.group.digest.label | `Weekly activity digest` |
| settings.notif.group.reminders.label | `Deadline and expiry reminders` |
| settings.notif.quiet_hours.label | `Quiet hours` |
| settings.notif.quiet_hours.hint | `Notifications during quiet hours are held and delivered at 07:00.` |
| settings.notif.quiet_hours.default | `22:00 – 07:00` |
| settings.notif.save | `Save preferences` |
| confirm.notif.save | `Notification preferences saved.` |

---

## Service provider (umpire/scorer) portal

### Dashboard

| Slot | String |
|---|---|
| sp.page.heading | `Support requests` |
| sp.section.incoming | `Incoming` |
| sp.section.upcoming | `Upcoming fixtures` |
| sp.section.past | `Past fixtures` |

### Empty states

| Context | Heading | Body |
|---|---|---|
| No incoming requests | `No incoming requests` | `When a fixture manager sends you a request, it will appear here.` |
| No upcoming fixtures | `No upcoming fixtures` | `Accepted requests will appear here.` |

### Request detail

| Slot | String |
|---|---|
| sp.request.from | `Request from {team_name}` |
| sp.request.date | `{fixture_date}` |
| sp.request.format | `{fixture_format}` |
| sp.request.venue | `at {venue_name}` |
| sp.request.note.label | `Their note` |
| sp.request.expiry | `Respond by {deadline_date}` |
| sp.request.cta_accept | `Accept` |
| sp.request.cta_decline | `Decline` |

---

## Trust badge context (inline, shown wherever badge appears)

| Badge | Display string | Tooltip / explain text |
|---|---|---|
| New | `New` | `This club has completed fewer than [N] fixtures on the platform. No positive or negative signal yet.` |
| Reliable | `Reliable` | `This club has a positive track record based on completed fixtures and post-match reviews.` |
| Established | `Established` | `This club has a long-standing positive track record.` |

**"How trust badges work" link** — links to help centre article `HC-03`.

---

*Agent 7: use these strings as final copy in Figma. Replace all wireframe placeholder text with the strings above.*
*Agent 9: each string key (e.g., `card.fixture.status.confirmed`) is the translation key. Variables are in `{curly_brace}` notation.*
