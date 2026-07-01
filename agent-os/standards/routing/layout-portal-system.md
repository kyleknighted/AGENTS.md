# Layout Portal / Slot System

Shared layout regions (sidebar, header/top content, etc.) are filled by child routes via context "portals" rather than prop drilling.

```ts
// A route contributes content to a layout slot and cleans up on unmount.
const { setSidebar } = useLayoutSidebar();

useIsomorphicLayoutEffect(() => {
  setSidebar(<Details id={id} />);
  return () => setSidebar(null); // ALWAYS clean up
}, [id, setSidebar]);
```

- Each slot has a small, documented API (single-slot setter vs. multi-contributor register).
- **Always clean up in the effect return** to avoid stale content lingering after navigation.
- Provide slots in the root layout hierarchy; make their hooks throw outside the provider.
- If multiple slot systems exist with different APIs, note it explicitly so contributors don't assume symmetry.

<!--
Fill in:
- The real slots, their hook names, and single- vs. multi-contributor semantics.
- Which effect variant to use (layout effect for pre-paint slot content).
-->
