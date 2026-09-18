# Event Table Planner — Remote Staging KNOWN_ISSUES

## Remaining environment / release gates

1. **Exact canonical V0.28 runtime bundle is not connected**
   - Final V0.28 HTML/UAT evidence exists.
   - Exact final `app.js / styles.css / event-core.js / webmcp.js` are still unavailable.
   - Remote R11 is a temporary operations shell, not the final V0.28 visual UI.

2. **Four real Auth personas are not yet exercised in independent browsers**
   - One confirmed real Organizer account is active.
   - Reception / Floor / Viewer are DB/RPC-verified with independent identity contexts.
   - Core true parallel two-identity races pass.

3. **Physical network interruption UAT remains**
   - R7 reconnect/stale-state logic is implemented and normal-network smoke passes.
   - A real phone/tablet offline / weak-network → reconnect cycle remains to be exercised.

4. **Official CSV file-picker UAT remains**
   - R10 parser and transactional backend support the official canonical columns.
   - A 121-row structural mirror with the official expected counts passes on real Supabase.
   - The exact File Library CSV has not yet been selected/imported through an authenticated real browser file picker.

5. **Native WebMCP final-origin test remains**
   - Validate only after the exact canonical V0.28 runtime is recovered/deployed.

6. **Auth email environment**
   - Supabase built-in confirmation email rate limiting was encountered.
   - Custom SMTP is not configured.
   - Leaked Password Protection remains disabled in Supabase Auth; this project-level account setting was not changed automatically.

## Non-blocking advisor findings

- Anonymous SECURITY DEFINER exposure: only intentional `get_guest_portal(p_token)`.
- Authenticated SECURITY DEFINER warnings reflect the authoritative role-checked RPC surface.
- Performance Advisor still contains unindexed-FK and unused-index INFO findings; no blind bulk indexing is applied.
