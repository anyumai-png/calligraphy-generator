# Event Table Planner — Remote Staging STATUS

Checkpoint: 2026-09-18

> Temporary remote-staging host/checkpoint only. It is not the canonical V0.28 repository. Final V0.28 `index.html` and final UAT evidence are recoverable, but the exact final `app.js / styles.css / event-core.js / webmcp.js` bundle is still unavailable. Older runtime files must not be mixed into V0.28.

## Current state

- Remote console: **R12.2**
- R12.2 commit: `94f75d958e1445180b3e7815fa2bf1243cd80fee`
- Product baseline: **V0.28 — Final Production Candidate**
- Console: https://anyumai-png.github.io/calligraphy-generator/event-table-planner-staging/
- Guest Portal: https://anyumai-png.github.io/calligraphy-generator/event-table-planner-staging/guest/
- Backend: Supabase staging `vdmnfzrwxtvscutqozmx`
- Event: `Annual Dinner 2026 — STAGING`
- Clean business-data checkpoint: **20 Tables / 0 Guests / 0 Tasks / 0 Run items / 1 Organizer / 0 leases / 0 publications**
- Seating stage: **draft**
- Publish revision: **0**
- Organizer account: confirmed; password-recovery email successfully requested on 2026-09-18.

## Critical regression corrected in R12.2

R7 introduced an extra closing brace after `renderNetworkState()`. The static page continued to render, but the module script did not parse. R8–R12.1 inherited the same defect.

R12.2:
- removes the extra brace;
- runs a full V8 parse gate over the entire module before commit;
- passes the parse gate;
- proves actual client JavaScript execution through the Forgot Password flow;
- successfully sends a Supabase password-recovery request and updates `auth.users.recovery_sent_at`.

Previous R7–R12.1 “runtime smoke” records must be interpreted as **static HTML/deployment smoke only**, not JavaScript runtime validation.

## Remote capabilities present in the R12.2 source

- Role-aware views: Overview / Floor / Guests / Reception / Run / Admin
- Organizer / Reception / Floor / Viewer authorization surfaces
- Guest creation and full-field transactional CSV bulk import
- Normalized Guest Groups + table-group eligibility
- RSVP / atomic check-in / concurrency-safe Working seating
- Editable Floor Plan with server-enforced Organizer lease
- Table Maintenance with occupied-seat capacity guard
- Human-confirmed atomic Publish
- Published-only Guest Portal
- Event Tasks + Run of Show
- R7 reconnect/stale-data logic
- Emergency Pack exports
- Password recovery and in-browser new-password flow

## Verified gates that remain valid

Backend/database tests were not affected by the client syntax defect:
- official-scale structural import: **121 bookings / 232 confirmed / 6 pending / 4 declined**
- measured bulk import DB execution: **~34.28 ms**
- true parallel two-identity races: **PASS**
- Task identity concurrency: **PASS**
- Run-of-Show identity + serialized sort order: **PASS (0 / 1)**
- RLS / authoritative RPC role tests: **PASS**
- Security Advisor anonymous surface: only intentional Guest Portal

Client/deployment:
- R12.2 GitHub Pages deployment: **PASS**
- full module V8 parse: **PASS**
- Forgot Password handler real execution: **PASS**
- Supabase recovery request recorded: **PASS**

## Highest-priority next gates

1. Complete password reset from the emailed recovery link and sign in with the new password.
2. Re-run authenticated browser UAT on R12.2 for Organizer views and mutations.
3. Four independent real browser Auth personas.
4. Real phone/tablet network interruption → reconnect UAT.
5. Actual browser file-picker import of the official 121-booking CSV.
6. Recover/reconnect exact canonical V0.28 runtime and upstream all staging-proven changes.
7. Native WebMCP final-origin validation on the canonical build.
