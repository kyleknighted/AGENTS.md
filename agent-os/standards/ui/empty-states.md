# Empty States

Every list/table view must have an empty state. Always include three things: **title**, **guidance**, **action**.

```tsx
<FilteredResultsEmptyState
  title="No issues found"
  guidance="Try adjusting your filters or search terms."
  resetButtonLabel="Reset filters"
  onResetFilters={handleReset}
/>
```

- **Title** — what's empty ("No issues found", "No calls yet").
- **Guidance** — why it's empty or what to do next.
- **Action** — a button that resolves the state (reset filters, create first item).
- Distinguish **"no data yet"** (first-run) from **"no results for these filters"** — they need different copy and actions.
- Never ship a bare "No results" with no context or next step.
- Use a **shared empty-state component** so every list looks consistent.

<!--
Fill in:
- The shared component name/location and its container styling.
-->
