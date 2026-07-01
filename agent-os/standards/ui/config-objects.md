# Config Objects for Status & Severity

Map enums (status, severity, type) to display properties with a **config object**, not `switch`/`if` chains.

```ts
const STATUS_CONFIG: Record<IssueStatus, { label: string; color: BadgeColor; icon: ReactNode }> = {
  OPEN: { label: 'Open', color: 'blue', icon: <CircleIcon /> },
  IN_PROGRESS: { label: 'In Progress', color: 'orange', icon: <ClockIcon /> },
  RESOLVED: { label: 'Resolved', color: 'green', icon: <CheckIcon /> },
  DISMISSED: { label: 'Dismissed', color: 'gray', icon: <MinusCircleIcon /> },
};

const config = STATUS_CONFIG[status];
return <Badge color={config.color}>{config.label}</Badge>;
```

- Centralizes all visual representations in one place — update once, consistent everywhere.
- Type as `Record<EnumType, ConfigShape>` so the compiler flags a **missing variant** when the enum grows.
- Store config objects as **module-level constants**, not rebuilt inside components.
- More readable and diff-friendly than long conditional blocks.

<!--
Fill in:
- Nothing framework-specific required — swap Badge/color types for your design system.
-->
