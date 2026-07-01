# Visual Snapshot Stabilization

Visual-regression snapshots must be **deterministic**. Make snapshots opt-in and remove every source of run-to-run variance.

```ts
// Example uses a Playwright-based snapshot tool; adapt to your visual-testing setup.
import { expect, test, takeSnapshot } from '<visual-snapshot-tool>';

test.use({ disableAutoSnapshot: true }); // opt-in, not automatic

test('page renders correctly', async ({ page }, testInfo) => {
  await page.goto('/');
  await takeSnapshot(page, 'page renders correctly', testInfo);
});
```

## Common Flakiness Sources to Avoid

- **Date/time** — mock the clock or use fixed timestamps; relative labels like "just now" drift.
- **External images/avatars** — block external requests so components fall back deterministically.
- **Loading races** — wait for data before snapshotting; rely on the runner's auto-waiting.
- **Animations & hover** — disable transitions and non-deterministic states in snapshot contexts.
- **Brittle selectors** — prefer `getByRole` / `getByTestId` / `getByText` over CSS paths or generated class names.
- **Hardcoded timeouts** — never `waitForTimeout`; use web-first assertions.
- **Shared state / order dependence** — keep tests isolated.
- **Missing `await`** — always await async actions before asserting.

<!--
Fill in:
- Any component-specific overrides needed for stable snapshots (scrollbars, portals).
- The external-image blocking helper's location.
-->
