# 04 — Wireframes: Desktop

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 6 (Information Architecture & Flows)  
**Status:** Draft — annotation-heavy; for thinking, not selling

**Viewport:** 1280px wide minimum. Left sidebar nav (240px). Content area (full remaining width).  
**Greyscale only.** Borders = outlines. Fills = grey blocks. Text = real copy, no lorem ipsum.  
**State variants:** Each screen has Default, Empty, Loading, and Error states documented.

---

## Screen 1 — Dashboard

### Default state (user has active fixtures)

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [PLATFORM NAME]                                    [Graham Okafor ▼] [2nd XI ▼]  │
├───────────────┬────────────────────────────────────────────────────────────────────┤
│               │                                                                    │
│  ● Dashboard  │  Good evening, Graham                                              │
│  ○ Find a     │                                                                    │
│    game       │  ┌──────────────────────────────────────────────────────────────┐ │
│  ○ My         │  │ NEEDS YOUR ATTENTION                                         │ │
│    fixtures   │  │                                                              │ │
│  ○ Requests   │  │ ┌──────────────────────────────────────────────────────────┐ │ │
│    [1]        │  │ │ Match request from Thornton CC 1st XI                    │ │ │
│  ○ Notify.    │  │ │ Sunday 14 June · T20 · Home at Thornton Park             │ │ │
│    [3]        │  │ │ "We'd love a game. Similar level, good pitch."           │ │ │
│               │  │ │ Trust badge: ◆ Reliable           [View request →]       │ │ │
│  ─────────    │  │ └──────────────────────────────────────────────────────────┘ │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
│  ○ Club       │                                                                    │
│  ○ Settings   │  UPCOMING FIXTURES                                                 │
│               │                                                                    │
│               │  ┌────────────────────────────┐  ┌────────────────────────────┐  │
│               │  │ Sat 23 May                 │  │ Sun 7 June                 │  │
│               │  │ vs Redfield CC 2nd XI      │  │ [Awaiting response]        │  │
│               │  │ ◆ Confirmed                │  │ Sent to Westfield CC 1st   │  │
│               │  │ T20 · Home                 │  │ Waiting since 2 days ago   │  │
│               │  │ [View →]                   │  │ [View →]  [Withdraw]       │  │
│               │  └────────────────────────────┘  └────────────────────────────┘  │
│               │                                                                    │
│               │  PUBLISHED AVAILABILITY (no match request yet)                    │
│               │                                                                    │
│               │  ┌────────────────────────────────────────────────────────────┐   │
│               │  │ Sun 28 June · T20 · Away preferred · within 20 miles       │   │
│               │  │ Published 5 days ago · Awaiting opponent                   │   │
│               │  │ [Edit]  [Withdraw]                                         │   │
│               │  └────────────────────────────────────────────────────────────┘   │
│               │                                                                    │
│               │  [Find a game]    [Post availability]                              │
└───────────────┴────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] Greeting uses first name only. No "Welcome back!" or "Good to see you."
- [B] "Needs your attention" panel appears only when there are action items. It is not a permanent section — if nothing needs attention, it is absent.
- [C] Badge count on "Requests" in nav reflects unread/unactioned requests only.
- [D] Team context picker (2nd XI ▼) is persistent and prominent. Context switch refreshes all fixture data.
- [E] "Awaiting response" fixture card shows elapsed time and a withdraw option. This answers the user's implicit question: "When does this expire?"
- [F] The two primary CTAs at the bottom (Find a game / Post availability) are present even when there are active fixtures. The dashboard is a dispatch surface, not just a status page.

---

### Empty state (new user, no fixtures, no availability)

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [PLATFORM NAME]                                    [Graham Okafor ▼] [2nd XI ▼]  │
├───────────────┬────────────────────────────────────────────────────────────────────┤
│  ● Dashboard  │                                                                    │
│  ○ Find       │  Hello, Graham.                                                    │
│  ○ Fixtures   │                                                                    │
│  ○ Requests   │  ┌──────────────────────────────────────────────────────────────┐ │
│  ○ Notify.    │  │                                                              │ │
│               │  │  Your fixture list is empty.                                 │ │
│               │  │                                                              │ │
│               │  │  Start by searching for available teams, or post your        │ │
│               │  │  own availability so other teams can find you.               │ │
│               │  │                                                              │ │
│               │  │  [Find a game]          [Post availability]                  │ │
│               │  │                                                              │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
│               │                                                                    │
│               │  ─────────────────────────────────────────────────────────────── │
│               │                                                                    │
│               │  HOW IT WORKS                                                      │
│               │                                                                    │
│               │  1. Search for available teams in your area and format.            │
│               │  2. Send a match request when you find a suitable team.            │
│               │  3. They accept, and your fixture is confirmed.                    │
│               │  4. If no teams are available, post your availability.             │
│               │     Other clubs will find you.                                     │
│               │                                                                    │
└───────────────┴────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] No dummy data, no fake fixtures. Honest empty state.
- [B] "How it works" is a 4-step summary that communicates the search-first principle without the word "search-first."
- [C] Equal prominence for Find a game and Post availability — not steering toward either. The copy ("start by searching") provides the recommended path without forcing it.
- [D] No onboarding video, no animated tutorial. Boring and direct.

---

### Loading state

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  [████████████████]                                          │
│  [████████████]                                              │
│                                                              │
│  ┌────────────────────┐   ┌────────────────────┐            │
│  │ ░░░░░░░░░░░░░░░░░ │   │ ░░░░░░░░░░░░░░░░░ │            │
│  │ ░░░░░░░░░░░░░░░░░ │   │ ░░░░░░░░░░░░░░░░░ │            │
│  │ ░░░░░░░░░░         │   │ ░░░░░░░░░░         │            │
│  └────────────────────┘   └────────────────────┘            │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

**Annotations:** Skeleton loading pattern. Content-shaped grey blocks. No spinner. No "Loading..." text. Avoids layout shift when content arrives.

---

### Error state

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  Unable to load your dashboard.                              │
│                                                              │
│  Check your internet connection and try again.               │
│                                                              │
│  [Try again]                                                 │
│                                                              │
│  If this continues, contact support at                       │
│  support@[platformdomain].co.uk                              │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

**Annotations:**
- No emoji. No "Oops!" No exclamation marks.
- Tells the user what to do, not just what went wrong.
- Support contact is plain text, always present on error screens.

---

## Screen 2 — Find a game (search form)

### Default state

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [PLATFORM NAME]                                    [Graham Okafor ▼] [2nd XI ▼]  │
├───────────────┬────────────────────────────────────────────────────────────────────┤
│  ○ Dashboard  │                                                                    │
│  ● Find a     │  Find a game                                                       │
│    game       │                                                                    │
│  ○ Fixtures   │  ┌──────────────────────────────────────────────────────────────┐ │
│  ○ Requests   │  │                                                              │ │
│  ○ Notify.    │  │  Date                                                        │ │
│               │  │  ┌──────────────────────────┐                               │ │
│               │  │  │  14 June 2026         ▼  │  or  [Date window ▼]          │ │
│               │  │  └──────────────────────────┘                               │ │
│               │  │                                                              │ │
│               │  │  Format                                                      │ │
│               │  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌────────┐ ┌────────┐ │ │
│               │  │  │   T20   │ │ 40-over │ │ 50-over │ │ Timed  │ │ Sunday │ │ │
│               │  │  │ ●       │ │         │ │         │ │        │ │        │ │ │
│               │  │  └─────────┘ └─────────┘ └─────────┘ └────────┘ └────────┘ │ │
│               │  │                                                              │ │
│               │  │  Home or away preference                                     │ │
│               │  │  ○ No preference   ● Home preferred   ○ Away preferred       │ │
│               │  │                                                              │ │
│               │  │  Distance                                                    │ │
│               │  │  ┌─────────────────────────┐                                │ │
│               │  │  │  Within 20 miles      ▼ │                                │ │
│               │  │  └─────────────────────────┘                                │ │
│               │  │                                                              │ │
│               │  │  ▶ More options (age group, gender)                          │ │
│               │  │                                                              │ │
│               │  │  [Search for available teams]                                │ │
│               │  │                                                              │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
└───────────────┴────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] Format selection uses a segmented toggle, not a dropdown. This makes all 5 options visible without a click to open. The most common format (T20 or 40-over) is not pre-selected — the user must actively choose. This avoids incorrect format defaults creating wrong search results.
- [B] "More options" expander for age group and gender — these are less frequently changed. Power users can access them; casual users are not distracted by them.
- [C] "Home preferred" is the pre-selected radio — this is the most common scenario (home teams posting availability tend to stay home). If the user's club has no home ground set, this radio is greyed with a note: "Add your home ground in Club settings."
- [D] Date window option (collapsible) allows users to search across a range of dates. Not the default — most users are searching for a specific date.
- [E] The form assumes the user's home postcode as the search origin. This is drawn from their club profile. A "Change location" override link is present for edge cases.

---

### Loading state (after submit)

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  Searching for teams available on 14 June...                     │
│                                                                  │
│  ─────────────────────────────────────────────                   │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░                  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░                                     │
│                                                                  │
│  (skeleton cards appear after 500ms)                             │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Screen 3 — Search results

### Populated state

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [PLATFORM NAME]                                    [Graham Okafor ▼] [2nd XI ▼]  │
├───────────────┬────────────────────────────────────────────────────────────────────┤
│  ○ Dashboard  │                                                                    │
│  ● Find a     │  [← Back to search]    14 June · T20 · Home preferred · 20 miles  │
│    game       │                                                                    │
│  ○ Fixtures   │  4 teams available                                                 │
│  ○ Requests   │                                                                    │
│  ○ Notify.    │  ┌──────────────────────────────────────────────────────────────┐ │
│               │  │ Thornton CC 1st XI                           8 miles away    │ │
│               │  │ T20 · Men's · Open · Tier 3   ◆ Reliable                    │ │
│               │  │ Home: Thornton Park, Thornton                                │ │
│               │  │ [View availability →]                                        │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
│               │                                                                    │
│               │  ┌──────────────────────────────────────────────────────────────┐ │
│               │  │ Redfield CC 2nd XI                          13 miles away    │ │
│               │  │ T20 · Men's · Open · Tier 3   ● New                         │ │
│               │  │ Home: Redfield Recreation Ground                             │ │
│               │  │ [View availability →]                                        │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
│               │                                                                    │
│               │  ┌──────────────────────────────────────────────────────────────┐ │
│               │  │ Southbury CC Sunday XI                      18 miles away    │ │
│               │  │ Sunday format preferred · Men's · Open · Tier 2              │ │
│               │  │ ⚠ Format note: Sunday XI matches on T20 by agreement         │ │
│               │  │ ◆ Reliable                                                   │ │
│               │  │ [View availability →]                                        │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
│               │                                                                    │
│               │  ┌──────────────────────────────────────────────────────────────┐ │
│               │  │ Oldwick CC 1st XI                           19 miles away    │ │
│               │  │ T20 · Men's · Open · Tier 4                                  │ │
│               │  │ ⚠ Tier note: They play at a higher level (Tier 4 vs Tier 3)  │ │
│               │  │ ◆ Established                                                │ │
│               │  │ [View availability →]                                        │ │
│               │  └──────────────────────────────────────────────────────────────┘ │
│               │                                                                    │
│               │  ─────────────────────────────────────────────────────────────── │
│               │                                                                    │
│               │  None of these right?  [Post your availability instead]           │
│               │                                                                    │
└───────────────┴────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] Result count ("4 teams available") is shown prominently. This gives immediate feedback on search density.
- [B] Trust badge is text-based with a simple indicator (◆ symbol), not a star rating or percentage.
- [C] Compatibility notices (⚠ format note, ⚠ tier note) are inline on each card — not hidden behind a click.
- [D] "None of these right?" with "Post your availability" link is the footer of all results lists — even when results exist. This surfaces the fallback path without requiring an empty state.
- [E] Results are sorted by relevance (proximity × tier match × trust). The sort order is not explained to the user; the relevance model is not surfaced.
- [F] The "Back to search" link at top left preserves the search form state when clicked.

---

### Empty state

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│  [← Back to search]    14 June · T20 · Home preferred · 20 miles                 │
│                                                                                    │
│  No availability found for 14 June within 20 miles.                               │
│                                                                                    │
│  ┌──────────────────────────────────────────────────────────────────────────────┐ │
│  │ Try adjusting your search                                                    │ │
│  │                                                                              │ │
│  │  • Widen to 35 miles  [Try this →]                                           │ │
│  │  • Try a different date  [Adjust dates →]                                   │ │
│  │  • Include away games  [Change preference →]                                 │ │
│  └──────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                    │
│  ─────────────────────────────────────────────────────────────────────────────── │
│                                                                                    │
│  Or post your availability for this date.                                          │
│  Other teams searching for a 14 June T20 will find you.                            │
│                                                                                    │
│  [Post availability for 14 June]                                                   │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] Three progressive suggestions before the "post your availability" pivot. Not all three will always apply (e.g., if they already have no preference, the "include away games" suggestion doesn't appear).
- [B] The Post Availability CTA is pre-parameterised: "Post availability for 14 June" — clicking it opens the form with date and format pre-filled.
- [C] No "Oops." No sad face. No "Try again later." Direct and practical.

---

## Screen 4 — Fixture detail + "What's missing" panel

### Populated state (awaiting venue)

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [← My fixtures]                                   [Graham Okafor ▼] [2nd XI ▼]  │
├───────────────┬────────────────────────────────────────────────────────────────────┤
│               │                                                                    │
│               │  Thornton CC 2nd XI vs Westfield CC 2nd XI                         │
│               │  Sunday 14 June 2026 · T20 · Men's                                 │
│               │                                                                    │
│               │  Status: Awaiting venue                                             │
│               │                                                                    │
│               │  ┌───────────────────────────────────┬────────────────────────┐   │
│               │  │                                   │ WHAT'S MISSING         │   │
│               │  │  FIXTURE DETAIL                   │                        │   │
│               │  │                                   │ ✗ Venue               │   │
│               │  │  Home team: Thornton CC 2nd XI    │   [Confirm venue →]    │   │
│               │  │  Away team: Westfield CC 2nd XI   │                        │   │
│               │  │  Format: T20                      │ ✓ Opponent             │   │
│               │  │  Date: Sunday 14 June 2026        │ ✓ Officials not        │   │
│               │  │  Start time: 13:00 (unconfirmed)  │   required (friendly)  │   │
│               │  │  Venue: [Not confirmed]           │                        │   │
│               │  │  Officials: Not required          │ Once venue is          │   │
│               │  │                                   │ confirmed, this        │   │
│               │  │  ─────────────────────────────   │ fixture is Confirmed.  │   │
│               │  │                                   │                        │   │
│               │  │  CONTACTS                         └────────────────────────┘   │
│               │  │  Your FM: You                                                  │
│               │  │  Their FM: Sarah Okonkwo                                       │
│               │  │  Contact via: sarah@westfield.cc                               │
│               │  │                                                                │
│               │  │  ─────────────────────────────                                 │
│               │  │                                                                │
│               │  │  HISTORY                                                       │
│               │  │  23 Apr: Match request sent                                    │
│               │  │  24 Apr: Match request accepted by Westfield CC                │
│               │  │                                                                │
│               │  │  ─────────────────────────────                                 │
│               │  │                                                                │
│               │  │  [Cancel fixture]                                              │
│               │  └───────────────────────────────────────────────────────────────┘ │
└───────────────┴────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] "What's missing" panel is on the right, always visible at this viewport width. It is not a tab, not an accordion, not below the fold.
- [B] ✗ indicates missing; ✓ indicates resolved. The text next to ✓ items is subdued to reduce visual noise.
- [C] "Officials not required (friendly)" resolves the officials gap without requiring action — the fixture manager doesn't need to find an umpire for a friendly. This must be clear and not prompt unnecessary action.
- [D] Contact details for the opposing FM are shown. This is intentional: real-world fixture coordination still happens between humans. The platform facilitates but doesn't replace the phone call.
- [E] History log is a lightweight audit trail. Not prominent, but present for reference.
- [F] "Cancel fixture" is at the bottom, accessible but not prominent. It is a destructive action — its visual weight reflects that.

---

### Confirmed state (all gaps resolved)

```
│  Status: Confirmed ◆                                               │
│                                                                    │
│  ┌─────────────────────────────────────────┬────────────────────┐ │
│  │ FIXTURE DETAIL                          │ ALL CONFIRMED ✓    │ │
│  │                                         │                    │ │
│  │ Home team: Thornton CC 2nd XI           │ ✓ Opponent         │ │
│  │ Away team: Westfield CC 2nd XI          │ ✓ Venue            │ │
│  │ Format: T20                             │ ✓ Officials n/a    │ │
│  │ Date: Sunday 14 June 2026              │                    │ │
│  │ Start time: 13:00                       │ [Cancel fixture]   │ │
│  │ Venue: Thornton Park, Thornton, GU14    │                    │ │
│  │                                         └────────────────────┘ │
│  │ CONTACTS                                                        │
│  │ ...                                                             │
│  └─────────────────────────────────────────────────────────────── │
```

---

### Completed state (mark complete + review prompt)

```
│  Date: Sunday 14 June 2026 (past)                                  │
│                                                                    │
│  [Mark as complete]                                                 │
│                                                                    │
│  (After marking complete:)                                          │
│                                                                    │
│  Status: Completed ✓                                               │
│                                                                    │
│  Leave a review for Westfield CC 2nd XI?                           │
│  Your review is private and helps the platform.                    │
│  [Leave a review]   [Not now — remind me later]                    │
```

---

## Screen 5 — Send match request

### Default state

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [← Westfield CC 2nd XI availability]                                              │
│                                                                                    │
│  Send match request to Westfield CC 2nd XI                                         │
│                                                                                    │
│  ┌──────────────────────────────────────────────────────────────────────────────┐ │
│  │ FIXTURE DETAILS                                                              │ │
│  │ These are drawn from the availability you found.                            │ │
│  │                                                                              │ │
│  │ Date:        Sunday 14 June 2026                   (not editable)            │ │
│  │ Format:      T20                                   (not editable)            │ │
│  │ Your team:   Thornton CC 2nd XI                    (not editable)            │ │
│  │                                                                              │ │
│  │ ─────────────────────────────────────────────────────────────────────────── │ │
│  │                                                                              │ │
│  │ ADD A NOTE (optional)                                                        │ │
│  │ ┌────────────────────────────────────────────────────────────────────────┐ │ │
│  │ │                                                                        │ │ │
│  │ │ e.g. "We play a similar level and have a good outfield. Happy to       │ │ │
│  │ │ provide teas."                                                          │ │ │
│  │ │                                                                        │ │ │
│  │ └────────────────────────────────────────────────────────────────────────┘ │ │
│  │                                            0 / 200 characters               │ │
│  │                                                                              │ │
│  │ ─────────────────────────────────────────────────────────────────────────── │ │
│  │                                                                              │ │
│  │ ⚠ FORMAT NOTE: Westfield CC Sunday XI prefer Sunday format. You're          │ │
│  │ requesting T20. Both teams will need to agree the format before             │ │
│  │ confirming.                                                                  │ │
│  │ [I understand — continue]  ☐  (checkbox, required if notice shown)          │ │
│  │                                                                              │ │
│  │ ─────────────────────────────────────────────────────────────────────────── │ │
│  │                                                                              │ │
│  │  [Cancel]                          [Send match request]                     │ │
│  └──────────────────────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] Fixture details from the availability are not editable. This prevents misrepresentation. The user is requesting to play under the terms already published.
- [B] Compatibility notice (⚠) appears only for soft-match situations. It requires explicit acknowledgement (checkbox). This is not a warning to scare the user — it is information they need to discuss with the other team.
- [C] Note field is a textarea with character counter. Placeholder text is a concrete example, not "Add a note here..."
- [D] Confirmation step after submit (not shown here): "Match request sent. We've notified Westfield CC 2nd XI's fixture manager. They have 7 days to respond."

---

### Error state (cannot send — already has a pending request for this date)

```
│  ┌──────────────────────────────────────────────────────────────────────────────┐ │
│  │ You already have a match request pending for 14 June.                       │ │
│  │ Your availability for this date is locked while that request is active.     │ │
│  │                                                                              │ │
│  │ [View your pending request →]                                               │ │
│  └──────────────────────────────────────────────────────────────────────────────┘ │
```

---

## Screen 6 — Match request detail (receiving team)

### Default state

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ [← Requests]                                      [Priya Sharma ▼] [Ladies XI ▼] │
│                                                                                    │
│  Match request from Thornton CC 1st XI                                             │
│  Received 2 hours ago                                                              │
│                                                                                    │
│  ┌──────────────────────────────────────────────────────────────────────────────┐ │
│  │ REQUESTING TEAM                                                              │ │
│  │                                                                              │ │
│  │ Thornton CC 1st XI                                                           │ │
│  │ T20 · Women's · Open · Tier 3                                                │ │
│  │ Home ground: Thornton Park, Thornton (8 miles from your ground)             │ │
│  │ Trust badge: ● New (joined platform this season)                             │ │
│  │                                                                              │ │
│  │ ─────────────────────────────────────────────────────────────────────────── │ │
│  │                                                                              │ │
│  │ FIXTURE DETAILS                                                              │ │
│  │                                                                              │ │
│  │ Date:   Sunday 7 June 2026                                                   │ │
│  │ Format: T20                                                                  │ │
│  │ Venue:  [To be agreed — both teams have home grounds available]              │ │
│  │                                                                              │ │
│  │ ─────────────────────────────────────────────────────────────────────────── │ │
│  │                                                                              │ │
│  │ NOTE FROM THORNTON CC                                                        │ │
│  │ "We're looking for a Sunday T20 to start our season. Similar level. We      │ │
│  │ can provide teas."                                                           │ │
│  │                                                                              │ │
│  │ ─────────────────────────────────────────────────────────────────────────── │ │
│  │                                                                              │ │
│  │ This request expires on 14 June 2026 (7 days from now).                     │ │
│  │ Your availability for 7 June is reserved until you respond.                  │ │
│  │                                                                              │ │
│  │           [Decline]                    [Accept]                              │ │
│  └──────────────────────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- [A] Trust badge for the requesting team is shown prominently. "New (joined platform this season)" explains the badge without hiding it.
- [B] The note from the requesting FM is given its own clearly labelled section. This is where a lot of the real trust signalling happens in practice.
- [C] Expiry date is shown: "expires 14 June (7 days from now)." This helps the receiving FM understand urgency without creating artificial pressure.
- [D] "Your availability for 7 June is reserved" — this explains the lock mechanism transparently.
- [E] Decline button is present and requires no reason. Accept button requires a confirmation step.
- [F] Accept confirmation step (not shown): "Accepting this request confirms a match on 7 June. You can still cancel later, but cancellations within 48 hours affect your trust record. [Confirm] [Go back]"

---

### Error state (request already expired or withdrawn)

```
│  This match request is no longer active.                            │
│  Thornton CC 1st XI withdrew their request on 8 June.              │
│  Your availability for 7 June is open again.                       │
│                                                                    │
│  [Back to requests]                                                │
```
