# Context Provider Composition

Compose all app-wide providers in **one root file**. State this app's global-state approach up front (e.g. pure React Context, or a store library) so contributors don't mix paradigms.

```
AuthProvider              // outermost — everything depends on auth
  → ThemeProvider
    → <Tenant/Org selection>
      → <Feature providers>
        → <Layout providers>
          → AppLayout
            → <Route outlet>
```

- **Auth outermost** — all downstream state depends on auth being resolved.
- Order dependent providers so parents supply what children read (e.g. tenant depends on org).
- Make every context hook **throw if used outside its provider** — fail loud, not silently `undefined`.
- Persist user-scoped selections with keys namespaced by user id (`${baseKey}:${userId}`) so they don't leak across accounts.
- Support a **mock/dev variant** of auth-dependent providers for E2E — see [[authless-e2e-mode]].

<!--
Fill in:
- The real provider tree and which orderings are hard dependencies vs. cosmetic.
- The global-state approach (Context / store library / none).
- Which providers persist state and under what keys.
-->
