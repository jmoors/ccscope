# 04 — Error Messages

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 8 (Content & Microcopy)
**Feeds:** Agent 7 (UI copy), Agent 9 (implementation, error code registry)

**Format:** Each entry has:
- Error code (format: `ERR-[AREA]-[NNN]`)
- HTTP status or trigger (where applicable)
- User-facing heading (one line)
- User-facing body (what happened, why if known, what to do)
- Field-level variant (shorter, for inline validation)
- Internal log note (for Agent 9 — never shown to user)

**Rules applied:**
- No blame language — subject is the field or system, not the user
- No apology theatre ("Sorry", "Unfortunately")
- No exclamation marks
- Specific where possible; no "Something went wrong" without more detail
- Every error has a code for support reference

---

## Area codes

| Code | Area |
|---|---|
| `AUTH` | Authentication and authorisation |
| `DATE` | Date input and validation |
| `FORM` | Generic form validation |
| `FIXT` | Fixture operations |
| `REQ` | Match request operations |
| `AVAIL` | Availability operations |
| `SUPP` | Support request operations |
| `REV` | Review operations |
| `NET` | Network and connectivity |
| `SRV` | Server / system errors |
| `PERM` | Permission / access errors |
| `CLUB` | Club and team management |

---

## Authentication errors

### ERR-AUTH-001 — Sign-in failed

**Trigger:** Invalid email or password
**Heading:** `Sign-in failed`
**Body:** `The email address or password is incorrect. Check your details and try again.`
**Field-level:** `Email address or password is incorrect.`
**Internal note:** Do not reveal which field is wrong (security). Log attempt count for brute-force monitoring.

---

### ERR-AUTH-002 — Session expired

**Trigger:** JWT/session token expired mid-session
**Heading:** `Session expired`
**Body:** `You have been signed out due to inactivity. Sign in again to continue.`
**CTA:** `Sign in`
**Internal note:** Preserve the current URL so the user is redirected back after sign-in.

---

### ERR-AUTH-003 — Account not found

**Trigger:** Email entered during sign-in does not match any account
**Heading:** `No account found`
**Body:** `There is no account linked to that email address. Check the address or join via your club's invitation code.`
**Internal note:** Same presentation as ERR-AUTH-001 to prevent email enumeration. Display this only after a link from an invitation email — otherwise display AUTH-001.

---

### ERR-AUTH-004 — Invitation code invalid or expired

**Trigger:** User enters an invalid invitation code during join flow
**Heading:** `Invitation code not recognised`
**Body:** `The code entered does not match any active invitation. Codes expire after 7 days. Ask your Club Administrator for a new one.`
**Field-level:** `Code not recognised. Ask your Club Administrator for a new code.`

---

## Date validation errors

### ERR-DATE-001 — Date field empty

**Heading:** `Date is required`
**Field-level:** `Enter a date.`
**Body:** `The date field needs a value. Use the format Saturday 12 July.`

---

### ERR-DATE-002 — Date format unrecognised

**Heading:** `Date format not recognised`
**Field-level:** `Use the format Saturday 12 July.`
**Body:** `The date format is not recognised. Use the format Saturday 12 July.`

---

### ERR-DATE-003 — Date is in the past

**Heading:** `Date is in the past`
**Field-level:** `Choose a future date.`
**Body:** `The date entered has already passed. Choose a future date.`

---

### ERR-DATE-004 — Date outside season

**Heading:** `Date is outside the playing season`
**Field-level:** `Dates must fall within the playing season (April to September).`
**Body:** `The date entered falls outside the playing season. Cricket fixtures are available from April to September.`
**Internal note:** Validate against configurable season window, not hardcoded months.

---

### ERR-DATE-005 — Date conflict (existing fixture)

**Heading:** `Date conflict`
**Field-level:** `This team already has a fixture on {conflicting_date}.`
**Body:** `{team_name} already has a confirmed fixture on {conflicting_date}. Choose a different date.`

---

## Form validation errors

### ERR-FORM-001 — Required field missing

**Field-level:** `This field is required.`
**Notes:** Generic fallback only. Prefer specific errors like ERR-DATE-001 where possible.

---

### ERR-FORM-002 — Field too long

**Field-level:** `This field cannot be longer than {max_chars} characters. Remove {over_count} characters.`

---

### ERR-FORM-003 — Email address format invalid

**Field-level:** `Enter a valid email address.`
**Body:** `The email address format is not valid. It should look like: name@example.com.`

---

## Fixture errors

### ERR-FIXT-001 — Fixture not found

**Heading:** `Fixture not found`
**Body:** `This fixture does not exist or has been removed. Return to your fixture list.`
**CTA:** `My fixtures`
**HTTP:** 404

---

### ERR-FIXT-002 — Cannot cancel confirmed fixture (within 48 hours)

**Heading:** `Short-notice cancellation`
**Body:** `Cancelling a fixture within 48 hours of the match date will be recorded on your club's trust record. Do you want to continue?`
**CTA primary:** `Cancel fixture`
**CTA secondary:** `Keep fixture`
**Internal note:** This is a confirmation warning, not a block. The user can still proceed. Record the cancellation type as short-notice regardless.

---

### ERR-FIXT-003 — Cannot cancel completed fixture

**Heading:** `Fixture already completed`
**Body:** `This fixture has been marked as completed and cannot be cancelled.`

---

### ERR-FIXT-004 — Cannot cancel cancelled fixture

**Heading:** `Fixture already cancelled`
**Body:** `This fixture has already been cancelled.`

---

### ERR-FIXT-005 — No edit permission

**Heading:** `You do not have permission to edit this fixture`
**Body:** `Only the fixture manager for {team_name} can edit this fixture. If you believe this is incorrect, contact your Club Administrator.`
**Error code for support:** `ERR-FIXT-005`

---

## Match request errors

### ERR-REQ-001 — Request already sent to this team for this date

**Heading:** `Request already sent`
**Body:** `You have already sent a match request to {team_name} for {fixture_date}. View the existing request.`
**CTA:** `View request`

---

### ERR-REQ-002 — Requesting team has date conflict

**Heading:** `Date conflict`
**Body:** `{your_team} already has a fixture on {fixture_date}. You cannot send a match request for a date that is already taken.`

---

### ERR-REQ-003 — Network error sending request

**Heading:** `Match request could not be sent`
**Body:** `The match request could not be sent. Check your connection and try again. If this continues, contact support. (ERR-REQ-003)`
**CTA:** `Try again`

---

### ERR-REQ-004 — Request expired (on view)

**Heading:** `This request has expired`
**Body:** `This match request was not answered within 7 days and has expired. No action is available.`

---

### ERR-REQ-005 — Request already accepted (race condition)

**Heading:** `Request already accepted`
**Body:** `This match request has already been accepted. View the confirmed fixture.`
**CTA:** `View fixture`

---

### ERR-REQ-006 — Request already declined

**Heading:** `Request already declined`
**Body:** `This match request has already been declined.`

---

### ERR-REQ-007 — Cannot withdraw accepted request

**Heading:** `Request already accepted`
**Body:** `This request has already been accepted and a fixture is confirmed. To cancel the fixture, go to the fixture detail page.`
**CTA:** `View fixture`

---

## Availability errors

### ERR-AVAIL-001 — Duplicate availability

**Heading:** `Availability already posted`
**Body:** `{team_name} already has availability posted for {fixture_date}. View or manage the existing availability.`
**CTA:** `View availability`

---

### ERR-AVAIL-002 — Cannot post availability when fixture confirmed

**Heading:** `Fixture already confirmed for this date`
**Body:** `{team_name} has a confirmed fixture on {fixture_date}. You cannot post availability for a date that is already taken.`

---

### ERR-AVAIL-003 — Availability not found

**Heading:** `Availability not found`
**Body:** `This availability does not exist or has been removed.`
**HTTP:** 404

---

### ERR-AVAIL-004 — Cannot remove availability with pending requests

**Heading:** `There are pending requests on this availability`
**Body:** `{count} match request is awaiting a response before this availability can be removed. Accept, decline, or wait for the requests to expire first.`

---

## Support request errors

### ERR-SUPP-001 — Umpire already assigned

**Heading:** `An umpire has already been confirmed`
**Body:** `{official_name} is already confirmed as umpire for this fixture. Remove them first before adding a different umpire.`

---

### ERR-SUPP-002 — Umpire not on roster

**Heading:** `This person is not on your roster`
**Body:** `Only umpires and scorers on your club's roster can receive support requests. Ask your Club Administrator to add them.`

---

### ERR-SUPP-003 — Support request already sent to this person

**Heading:** `Request already sent`
**Body:** `You have already sent a request to {official_name} for {fixture_date}. They have been notified and will respond.`

---

## Review errors

### ERR-REV-001 — Review window closed

**Heading:** `Review window has closed`
**Body:** `The review window for the {fixture_date} fixture closed on {window_close_date}. Reviews can no longer be submitted for this fixture.`

---

### ERR-REV-002 — Review already submitted

**Heading:** `Review already submitted`
**Body:** `You have already submitted a review for the {fixture_date} fixture.`

---

### ERR-REV-003 — Fixture not yet completed

**Heading:** `Fixture not yet completed`
**Body:** `Reviews can only be submitted for completed fixtures.`

---

## Permission errors

### ERR-PERM-001 — Requires Club Administrator access

**Heading:** `Club Administrator access required`
**Body:** `This action requires Club Administrator access. Contact your Club Administrator.`

---

### ERR-PERM-002 — Not a member of this club

**Heading:** `Access not permitted`
**Body:** `You do not have permission to view or edit this. If you believe this is incorrect, contact your Club Administrator. (ERR-PERM-002)`

---

### ERR-PERM-003 — Cannot act on behalf of another team

**Heading:** `Wrong team context`
**Body:** `You are currently acting as {current_team}. Switch to the correct team to take this action.`

---

## Network and server errors

### ERR-NET-001 — No connection

**Heading:** `No internet connection`
**Body:** `The action could not be completed. Check your connection and try again.`
**CTA:** `Try again`

---

### ERR-SRV-500 — Server error

**Heading:** `Something went wrong on our end`
**Body:** `The request could not be completed due to a server error. Try again in a moment. If this continues, contact support with reference ERR-SRV-500.`
**CTA:** `Try again`
**Internal note:** Log with trace ID. Display generic message; do not expose stack traces or internal detail.

---

### ERR-SRV-503 — Service unavailable

**Heading:** `Service temporarily unavailable`
**Body:** `The service is temporarily unavailable. Try again in a few minutes. (ERR-SRV-503)`
**CTA:** `Try again`

---

### ERR-SRV-404 — Page not found

**Heading:** `Page not found`
**Body:** `The page you are looking for does not exist or has been moved.`
**CTA:** `Go to dashboard`

---

## Club and team management errors

### ERR-CLUB-001 — Club name already taken

**Field-level:** `This club name is already registered. If your club is already on the platform, ask your Club Administrator for an invitation.`

---

### ERR-CLUB-002 — Team name required

**Field-level:** `Enter a team name. Use standard format: 1st XI, 2nd XI, Sunday XI.`

---

### ERR-CLUB-003 — Cannot delete team with active fixtures

**Heading:** `Team has active fixtures`
**Body:** `{team_name} has active fixtures and cannot be removed. Cancel or complete all fixtures before removing the team.`

---

## Error code registry note

A full registry of error codes with internal details is maintained by Agent 9 in the engineering outputs. This document provides the user-facing copy; Agent 9 provides the technical implementation. The two must stay in sync.

If a new error condition is discovered during development that has no copy here, Agent 9 should raise it with Agent 8 before shipping a generic fallback.

---

*Maintained by: Agent 8 (Content & Microcopy)*
*Implementation: Agent 9 (Engineering)*
