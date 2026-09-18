# Event Table Planner — Remote Staging KNOWN_ISSUES

## Release blockers / environment gates

1. **Canonical V0.28 source not connected**
   - The connected GitHub account does not expose the canonical Event Table Planner repository.
   - Remote R6 is a temporary staging operations console, not the final V0.28 visual UI.

2. **Four real Auth personas not yet exercised concurrently**
   - One real confirmed Organizer account is active.
   - Reception / Floor / Viewer authorization has been transaction-tested with separate user identity simulation, but not yet through independent real browser sessions.

3. **True simultaneous race test still pending**
   - Stale-token conflict behavior is verified.
   - Row-lock / revision primitives are verified.
   - Two physically independent sessions issuing the same mutation at the same instant remain to be tested.

4. **Weak-network / Realtime reconnect not yet tested**
   - Normal Realtime subscriptions are implemented in the staging console.
   - Disconnect/reconnect and stale recovery still require device/network UAT.

5. **Auth email environment**
   - Supabase built-in email service hit rate limiting during signup.
   - Staging account was confirmed through an admin-only one-time staging action, which was then disabled.
   - Custom SMTP is not configured.
   - Supabase Security Advisor reports Leaked Password Protection disabled. This is a project-level Auth setting and has not been changed automatically.

## Non-blocking advisor findings

- Security Advisor: the only anonymous SECURITY DEFINER RPC is intentionally public `get_guest_portal(p_token)`.
- Authenticated SECURITY DEFINER RPC warnings are expected for the authoritative RPC surface; role checks are enforced inside the functions.
- Performance Advisor still reports unindexed foreign-key INFO findings and unused-index INFO findings. No bulk indexing was applied without workload evidence.
