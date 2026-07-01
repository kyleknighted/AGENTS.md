# Tenant / Scope Injection

If the app is multi-tenant (workspace / org / account scoping), inject the scope in **one central place** — the shared API client — not at every call site.

```ts
// Happens automatically inside the shared client — no manual scoping per call.
const scopedPath =
  method === 'GET' && path.startsWith('/api/v1/')
    ? withScope(path) // appends ?tenant_id=<id>
    : path;
```

- Resolve the current scope from one source of truth (e.g. `getCurrentTenantId()` backed by storage), not scattered reads.
- Define the behavior for an "all tenants" selection (usually: skip the param).
- Be explicit about **which methods** are auto-scoped. If only reads are auto-scoped, mutations must pass scope themselves — document this sharp edge.
- Expose a manual override (`withScope(path, id?)`) for the cases that need it.

<!--
Fill in:
- Whether the app is multi-tenant at all (delete this file if not).
- The scope param name, the resolver, and where selection is persisted.
- Exactly which requests are auto-scoped vs. manual.
-->
