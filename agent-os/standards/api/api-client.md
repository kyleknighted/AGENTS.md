# Shared API Client

Route **all** network calls through a shared, typed client wrapper. No ad hoc `fetch()` with hand-rolled request/response parsing in feature code.

```ts
// Generic wrapper — one for REST, one for GraphQL, or a unified client.
import { apiRequest } from '@/lib/apiClient';

const data = await apiRequest<ResponseType>({
  path: '/resource',
  method: 'GET',
  token, // when the transport needs it explicitly
});
```

- **Centralize** base URL, headers, auth, error handling, and retries in the wrapper — call sites stay declarative.
- **Type requests and responses.** Prefer generated types (OpenAPI / GraphQL codegen) over hand-written shapes so they track the contract.
- **Normalize errors.** A non-2xx status — or a `200 OK` GraphQL body containing `errors` — should throw a typed error, not silently return partial data.
- Keep query/document strings in dedicated modules, not inlined at call sites.

<!--
Fill in:
- The wrapper's name and location (e.g. `src/lib/apiClient.ts`).
- REST vs. GraphQL vs. both; whether codegen is adopted or planned.
- The typed-error class name and what triggers it.
- Any in-progress migration between transports and the safe default.
-->
