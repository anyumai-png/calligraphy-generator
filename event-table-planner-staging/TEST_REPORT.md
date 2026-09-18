# Event Table Planner — Remote Staging TEST_REPORT

Checkpoint: 2026-09-18

## External deployed browser

- GitHub Pages R6 render: **PASS**
- GitHub Pages R7 render / reconnect-state shell: **PASS**
- GitHub Pages R8 workflow: **SUCCESS**
- Deployed build identity `.build = R8 · GitHub Pages`: **PASS**
- R8 sign-in UI render: **PASS**
- No raw HTML / blank screen: **PASS**
- No visible JS/module load error: **PASS**
- Stale/offline banner hidden on healthy signed-out load: **PASS**
- Deployed R8 static DOM contains Overview / Floor / Guests / Reception / Admin navigation: **PASS**
- Guest Portal route published: **PASS**
- Guest Portal invalid/no-token state exposes no guest data: **PASS**

## Role authorization

- Organizer team access: **PASS**
- Reception create guest: **PASS**
- Reception edit RSVP: **PASS**
- Reception seating move: **PASS**
- Reception team admin denied: **PASS**
- Floor check-in: **PASS**
- Floor guest-master edit denied: **PASS**
- Floor seating move denied: **PASS**
- Viewer event read: **PASS**
- Viewer create guest denied: **PASS**
- Viewer check-in denied: **PASS**
- Viewer guest edit denied: **PASS**

## Sequential concurrency / atomicity regression

- Different Guest fields merge with independent field versions: **PASS**
- Same-field stale Guest write rejected with 40001: **PASS**
- First seating move increments assignment revision: **PASS**
- Stale seating move rejected and first result preserved: **PASS**
- Atomic party check-in increments and arrival versions: **PASS**
- Publish revision increments atomically: **PASS**
- Stale Publish revision rejected: **PASS**
- Floor Plan lease blocks second Organizer: **PASS**
- Lease renewal / release / takeover: **PASS**
- Organizer position write without lease denied: **PASS**
- Organizer position write with lease succeeds: **PASS**
- Stale position write denied: **PASS**
- Reception position write denied: **PASS**
- Reception table metadata write succeeds: **PASS**

## True parallel two-connection race gate

Two separate Supabase calls were launched concurrently with two different user identities.

- Different Guest fields, same Guest:
  - Organizer company edit: success
  - Reception name edit: success
  - final field versions preserved independently
  - **PASS**
- Same Guest field, same expected version:
  - one success
  - one `40001 concurrent guest field update`
  - **PASS**
- Simultaneous check-in `+1 / +1`:
  - first returns arrival 1
  - second returns arrival 2
  - no lost update
  - **PASS**
- Same Guest simultaneous seating to Table 1 / Table 2:
  - one success, assignment revision 1 → 2
  - other `40001 concurrent seating update`
  - **PASS**
- Simultaneous Publish on isolated synthetic event, expected revision 0:
  - one success revision 1
  - other `40001 concurrent publish revision`
  - **PASS**
- Simultaneous Floor Plan lease acquisition:
  - one Organizer `acquired=true`
  - the other `acquired=false` and sees the first holder
  - **PASS**

## Published isolation

- Initial publish visible to Guest Portal: **PASS**
- Working unassign after publish does not leak into Guest Portal: **PASS**
- Republish updates Guest Portal: **PASS**

## Data integrity

- Guest creation resolves normalized `group_id`: **PASS**
- Group-eligible seating assignment: **PASS**
- Capacity shrink below occupied seat denied: **PASS**
- Safe capacity expansion allowed: **PASS**
- Trigger-only capacity function direct EXECUTE revoked: **PASS**

## Cleanup verification

After all probes and true race fixtures:
- Tables: **20**
- Guests: **0**
- Memberships: **1 Organizer**
- Active leases: **0**
- Publications: **0**
- Seating stage: **draft**
- Publish revision: **0**
- Synthetic concurrency event: **deleted**
- Table 1 restored: name `主家 1`, capacity 12, position 145/235

## Remaining environment tests

- Four independent real browser Auth accounts simultaneously.
- Physical phone/tablet offline / weak-network → Realtime reconnect.
- Exact canonical V0.28 final UI on deployed origin.
- Native WebMCP registration on the final canonical deployed origin.
