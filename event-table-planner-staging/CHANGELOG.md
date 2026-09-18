# Event Table Planner — Remote Staging CHANGELOG

## 2026-09-18 — R8

- Reworked the temporary console into role-aware task views:
  - Overview
  - Floor
  - Guests
  - Reception
  - Admin
- Added role-specific allowed/default views.
- Added URL hash persistence with `#view=...`.
- Added Unassigned and Pending overview metrics.
- Reception view focuses confirmed guests and check-in, removing seating/admin clutter.
- GitHub Pages workflow for R8 completed successfully.
- Deployed `.build` identity verified as **R8 · GitHub Pages**.
- Static deployed DOM verified to contain all five operations navigation buttons.

### True parallel concurrency gate

Used two independent Supabase connection calls and two different user identities.

- Different Guest fields updated concurrently: both succeed and merge.
- Same Guest field updated concurrently: one succeeds; the other receives `40001 concurrent guest field update`.
- Two simultaneous arrival increments: final arrival count is 2 with no lost update.
- Same Guest simultaneously moved to two different Tables: one succeeds; the other receives `40001 concurrent seating update`.
- Two Organizers publish the same expected revision concurrently: one succeeds; the other receives `40001 concurrent publish revision`.
- Two Organizers acquire the same Floor Plan lease concurrently: one `acquired=true`, the other `acquired=false`.

All race fixtures and the isolated synthetic event were deleted after validation.

## R7

- Added explicit stale/offline state instead of pretending the last snapshot is live.
- Preserves the last confirmed data on transient fetch failures.
- Added exponential reconnect/backoff.
- Rebuilds failed Realtime channels rather than only changing the status dot.
- Added online/offline event handling.
- Added foreground refresh after returning to the tab/app.
- Critical mutations revalidate data if the last confirmed load is stale.
- Floor Plan editing is paused if connection confidence is lost.
- External R7 browser smoke PASS.

## R6

- Added Table Maintenance for Organizer / Reception.
- Table number remains read-only in the temporary console.
- Added server-side guard preventing capacity from being reduced below occupied working or published seat numbers.
- Revoked direct API execution on the trigger-only capacity guard function.
- External GitHub Pages R6 smoke test PASS.

## R5

- Added real-coordinate Floor Plan using the 20-table staging layout.
- Added Organizer-only Edit Layout flow.
- Added `floor_plan` edit lease acquisition, renewal and release.
- Added pointer/touch drag with field-version guarded position writes.
- Added server-side enforcement: position/rotation changes require Organizer + active floor-plan lease.
- Verified Reception can maintain table metadata but cannot change floor coordinates.

## R4

- Added human-confirmed Publish action.
- Added Guest Portal link generation.
- Added public Published-only Guest Portal page under `/guest/`.
- Added noindex/nofollow to staging pages.
- Verified Working seating changes do not leak to Guest Portal until republish.

## R3

- Normalized guest creation to `guest_groups.group_id`.
- Replaced free-text Add Guest group with configured groups.
- CSV import validates configured groups.
- Seating dropdown filters to group-eligible tables.
- Fixed unassignable-guest defect caused by text-only guest groups.

## R2

- Added correct access-pending state.
- Added Team / Staging Access role management.
- Added CSV guest import.
- Added RSVP edit and check-in decrement.
- Added mobile action bar.
- Fixed first Organizer claim ambiguity.
- Fixed Floor check-in trigger conflict with arrival field-version bookkeeping.

## Earlier staging hardening

- Created live Supabase staging project and 20-table fixture.
- Applied the required V0.8 → V0.26.2 database evolution.
- Post-migration structural gate 22/22 PASS.
- Fixed anonymous EXECUTE exposure on operational SECURITY DEFINER RPCs.
- Removed legacy deterministic Guest Portal token lookup.
- Added UUID Guest Portal lookup index.
- Removed duplicate permissive RLS policy warnings.
