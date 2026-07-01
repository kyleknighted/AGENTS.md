# Auth-Bypassed E2E Mode

Run E2E tests without a real identity provider or backend. Gate the bypass behind explicit flags so it can never leak into production.

```ts
// Every test's beforeEach
await page.addInitScript(() => {
  window.localStorage.setItem('e2e_authless', 'true');
  window.localStorage.setItem('e2e_mock_session_data', 'true'); // optional
});
```

- Drive the bypass with **build/runtime flags** (env var) and/or **local-storage flags** read by the app.
- Point the test build at a **dummy API host** (e.g. `http://127.0.0.1:65535`) so a misconfigured test can never hit a real backend.
- In bypass mode, the auth token resolves to a known test value — see [[auth-token-resolution]].
- Mock API responses via route interception or inline fixtures — see [[api-e2e-mocking]].
- Build tests in a dedicated **test mode**, not dev mode, so bundling matches what you ship.

<!--
Fill in:
- The exact flag names (env + storage) and where the app reads them.
- The dummy host value and where it's configured.
- The test-build command and how to run against a live local server.
-->
