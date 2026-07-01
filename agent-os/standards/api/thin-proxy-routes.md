# Thin Proxy Routes

If the app proxies to a backend, route handlers are **pure pass-throughs** with zero business logic. The web tier is a security boundary, not a logic layer.

```ts
// Generic server route handler — delegates to a shared proxy helper.
const handle = ({ request }: { request: Request }) => proxyRequest(request, '/api/v1/resource');
export const Route = createFileRoute('/api/v1/resource')({ server: { handlers: { GET: handle } } });
```

- **No validation, transformation, or error handling in route files.** Business logic lives in the backend.
- The shared `proxyRequest()` helper forwards headers (stripping hop-by-hop), preserves query strings, and returns the upstream response as-is.
- Auth (cookies/tokens) flows through implicitly — no per-route extraction.
- On upstream failure, return a consistent gateway error (e.g. HTTP 502 with a short body).

**Exception:** stateful streaming routes (SSE/WebSocket) need custom connection management — see [[sse-streaming-tests]].

<!--
Fill in:
- Whether this app proxies at all (delete this file if it calls the backend directly).
- The proxy helper's name/location and its exact failure behavior.
- The list of routes that are legitimately NOT thin (streaming, auth callbacks).
-->
