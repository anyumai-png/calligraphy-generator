# Event Table Planner — Remote Staging KNOWN_ISSUES

## Remaining release / environment gates

1. **Exact canonical V0.28 runtime bundle is not connected**
   - Final V0.28 `index.html` and final UAT evidence were recovered from File Library.
   - Exact final `app.js / styles.css / event-core.js / webmcp.js` are still not directly available.
   - Older V0.26.x runtime files must not be mixed into the V0.28 shell.
   - Remote R8 remains a temporary operations console, not the final V0.28 visual UI.

2. **Four real Auth personas not yet exercised through independent browsers**
   - One real confirmed Organizer account is active.
   - Reception / Floor / Viewer authorization has been verified at database/RPC level with separate user identity contexts.
   - Core two-identity races were also executed through genuinely parallel Supabase calls.
   - Full browser-session UAT still requires separate real Auth accounts/sessions.

3. **Physical weak-network / reconnect UAT remains**
   - R7 implements stale-state handling, reconnect backoff, channel rebuilding, online/offline handling, foreground refresh and stale-mutation protection.
   - External normal-network rendering is verified.
   - A real phone/tablet network interruption and recovery has not yet been exercised end-to-end.

4. **Native WebMCP final-origin validation remains**
   - Canonical V0.26+ Event Core/WebMCP design remains documented.
   - Final validation should occur after the exact V0.28 runtime is recovered and deployed.

5. **Auth email environment**
   - Supabase built-in email service hit rate limiting during signup.
   - The first staging account was confirmed through a one-time staging admin action that was subsequently disabled.
   - Custom SMTP is not configured.
   - Supabase Security Advisor reports Leaked Password Protection disabled. This is a project-level Auth setting and has not been changed automatically.

## Closed since R6

- True simultaneous database race gate is no longer pending.
- GitHub Pages deployed-origin behavior is no longer pending for the temporary staging shell.
- R7 reconnect/stale-state logic is implemented; only physical network-device UAT remains.

## Non-blocking advisor findings

- Security Advisor: the only anonymous SECURITY DEFINER RPC is intentionally public `get_guest_portal(p_token)`.
- Authenticated SECURITY DEFINER warnings are expected for the authoritative RPC surface; role checks are enforced inside the functions.
- Performance Advisor still reports unindexed foreign-key INFO findings and unused-index INFO findings. No bulk indexing is applied without workload evidence.
