# Auth Token Resolution

Every data-fetching hook must resolve an auth token **before** enabling its query. Queries that fire before auth is ready pollute the cache with auth errors.

```ts
// Generic pattern — adapt to your auth provider and query library.
const { accessToken } = useAuth();
const token = accessToken ?? (isTestMode() ? 'test-token' : undefined);

return useQuery({
  // Do not fetch until a token exists.
  enabled: Boolean(token) && options?.enabled !== false,
  // ...
});
```

- **`enabled: Boolean(token)` is critical** — without it, queries run before auth resolves and cache failures.
- Provide a **test/dev fallback token** (e.g. `'test-token'`) so E2E/dev runs work without a real identity provider. Gate it behind an explicit flag — see [[authless-e2e-mode]].
- Keep token resolution in **one shared hook/util** rather than repeating it per query.
- Prefer implicit transport where possible (e.g. cookies) and only pass the token explicitly where the transport requires it (e.g. an `Authorization: Bearer` header).

<!--
Fill in:
- Which auth provider/SDK supplies the token, and the hook name.
- The name of the shared resolver (e.g. `useResolvedToken()`).
- Which requests need the token explicitly vs. implicitly (cookies).
- The exact test-mode flag(s) — cross-link the E2E standard.
-->
