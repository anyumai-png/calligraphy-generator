# Event Table Planner — Remote Staging TEST_REPORT

Checkpoint: 2026-09-18

## Critical client-runtime correction

A full-source V8 parse performed on the historical staging commits found:
- R6: **PARSE PASS**
- R7: **PARSE FAIL**
- R8: **PARSE FAIL**
- R9: **PARSE FAIL**
- R10: **PARSE FAIL**
- R11: **PARSE FAIL**
- R12 / R12.1: inherited failure
- R12.2: **PARSE PASS**

Root cause: an extra closing brace after `renderNetworkState()`, introduced in R7.

Therefore all earlier R7–R12.1 browser “runtime smoke” claims are reclassified as **static HTML/deployment smoke only**. They cannot be used as proof of JavaScript execution.

## R12.2 client validation

- GitHub Pages deployment: PASS
- deployed build identity R12.2: PASS
- full module V8 parse: PASS
- Forgot Password button handler actually executes: PASS
- visible success status produced: PASS
- Supabase password recovery accepted: PASS
- `auth.users.recovery_sent_at`: populated
- recovery-link new-password screen: source implemented; end-to-end link click pending user inbox action
- authenticated Organizer UI regression: pending password reset/sign-in

## Backend authorization

These tests were executed directly against Supabase and remain valid:
- Organizer team / guest / seating / layout / Publish: PASS
- Reception guest / seating / check-in: PASS
- Reception team admin and Run-of-Show edit denied: PASS
- Floor check-in and Task operations: PASS
- Floor guest-master / seating / Run-of-Show edit denied: PASS
- Viewer read-only; guest/task mutations denied: PASS

## True parallel backend concurrency

- different Guest fields simultaneously: merge safely — PASS
- same Guest field: one success + one 40001 — PASS
- simultaneous +1 / +1 arrivals: final arrival 2 — PASS
- same Guest simultaneous seating moves: one success + one 40001 — PASS
- simultaneous Publish revision: one success + one 40001 — PASS
- simultaneous Floor Plan lease: one acquired + one blocked — PASS
- parallel Task create: distinct identity IDs — PASS
- parallel Run item create: distinct IDs + sort_order 0 / 1 — PASS

## Data / import backend integrity

- full-field single-row import: PASS
- normalized Group ID: PASS
- duplicate Name + Company skip: PASS
- Floor bulk import denied: PASS
- 121-row Supabase scale import:
  - bookings 121
  - confirmed 232
  - pending 6
  - declined 4
  - normalized group rows 121
  - group counts: 主家 12 / 供應商 25 / 客戶 44 / 同事 18 / 朋友 22
  - measured DB transaction ~34.28 ms
  - PASS

## Other backend gates

- Guest Portal Working/Published isolation: PASS
- Table capacity shrink guard: PASS
- Floor Plan lease enforcement: PASS
- stale position update rejection: PASS
- atomic check-in: PASS
- stale Publish guard: PASS
- Security Advisor anonymous definer surface: only intentional Guest Portal

## Clean business-data state

- Tables: 20
- Guests: 0
- Tasks: 0
- Run-of-Show items: 0
- Memberships: 1 Organizer
- Active leases: 0
- Publications: 0
- Stage: draft
- Publish revision: 0

## Remaining client/environment tests

- click newest recovery email link, set new password, then sign in
- authenticated Organizer R12.2 browser UAT
- four independent real browser Auth accounts
- real mobile/tablet offline → reconnect
- exact official CSV through authenticated browser file picker
- exact canonical V0.28 deployed runtime
- native WebMCP on final canonical deployed origin
