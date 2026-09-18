# Event Table Planner — Remote Staging TEST_REPORT

Checkpoint: 2026-09-18

## External browser

- GitHub Pages R6 render: **PASS**
- R6 build label visible: **PASS**
- Sign-in form visible: **PASS**
- No raw HTML / blank screen: **PASS**
- No visible JS/module load error: **PASS**
- Guest Portal route published: **PASS**
- Guest Portal invalid/no-token state renders without exposing guest data: **PASS**

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

## Concurrency / atomicity

- Different Guest fields merge with independent field versions: **PASS**
- Same-field stale Guest write rejected with 40001: **PASS**
- First seating move increments assignment revision: **PASS**
- Stale seating move rejected and first result preserved: **PASS**
- Atomic two-step party check-in preserved; arrival version increments: **PASS**
- Publish revision increments atomically: **PASS**
- Stale Publish revision rejected: **PASS**
- Floor Plan lease blocks second Organizer: **PASS**
- Lease renewal / release / takeover: **PASS**
- Organizer position write without lease denied: **PASS**
- Organizer position write with lease succeeds: **PASS**
- Stale position write denied: **PASS**
- Reception position write denied: **PASS**
- Reception table metadata write succeeds: **PASS**

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

After all transaction probes:
- Tables: **20**
- Guests: **0**
- Memberships: **1 Organizer**
- Active leases: **0**
- Publications: **0**
- Seating stage: **draft**
- Publish revision: **0**
- Table 1 restored: name `主家 1`, capacity 12, position 145/235

## Not yet tested

- Four independent real browser accounts simultaneously.
- Real simultaneous two-connection write race.
- Weak-network / offline / Realtime reconnect.
- Canonical V0.28 final UI on deployed origin.
