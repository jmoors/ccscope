# 02 — Roles and Permissions Matrix

**Version:** 1.0  
**Date:** 2026-04-19  
**Owner:** Agent 2 (Domain Model & Logic)  
**Status:** Draft — awaiting Agent 9 review

---

## 1. Role Definitions

### Club Admin

Manages the club's organisational record. Responsible for the club profile, venue list, and team roster. Authorises who holds the Fixture Manager role on each team. In small clubs, this person often also holds the Fixture Manager role on one or more teams.

**Scope:** Club-wide (all teams within the club)

---

### Fixture Manager

The person who arranges matches for a specific team. Searches for opponents, posts availability, sends and receives match requests, confirms fixtures, and marks them complete. Submits post-match trust reviews.

**Scope:** Team-specific. A person may hold this role on multiple teams (e.g., a Club Secretary managing the 1st and 2nd XI).

---

### Captain

Plays and leads on the day. In the MVP, the Captain has a read-only view of fixtures and can be delegated specific actions by the Fixture Manager (see §4 on delegation). Does not independently post availability or send match requests.

**Scope:** Team-specific.

---

### Service Provider

An umpire or scorer on a club's roster (v1: club roster only, not open marketplace). Receives support requests, accepts or declines. Has no access to fixture management outside their own requests.

**Scope:** Operates within one or more clubs' rosters.

---

### Platform User (authenticated, no team role)

A registered user who has not been assigned to a team or club role. Can browse public availability but cannot send match requests, post availability, or submit reviews. This state is transitional; a new user is expected to join a club or have their Club Admin assign them a role.

**Scope:** Read-only on public content.

---

## 2. Multi-Role Cases

### One person, multiple teams

A person (e.g., a Club Secretary) holds Fixture Manager for both the 1st XI and 2nd XI. This is represented as two separate `UserRole` records, one per team. Their permissions apply per-team context:

- When acting on a 1st XI fixture, they have Fixture Manager permissions for the 1st XI.
- When acting on a 2nd XI fixture, they have Fixture Manager permissions for the 2nd XI.
- They cannot act on behalf of another club's team.

The UI should require explicit context-switching when a user has roles on multiple teams, so they are always clear which team they are acting for.

### Club Admin who is also Fixture Manager

Represented as two concurrent roles: `club_admin` and `fixture_manager` on a specific team. Club Admin permissions apply across the whole club; Fixture Manager permissions apply per team. No special compound permission is created — permissions are additive.

### Fixture Manager who is also Captain

Permitted. The Fixture Manager role subsumes the Captain's fixture-viewing permissions. The Captain delegate action is therefore moot when the Captain is also the Fixture Manager.

### Service Provider who is also a player

A club's umpire may also be a registered player. These roles coexist. Umpire-role permissions apply when acting on support requests; player status has no system-level permissions in MVP.

---

## 3. Permission Matrix

Columns: **FM** = Fixture Manager | **CA** = Club Admin | **Cap** = Captain | **SP** = Service Provider | **PU** = Platform User

A "✓" means the role can perform this action. A "D" means allowed only when delegated by FM. A "✗" means not permitted.

### Availability

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| Publish availability | ✓ | ✗ | D | ✗ | ✗ |
| Withdraw availability | ✓ | ✗ | D | ✗ | ✗ |
| View own team's availability | ✓ | ✓ | ✓ | ✗ | ✗ |
| Search others' availability | ✓ | ✓ | D | ✗ | ✗ |

### Match Requests

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| Send match request | ✓ | ✗ | D | ✗ | ✗ |
| Accept match request | ✓ | ✗ | D | ✗ | ✗ |
| Decline match request | ✓ | ✗ | D | ✗ | ✗ |
| Withdraw sent match request | ✓ | ✗ | ✗ | ✗ | ✗ |

### Fixtures

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| View fixture detail | ✓ | ✓ | ✓ | ✓ (own) | ✗ |
| Confirm venue | ✓ | ✓ | ✗ | ✗ | ✗ |
| Mark fixture complete | ✓ | ✗ | D | ✗ | ✗ |
| Cancel fixture (> 48h notice) | ✓ | ✓ | ✗ | ✗ | ✗ |
| Cancel fixture (< 48h notice) | ✓ | ✓ | ✗ | ✗ | ✗ |
| Mark weather cancellation | ✓ | ✓ | D | ✗ | ✗ |

### Club and Team Management

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| Edit club profile | ✗ | ✓ | ✗ | ✗ | ✗ |
| Add / edit team | ✗ | ✓ | ✗ | ✗ | ✗ |
| Assign Fixture Manager role | ✗ | ✓ | ✗ | ✗ | ✗ |
| Assign Captain role | ✗ | ✓ | ✗ | ✗ | ✗ |
| Add umpire to club roster | ✗ | ✓ | ✗ | ✗ | ✗ |
| View own club's roster | ✓ | ✓ | ✓ | ✗ | ✗ |

### Trust Reviews

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| Submit post-match review | ✓ | ✗ | ✗ | ✗ | ✗ |
| View own team's received reviews (aggregate) | ✗ | ✓ | ✗ | ✗ | ✗ |
| View own team's trust badge | ✓ | ✓ | ✓ | ✗ | ✓ |
| View another team's trust badge | ✓ | ✓ | ✓ | ✗ | ✓ |
| View internal "Needs attention" flag | ✗ | ✗ | ✗ | ✗ | ✗ |

Reviews are private. The submitting FM cannot see the receiving team's individual review. Aggregate trust badge is public.

### Blocking

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| Block another club | ✓ | ✓ | ✗ | ✗ | ✗ |
| Remove a block | ✓ | ✓ | ✗ | ✗ | ✗ |
| View own blocks | ✓ | ✓ | ✗ | ✗ | ✗ |

Blocks are silent (blocked club not notified). See `07-edge-cases.md` for full block behaviour.

### Support Requests (Umpires / Scorers)

| Action | FM | CA | Cap | SP | PU |
|---|:---:|:---:|:---:|:---:|:---:|
| Send support request to rostered umpire | ✓ | ✗ | ✗ | ✗ | ✗ |
| Accept support request | ✗ | ✗ | ✗ | ✓ | ✗ |
| Decline support request | ✗ | ✗ | ✗ | ✓ | ✗ |
| View own club's rostered service providers | ✓ | ✓ | ✗ | ✗ | ✗ |

---

## 4. Delegation Rules

The Fixture Manager may delegate specific actions to the Captain. Delegation is explicit and per-fixture (not blanket). Delegation is recorded on the fixture record.

**Delegatable actions:**
- Accept / decline a match request
- Mark a fixture complete
- Mark a weather cancellation

**Non-delegatable actions (FM only):**
- Publish or withdraw availability
- Send a match request
- Cancel a fixture
- Submit a post-match review
- Block another club

**Mechanics:**
- FM creates a delegation record: `{fixture_id, delegated_to_user_id, action, expires_at}`
- If the FM does not act within `expires_at`, the Captain may act.
- FM can revoke delegation at any time before the Captain acts.
- A Captain cannot further sub-delegate.

**Why these constraints:**  
Availability and match requests carry trust implications. Blocks have privacy implications. Reviews must come from the person who managed the fixture. These cannot be safely delegated without introducing accountability gaps.

---

## 5. Edge Cases in Role Assignment

### Fixture Manager leaves club mid-season

Covered in `07-edge-cases.md`. Short version: Club Admin must reassign the Fixture Manager role. Fixtures in active states remain in those states; a grace period of 7 days is given for the Club Admin to reassign. After 7 days without reassignment, active match requests expire normally; confirmed fixtures remain confirmed. Neither the vacant FM role nor the Club Admin inherit FM action permissions automatically.

### Club has no Club Admin assigned

This should not be possible post-onboarding. The onboarding flow requires at least one user to be assigned Club Admin before the club profile is published. If a Club Admin's account is deleted, a platform-level admin must manually reassign the role. No automated fallback.

### Sole Fixture Manager is also Club Admin

Permitted. Common in small clubs. The same user holds both roles. All permissions are available. No conflict.

### A user requests to join a club without invitation

Outside MVP scope. In v1, users are added to club rosters by Club Admins only. There is no self-service join flow.
