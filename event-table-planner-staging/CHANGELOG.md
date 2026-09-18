# Event Table Planner — Remote Staging CHANGELOG

## 2026-09-18 — R12.2

- Found and fixed a critical client module syntax regression first introduced in R7.
- Root cause: an extra closing brace after `renderNetworkState()`.
- R7, R8, R9, R10, R11, R12 and R12.1 inherited the malformed module.
- Static HTML still rendered, which caused earlier visual smoke tests to overstate runtime health.
- Added an explicit V8 parse gate against the full module before commit.
- Full R12.2 module parse: PASS.
- Added/retained standard Supabase Password Recovery:
  - Forgot Password
  - recovery-link `PASSWORD_RECOVERY` state
  - in-browser Set New Password
  - sign out after password update
- Added reset-request timeout and visible exception handling.
- Actual Forgot Password JavaScript handler execution verified.
- Supabase `auth.users.recovery_sent_at` updated, proving the recovery request was accepted.

### Test-record correction

Earlier R7–R12.1 “runtime smoke PASS” entries are reclassified as **static page/deployment smoke only**. They do not prove module JavaScript execution. Backend/RPC/database tests from those rounds remain valid because they were executed independently of the browser module.

## R11

- Added Emergency Pack source functionality: Guests CSV, Tables CSV and printable snapshot.
- Added CSV formula-injection mitigation.
- Historical note: deployment/static DOM was verified, but JavaScript runtime execution was not valid until the R12.2 syntax repair.

## R10

- Replaced per-row CSV import source path with one transactional JSON RPC.
- Added canonical CSV fields.
- 121-row real Supabase backend scale regression passed.
- Historical note: browser static DOM was verified; authenticated client execution requires revalidation on R12.2.

## R9

- Added Run view, Event Tasks and Run of Show source functionality.
- Backend role/RPC and parallel-ID tests passed independently.
- Historical browser runtime claim superseded by R12.2 correction.

## R8

- Added role-aware task views.
- Backend true-parallel race suite passed independently.
- Historical browser runtime claim superseded by R12.2 correction.

## R7

- Added reconnect/stale-data source logic.
- Introduced the extra-brace syntax defect later fixed by R12.2.

## R6 and earlier

- R6 is the last pre-regression client version confirmed to parse before the R7 change.
- Table Maintenance with capacity guard.
- Server-enforced Floor Plan lease.
- Published-only Guest Portal.
- Normalized Guest Groups.
- Team role management.
- Live Supabase staging migration chain and 22/22 structural verification.
