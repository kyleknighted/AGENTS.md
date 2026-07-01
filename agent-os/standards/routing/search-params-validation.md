# Route Search Params & Validation

Validate URL search params with a **schema** (e.g. Zod) at the route boundary. Treat the URL as untrusted input.

```ts
const searchSchema = z.object({
  status: z.array(z.string()).optional(),
  sortBy: z.string().optional(),
  page: z.string().regex(/^\d+$/).optional(),
});

export const Route = createFileRoute('/resource')({
  validateSearch: (search) => searchSchema.parse(search),
});
```

- **Validate at the boundary** so downstream code receives typed, trusted values.
- **Coerce carefully.** Path/query values arrive as strings — validate as string then convert (`Math.max(1, Number(page))`). Beware naive boolean coercion: the string `"false"` is truthy.
- **Patch, don't replace** when updating params: `navigate({ search: (prev) => ({ ...prev, ...patch }) })` preserves unrelated params.
- **Normalize** canonical URL state (drop empties, fix casing) and navigate with `replace: true` on mismatch to avoid history spam.
- Keep any custom array/serialization logic in one module so it's testable and swappable.

<!--
Fill in:
- The real schemas per route and the serialization module.
- Any custom encoding (e.g. repeated keys `?status=a&status=b`) and whether the router can do it natively.
- How URL state maps to backend query input.
-->
