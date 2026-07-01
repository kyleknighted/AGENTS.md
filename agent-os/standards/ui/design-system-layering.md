# Design System Layering

If the app sits on a **design-system wrapper** over a **base component library**, define the layering rules so contributors know what to import from where.

```ts
// A wrapper component = base component with enforced project defaults.
const Badge = ({ children, ...rest }: BadgeProps) => (
  <BaseBadge size="1" variant="surface" radius="large" {...rest} />
);
```

- **Use the base library directly** for generic primitives (layout, form controls, one-offs).
- **Use the wrapper** for domain/branded components with enforced defaults.
- **Promote to the wrapper** when the same base configuration appears in **3+ places** (rule of three).
- Keep a clear component taxonomy (e.g. atoms → molecules → compounds → layout).
- Document the import boundary explicitly (which package for what) and any bans (e.g. don't import the base library's styling engine directly).

<!--
Fill in:
- The wrapper and base library names, or delete this file if the app uses one library directly.
- The exact import rules and the reuse threshold.
-->
