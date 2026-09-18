# Event Table Planner — Remote Staging STATUS

Checkpoint: 2026-09-18

> This directory is the temporary remote-staging host and checkpoint, not the canonical V0.28 product repository. The canonical final V0.28 `index.html` has been recovered from File Library evidence, but the exact final `app.js / styles.css / event-core.js / webmcp.js` bundle is still not available through the connected repository or File Library search. Do not mix older runtime files into V0.28.

## Current state

- Remote console build: **R8**
- R8 commit: `bf4934167a3a64d529edd24b71ba1eb76f61a5d5`
- GitHub Pages deployment workflow: **SUCCESS**
- Product baseline: **V0.28 — Final Production Candidate**
- Hosting: GitHub Pages
- Console: https://anyumai-png.github.io/calligraphy-generator/event-table-planner-staging/
- Guest Portal: https://anyumai-png.github.io/calligraphy-generator/event-table-planner-staging/guest/
- Backend: Supabase staging project `vdmnfzrwxtvscutqozmx`
- Event: `Annual Dinner 2026 — STAGING`
- Tables: **20**
- Guests: **0**
- Memberships: **1 Organizer**
- Seating stage: **draft**
- Publish revision: **0**
- Active edit leases: **0**
- Publications: **0**

## Remote capabilities

- Email/password sign-in and first Organizer claim
- Team role assignment
- Organizer / Reception / Floor / Viewer role boundaries
- Role-aware task views: Overview / Floor / Guests / Reception / Admin
- 20-table dashboard and real-coordinate Floor Plan
- Organizer edit lease + touch/pointer drag
- Server-side lease enforcement for layout writes
- Table Maintenance: name, zone, capacity, color
- Capacity guard against occupied Working / Published seats
- Normalized Guest Groups and table eligibility
- Add Guest and CSV import
- RSVP edit with field-version concurrency
- Atomic check-in +/-
- Working seating move with revision guard
- Human-confirmed atomic Publish
- Published-only Guest Portal and guest links
- Realtime updates
- R7 network resilience: stale-data state, reconnect backoff, foreground refresh, mutation stale guard, layout edit pause on disconnect

## Verified external environment gates

- GitHub Pages deployed-origin rendering: **PASS**
- R8 deployed build identity: **PASS**
- Guest Portal route: **PASS**
- Core two-identity / two-connection DB race tests: **PASS**
  - different-field Guest edits
  - same-field Guest conflict
  - simultaneous check-in increments
  - simultaneous same-Guest seating moves
  - simultaneous Publish
  - simultaneous Floor Plan lease acquisition

## Last completed loop

R8 task-oriented operations UI + true parallel Supabase concurrency gate.

## Next highest-priority work

1. Four independent real browser Auth personas: Organizer / Reception / Floor / Viewer.
2. Physical weak-network/offline → reconnect UAT on phone/tablet.
3. Recover/reconnect the exact canonical V0.28 runtime bundle and upstream staging-proven migrations/hotfixes.
4. Replace the temporary staging shell with the canonical V0.28 visual UI.
5. Final native WebMCP deployed-origin validation after canonical runtime recovery.
