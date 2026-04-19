# 01 — Content Style Guide

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 8 (Content & Microcopy)
**Feeds:** Agent 7 (screen copy), Agent 9 (translation-ready strings), Agent 10 (marketing — style applies, not content)

---

## 1. Voice in one sentence

Write like the club secretary who has run fixtures for twenty years: direct, specific, quietly competent.

---

## 2. Casing rules

| Element | Rule | Example |
|---|---|---|
| Button labels | Sentence case | `Post availability` not `Post Availability` |
| Page headings (H1) | Sentence case | `Find a game` not `Find A Game` |
| Section headings (H2, H3) | Sentence case | `Needs your attention` |
| Navigation labels | Sentence case | `My fixtures` |
| Status labels | Sentence case | `Awaiting opponent` |
| Trust badges | Title case (names) | `Reliable`, `Established`, `New` |
| Error codes | All caps | `ERR-DATE-001` |
| Date format | Day, day number, month name | `Saturday 12 July` — never `12/07`, never `July 12th` |
| Time format | 24-hour, no leading zero | `14:00` not `2:00 PM` or `14:00:00` |

**Rationale:** Sentence case reads calmer, consistent with GOV.UK and the National Trust digital registers. Title case on CTA buttons is startup register; avoid it.

---

## 3. Punctuation rules

| Rule | Do | Don't |
|---|---|---|
| No exclamation marks in system text | `Availability posted for 14 June.` | `Availability posted!` |
| Oxford comma | `T20, 40-over, or 50-over` | `T20, 40-over or 50-over` |
| Apostrophes: curly | `it's`, `you've` | `it's`, `you've` (straight) |
| Hyphens vs dashes | En dash (–) for ranges, em dash (—) for asides | Do not use double hyphen `--` |
| Serial date ranges | `12–19 July` | `12-19 July` or `July 12 to 19` |
| Format references | `T20`, `40-over`, `50-over`, `timed declaration` | `T-20`, `40 over`, `50-Over` |

---

## 4. Number and date conventions

- **Dates:** `Saturday 12 July` — day name, day number, month. No year unless cross-year context.
- **Dates with year:** `Saturday 12 July 2027`
- **Time:** `14:00` — always. Not `2pm`, not `2:00pm`, not `14:00:00`.
- **Counts:** Spell out one to nine. Use numerals from 10 upward.
- **Distance:** `30 miles` — always spell out; don't abbreviate `mi`.

---

## 5. Spelling and regional English

UK English throughout. Key divergences from US English:

| UK (correct) | US (incorrect) |
|---|---|
| organise | organize |
| recognise | recognize |
| colour | color |
| behaviour | behavior |
| centre | center |
| licence (noun) | license |
| fulfil | fulfill |
| cancelled | canceled |
| travelling | traveling |

---

## 6. Sentence patterns

### State the fact, then the action

> Wrong: "It seems like you haven't added any availability yet. Why not get started today?"
> Right: "No availability posted yet. Post your availability to be found by other teams."

### Specific over vague

> Wrong: "Something went wrong."
> Right: "The date field needs a value. Use the format Saturday 12 July."

### Active voice for errors

> Wrong: "The request could not be processed."
> Right: "The match request could not be sent. Check your internet connection and try again. (ERR-REQ-003)"

### Name the subject

> Wrong: "Confirmed."
> Right: "Fixture confirmed. Both teams have been notified."

---

## 7. Forbidden words and phrasings

From `shared/GLOSSARY.md` — enforced without exception:

**Forbidden phrases:**
- Oops / Uh-oh
- Awesome / Amazing / Great / Fantastic (as affirmations)
- Hey there / Hi there / Welcome back, friend / Hey [name]
- We're on it
- Something went wrong (without more information)
- Click here
- Learn more (always specify: "How trust badges work")
- Looks like / Seems like / It appears that
- Seamless / Effortless / Powered by
- Pending (use "Awaiting")
- Community

**Forbidden concepts in UI:**
- Algorithm
- Marketplace
- Rating (as noun)
- Stars / percentages in trust contexts
- Score (as noun in user-facing copy)

**Forbidden cricket clichés (brand/naming, not product copy):**
- Wicket, stumps, googly, howzat, maiden, crease, yorker

---

## 8. Empty state rules

Every empty state has three parts:

1. **Heading:** States the fact. One line. No apology.
2. **Body:** Explains why it's empty (if non-obvious) and what the user can do.
3. **Action:** A button or link to the most relevant next step. Specific label — not "Get started".

| Wrong | Right |
|---|---|
| "Looks like there's nothing here yet." | "No fixtures yet." |
| "Be the first to post!" | "Post your availability to be found by other teams searching for a game." |
| "Get started" (CTA) | "Post availability" (CTA) |

---

## 9. Error message rules

Every error message has:

1. **What happened** — one clear sentence.
2. **Why** — if known and useful.
3. **What the user can do** — a concrete next step.
4. **Error code** — for support escalation (format: `ERR-[AREA]-[NUMBER]`).

No blame language. The subject of the sentence is the system or the field, not the user.

| Wrong | Right |
|---|---|
| "You entered an invalid date." | "The date field needs a value in the format Saturday 12 July." |
| "You don't have permission." | "This action requires Club Administrator access. Contact your Club Administrator." |
| "Error 500" | "The request could not be completed due to a server error. Try again in a moment. If this continues, contact support with reference ERR-SRV-500." |

---

## 10. Notification rules

**Subject line:** The fact, precisely. Format: `[Subject] — [what happened/what's needed]`

| Wrong | Right |
|---|---|
| "You have a new message" | "Thornton CC 1st XI has sent you a match request for 14 June" |
| "Great news from the platform!" | "Match request accepted — fixture on 14 June is confirmed" |
| "Your request has been actioned" | "Blanktown CC 2nd XI has declined your match request for 28 June" |

**Preheader:** Adds context; does not repeat the subject line.

**Body:** One to three short paragraphs. Lead with what the recipient needs to do, if anything. End with the primary CTA link — one link, one action.

**Signature:** Plain sign-off. No "The [Platform] Team" cheerfulness. Just: `[Platform name]`

---

## 11. Button label rules

- **Verb-first:** `Post availability`, not `Availability posting`
- **No articles:** `Accept request` not `Accept the request`
- **No "Submit":** Use the specific action — `Send match request`, `Leave a review`, `Post availability`
- **Destructive actions:** Sentence case, no colour shorthand. Always followed by a confirmation step. Label: `Cancel fixture` (not `Yes, cancel` or `Confirm cancellation`)
- **Secondary actions:** Styled differently from primary. Use `Decline` not `No thanks`.

---

## 12. Form field labels and placeholder text

**Labels:** Always visible. Never inside the field only (accessibility requirement, WCAG 2.2 AA).

**Placeholder text:** A concrete example, not an instruction.

| Field | Label | Placeholder |
|---|---|---|
| Date | Date | Saturday 12 July |
| Format | Format | — (use a select, not placeholder) |
| Note to opposition | Note (optional) | — (no placeholder; leave blank) |
| Club name | Club name | Thornton CC |

**Hint text:** Appears below the label, before the input. Use for constraints or format guidance.

> Date hint: "Use the format Saturday 12 July."
> Note hint: "This is optional. It will be shown to the receiving team."

---

## 13. Read-aloud test

Before finalising any copy, read it aloud. Ask:

- Does it sound like a startup? → Rewrite.
- Does it sound like a sports app or betting site? → Rewrite.
- Does it sound like the National Trust, GOV.UK, or a well-run county club's website? → Keep.

---

## 14. Translation readiness

All strings are written to be translation-ready for Agent 9:

- No string concatenation in UI (`"Hi, " + userName` produces untranslatable strings)
- Variable tokens use named placeholders: `{team_name}`, `{fixture_date}`, `{format}`
- Date formatting must go through a localisation-aware date formatter, not string embedding
- Pluralisation handled separately: `{count} fixture` / `{count} fixtures`

---

## 15. Accessibility in copy

- Link text must describe the destination: `View match request from Thornton CC` not `Click here`
- Error messages must be associated with their field via `aria-describedby`
- Screen reader only text (`.sr-only`) used for icon-only buttons — copy must be written for these too
- Status updates for async actions (loading, success, error) must be announced via `aria-live`

---

*Maintained by: Agent 8 (Content & Microcopy)*
*Vocabulary authority: Agent 3 (Naming & Verbal Identity), `shared/GLOSSARY.md`*
