# Flex Scroll Containers

Any scrollable area inside a flex column needs `min-height: 0` on the flex child. Without it, content overflows instead of scrolling.

```tsx
// Correct: enables scroll
<Flex direction="column" flexGrow="1" minHeight="0">
  <ScrollArea>{/* long content */}</ScrollArea>
</Flex>

// Bug: content overflows the parent
<Flex direction="column" flexGrow="1">
  <ScrollArea>{/* long content */}</ScrollArea>
</Flex>
```

- Flex items default to `min-height: auto`, which refuses to shrink below content size; `min-height: 0` lets them shrink so the inner area can scroll.
- Apply to **every** flex child that wraps a scrollable region (nested flex layouts need it at each level).
- This is a framework-agnostic CSS rule — the prop name (`minHeight="0"`) or `style={{ minHeight: 0 }}` depends on your stack.
- A frequent, hard-to-debug source of overflow bugs — call it out in review.
