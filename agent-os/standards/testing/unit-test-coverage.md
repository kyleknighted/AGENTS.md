# Unit Test Coverage

Unit-test deterministic logic (pure utils, reducers, formatters). Define an explicit **coverage scope** and **thresholds** so "enough tests" is objective.

## Thresholds

| Metric | Threshold |
|--------|-----------|
| Statements | 80% |
| Branches | 70% |
| Functions | 80% |
| Lines | 80% |

## Conventions

- Test files: `*.test.ts(x)`, colocated with the code under test (sibling file or `__tests__/`).
- Default to a **Node** environment for pure logic; opt into a DOM environment only when needed (e.g. `// @vitest-environment jsdom`).
- Wrap component renders in the app's required providers (theme, etc.).
- Mock external modules, and reset mocks in `afterEach` (`clearAllMocks` / `restoreAllMocks`).
- Run coverage when changing shared utils, env handling, or other deterministic logic.

```ts
import { afterEach, describe, expect, it, vi } from 'vitest';

vi.mock('@/lib/apiClient', () => ({ apiRequest: vi.fn() }));

afterEach(() => {
  vi.clearAllMocks();
  vi.restoreAllMocks();
});
```

<!--
Fill in:
- The real coverage scope (which globs count) and your chosen thresholds.
- Which flows rely on E2E instead of unit coverage.
- The exact coverage command.
-->
