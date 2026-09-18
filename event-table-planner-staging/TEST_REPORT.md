# Event Table Planner — Remote Staging TEST_REPORT

Checkpoint: 2026-09-18

## Deployed-origin smoke

- R8 deployed identity / task navigation: PASS
- R9 Run workspace DOM + runtime smoke: PASS
- R10 full-field bulk import UI DOM + runtime smoke: PASS
- R11 Emergency Pack DOM + runtime smoke: PASS
- No raw HTML / blank screen / visible module errors: PASS
- Guest Portal route and invalid-token privacy state: PASS

## Authorization

- Organizer team / guest / seating / layout / Publish: PASS
- Reception guest / seating / check-in: PASS
- Reception team admin and Run-of-Show edit denied: PASS
- Floor check-in and Task operations: PASS
- Floor guest-master / seating / Run-of-Show edit denied: PASS
- Viewer read-only; guest/task mutations denied: PASS

## True parallel concurrency

- Different Guest fields simultaneously: both merge safely — PASS
- Same Guest field simultaneously: one success + one 40001 — PASS
- Simultaneous +1 / +1 arrivals: final arrival 2 — PASS
- Same Guest simultaneous seating moves: one success + one 40001 — PASS
- Simultaneous Publish revision: one success + one 40001 — PASS
- Simultaneous Floor Plan lease: one acquired + one blocked — PASS
- Parallel Task create: distinct identity IDs — PASS
- Parallel Run item create: distinct IDs + sort_order 0 / 1 — PASS

## Data / import integrity

- Full-field single-row import: PASS
- Normalized Group ID: PASS
- Duplicate Name + Company skip: PASS
- Floor bulk import denied: PASS
- 121-row structural scale import:
  - bookings 121
  - confirmed 232
  - pending 6
  - declined 4
  - normalized group rows 121
  - group counts: 主家 12 / 供應商 25 / 客戶 44 / 同事 18 / 朋友 22
  - measured DB transaction ~34.28 ms
  - PASS
- All scale/probe data rolled back or deleted.

## Other retained gates

- Guest Portal Working/Published isolation: PASS
- Table capacity shrink guard: PASS
- Floor Plan lease enforcement: PASS
- Stale position update rejection: PASS
- Atomic check-in: PASS
- Stale Publish guard: PASS
- Security Advisor anonymous definer surface: only intentional Guest Portal

## Clean-state verification

- Tables: 20
- Guests: 0
- Tasks: 0
- Run-of-Show items: 0
- Memberships: 1 Organizer
- Active leases: 0
- Publications: 0
- Stage: draft
- Publish revision: 0

## Remaining environment tests

- Four independent real browser Auth accounts.
- Real mobile/tablet network interruption and recovery.
- Exact official CSV through authenticated browser file picker.
- Exact canonical V0.28 deployed runtime.
- Native WebMCP on final canonical deployed origin.
