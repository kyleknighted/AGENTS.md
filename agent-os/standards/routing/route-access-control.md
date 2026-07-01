# Route Access Control

Guard protected routes with shared, named guard functions. Decide and document **where** guards run and **what** unauthorized users see.

```ts
import { enforceAdminAccess } from '@/lib/routeAccess';

function SettingsPage() {
  const authInfo = useAuth();
  enforceAdminAccess(authInfo); // throws a not-found/redirect if unauthorized

  if (authInfo.loading) return null; // wait for auth; avoid flash of protected content
  return <SettingsContent />;
}
```

- **Wait for auth to resolve** (`loading === false`) before checking roles; return `null` meanwhile to prevent a flash of unauthorized content.
- Centralize guards in one module and name them per capability (`enforceAdminAccess`, `enforceBillingAccess`, …) — no inline role checks scattered in components.
- Choose deliberately between **404 (hide existence)** and **403 (acknowledge, deny)** and apply it consistently.
- Reserve `beforeLoad`/loader-level checks for redirects and URL normalization; keep the choice of layer explicit.

<!--
Fill in:
- The guard module path and the real list of guards.
- Whether guards run in the component body or `beforeLoad`, and why.
- The 404-vs-403 policy for this app.
-->
