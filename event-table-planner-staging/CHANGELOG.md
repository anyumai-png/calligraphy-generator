# Event Table Planner — Remote Staging CHANGELOG

## 2026-09-18 — R11

- Added human-triggered Emergency Pack from the last confirmed in-browser snapshot.
- Added Guests CSV and Tables CSV download.
- Added printable event pack with summary + guest seating/check-in data.
- Export is restricted to Owner / Organizer / Reception.
- No permanent local guest-data cache is created by this feature.
- Added CSV formula-injection mitigation for values beginning with =, +, - or @.
- R11 GitHub Pages deployment and external runtime smoke: PASS.

## R10

- Replaced per-row CSV import with one transactional JSON RPC.
- Added canonical CSV fields: Name, Company, Group, Title, Party Size, Companion Label, Principal / 主角, VIP, Dietary, RSVP, Invitation, Notes.
- Added server-side normalized Group resolution.
- Exact Name + Company duplicates are skipped server-side.
- Import is limited to 500 rows per transaction.
- Floor cannot bulk import.
- 121-row structural scale regression:
  - 121 bookings
  - 232 confirmed people
  - 6 pending
  - 4 declined
  - 121 normalized group IDs
  - measured DB execution ~34.28 ms
- R10 deployed runtime smoke: PASS.

## R9

- Added Run work view.
- Added Event Tasks board.
- Added Run of Show timeline.
- Organizer / Reception / Floor may create/update Tasks; Viewer read-only.
- Organizer / Owner controls Run of Show.
- Added task/run Realtime subscriptions.
- Added authoritative staging RPCs for Task create/status and Run item create.
- Corrected initial assumption about IDs: both tables use GENERATED ALWAYS identity.
- Parallel Task create generated distinct IDs.
- Parallel Run item create generated distinct IDs and serialized sort_order 0 / 1.
- R9 deployed runtime smoke: PASS.

## R8

- Added role-aware task views: Overview / Floor / Guests / Reception / Admin.
- Reception view focuses confirmed guests and arrivals.
- Added URL hash view persistence.
- Added Unassigned and Pending metrics.
- True parallel Supabase race suite passed for Guest fields, check-in, seating, Publish and Floor Plan lease.

## R7

- Added explicit stale/offline state.
- Added reconnect backoff, channel rebuilding, online/offline handling and foreground refresh.
- Mutations revalidate stale snapshots before consequential writes.
- Floor Plan editing pauses when connection confidence is lost.

## R6 and earlier

- Table Maintenance with capacity guard.
- Server-enforced Floor Plan lease.
- Published-only Guest Portal.
- Normalized Guest Groups.
- Team role management.
- Live Supabase staging migration chain and 22/22 structural verification.
- Anonymous EXECUTE hardening; only intentional anonymous RPC is `get_guest_portal`.
