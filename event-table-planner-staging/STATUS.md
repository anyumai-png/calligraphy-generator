# Event Table Planner — Remote Staging STATUS

Checkpoint: 2026-09-18

> Temporary remote-staging host/checkpoint only. It is not the canonical V0.28 repository. Final V0.28 `index.html` and final UAT evidence are recoverable, but the exact final `app.js / styles.css / event-core.js / webmcp.js` bundle is still unavailable. Older runtime files must not be mixed into V0.28.

## Current state

- Remote console: **R11**
- R11 commit: `e772192348cdec76da1cee833f43119c75030e4b`
- Product baseline: **V0.28 — Final Production Candidate**
- Console: https://anyumai-png.github.io/calligraphy-generator/event-table-planner-staging/
- Guest Portal: https://anyumai-png.github.io/calligraphy-generator/event-table-planner-staging/guest/
- Backend: Supabase staging `vdmnfzrwxtvscutqozmx`
- Event: `Annual Dinner 2026 — STAGING`
- Clean checkpoint: **20 Tables / 0 Guests / 0 Tasks / 0 Run items / 1 Organizer / 0 leases / 0 publications**
- Seating stage: **draft**
- Publish revision: **0**

## Remote capabilities

- Role-aware views: Overview / Floor / Guests / Reception / Run / Admin
- Organizer / Reception / Floor / Viewer authorization surfaces
- Guest creation and full-field transactional CSV bulk import
- Normalized Guest Groups + table-group eligibility
- RSVP / atomic check-in / concurrency-safe Working seating
- Editable real-coordinate Floor Plan with server-enforced Organizer lease
- Table Maintenance with occupied-seat capacity guard
- Human-confirmed atomic Publish
- Published-only Guest Portal
- Event Tasks + Run of Show with role-based writes and Realtime updates
- R7 stale/offline state machine, channel rebuild and stale-mutation guard
- Emergency Pack: Guest CSV, Table CSV and printable snapshot
- CSV formula-injection mitigation on Emergency Pack exports

## Verified gates

- GitHub Pages deployed origin: **PASS**
- R11 deployed build identity + external browser smoke: **PASS**
- Official-scale structural import: **121 bookings / 232 confirmed / 6 pending / 4 declined**
- Bulk import database execution: **~34.28 ms** in the measured staging transaction
- True parallel two-identity races: **PASS**
- Task identity concurrency: **PASS**
- Run-of-Show identity + serialized sort order: **PASS (0 / 1)**

## Remaining highest-priority gates

1. Four independent real browser Auth personas.
2. Real phone/tablet network interruption → reconnect UAT.
3. Actual browser file-picker import of the official 121-booking CSV.
4. Recover/reconnect exact canonical V0.28 runtime and upstream all staging-proven changes.
5. Native WebMCP final-origin validation on the canonical build.
