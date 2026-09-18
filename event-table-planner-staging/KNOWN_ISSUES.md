# Event Table Planner — Remote Staging KNOWN_ISSUES

## Remaining environment / release gates

1. **Authenticated browser UAT must be repeated on R12.2**
   - R7–R12.1 static HTML rendered while the module contained a syntax error.
   - Backend/RPC tests remain valid.
   - Authenticated UI workflows must now be re-exercised on the fixed R12.2 client.

2. **Exact canonical V0.28 runtime bundle is not connected**
   - Final V0.28 HTML/UAT evidence exists.
   - Exact final `app.js / styles.css / event-core.js / webmcp.js` are still unavailable.
   - Remote R12.2 is a temporary operations shell, not the final V0.28 visual UI.

3. **Four real Auth personas are not yet exercised in independent browsers**
   - One confirmed Organizer account exists.
   - Reception / Floor / Viewer are backend/RPC verified with independent identity contexts.
   - Core true-parallel two-identity races pass.

4. **Physical network interruption UAT remains**
   - R7 reconnect/stale-state source logic is present.
   - Because R7–R12.1 did not execute due the syntax defect, the reconnect behavior must be tested afresh on R12.2 using a real device/network interruption.

5. **Official CSV file-picker UAT remains**
   - Transactional backend/import parser path exists.
   - 121-row structural mirror with official expected counts passes on real Supabase.
   - Exact browser file-picker import must be re-tested on R12.2 after sign-in.

6. **Native WebMCP final-origin test remains**
   - Validate only after exact canonical V0.28 runtime is recovered/deployed.

7. **Auth email environment**
   - Built-in confirmation mail rate limiting was encountered previously.
   - Password recovery is now proven to send successfully for the Organizer account.
   - Custom SMTP is not configured.
   - Leaked Password Protection remains disabled; this project-level Auth setting was not changed automatically.

## Non-blocking advisor findings

- Anonymous SECURITY DEFINER exposure: only intentional `get_guest_portal(p_token)`.
- Authenticated SECURITY DEFINER warnings reflect the authoritative role-checked RPC surface.
- Performance Advisor still contains unindexed-FK and unused-index INFO findings; no blind bulk indexing is applied.
