# Event Table Planner — Remote Staging STATUS

Checkpoint: 2026-09-18

> This directory is the temporary remote-staging host and checkpoint, not the canonical V0.28 product repository. The canonical final V0.28 runtime bundle is still not available through the connected GitHub repositories.

## Current state

- Remote console build: **R6**
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

- Email/password sign-in
- First Organizer claim
- Staging team role assignment
- Organizer / Reception / Floor / Viewer role surfaces
- 20-table status dashboard
- Normalized guest groups + table-group eligibility
- Add Guest
- CSV Guest import
- RSVP edit with field-version concurrency
- Atomic check-in +/-
- Working seating assignment with revision guard
- Human-confirmed Publish
- Published-only Guest Portal links
- Editable Floor Plan with Organizer edit lease and pointer/touch drag
- Table Maintenance: name, zone, capacity, color
- Realtime refresh for guests, tables, memberships

## Last completed loop

R6 Table Maintenance + server-side capacity guard + Floor Plan lease enforcement.

## Next highest-priority work

1. Real four-account UAT with separate Owner/Organizer, Reception, Floor, Viewer sessions.
2. True simultaneous two-browser race tests.
3. Realtime reconnect / weak-network recovery.
4. Recover or reconnect the canonical V0.28 runtime repository and upstream all staging-proven migrations.
5. Replace temporary GitHub Pages staging shell with the canonical V0.28 visual UI.
