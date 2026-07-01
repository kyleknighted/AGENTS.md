# Skeleton Loading States

Every view that loads data must have a **content-aware** skeleton that mirrors the real layout — not a generic spinner sitting in empty space.

```tsx
export const DashboardSkeleton = () => (
  <Flex direction="column" gap="3">
    <Skeleton loading height="32px" width="200px" />
    <Flex gap="3">
      <Skeleton loading height="120px" width="100%" />
      <Skeleton loading height="120px" width="100%" />
    </Flex>
  </Flex>
);
```

- **Match the real layout grid** — same structure and spacing — so the swap to loaded content doesn't shift the page.
- Either give skeleton blocks explicit `height`/`width`, or wrap real elements whose structure already defines dimensions.
- **Export named skeleton components** for reuse; colocate them with their component (or a `parts/` subdir).
- Prefer content-aware skeletons for in-view data loads; a spinner is acceptable for route-level navigation pending states.

<!--
Fill in:
- The skeleton primitive your design system provides and its API.
- Naming/colocation convention for skeleton components.
-->
