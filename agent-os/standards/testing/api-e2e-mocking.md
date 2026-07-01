# API Mocking in E2E

Intercept network calls and return fixtures. When many operations share one endpoint (e.g. a single GraphQL URL), dispatch on the request body.

```ts
await page.route('**/api/v1/graphql**', async (route) => {
  let body: { query?: string } = {};
  try {
    body = JSON.parse(route.request().postData() ?? '{}');
  } catch {
    body = {};
  }
  const query = body.query ?? '';

  if (query.includes('resources(')) {
    await route.fulfill({ body: JSON.stringify({ data: { resources: mockResources } }) });
    return;
  }

  await route.fulfill({ body: JSON.stringify({ data: {} }) }); // default
});
```

- Match the real response envelope (e.g. GraphQL `{ data: { ... } }`; errors as `{ errors: [...] }` with HTTP 200).
- Prefer **inline fixtures** when data is specific to one spec; extract shared fixtures to `tests/helpers/`.
- For REST, intercept per path/method instead of dispatching on a body.
- **Streaming endpoints need a different approach** — `route.fulfill()` closes the body immediately. See [[sse-streaming-tests]].

<!--
Fill in:
- Your real endpoint(s), envelope shape, and how errors are represented.
- Where shared fixtures live.
-->
