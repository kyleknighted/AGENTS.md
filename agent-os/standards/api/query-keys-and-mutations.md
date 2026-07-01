# Query Key Factory & Mutations

Use a **query-key factory** object per domain. Keys are hierarchical so a parent key can invalidate everything beneath it.

```ts
export const resourceKeys = {
  all: ['resource'] as const,
  list: (filters, page, pageSize, sortBy, sortOrder) =>
    [...resourceKeys.all, 'list', { filters, page, pageSize, sortBy, sortOrder }] as const,
  detail: (id: string) => [...resourceKeys.all, 'detail', id] as const,
};
```

- Top-level key (`resourceKeys.all`) enables `invalidateQueries({ queryKey: resourceKeys.all })` to clear the whole domain.
- List keys embed filter/sort objects for granular caching; detail keys end with the entity id.
- Never spell out raw key arrays at call sites — always go through the factory.

## Optimistic Updates

For mutations that change visible UI state, implement the full cancel → snapshot → rollback pattern:

```ts
onMutate: async (variables) => {
  await queryClient.cancelQueries({ queryKey });
  const previousData = queryClient.getQueryData(queryKey);
  queryClient.setQueryData(queryKey, optimisticUpdate);
  return { previousData };
},
onError: (_error, _variables, context) => {
  if (context?.previousData) queryClient.setQueryData(queryKey, context.previousData);
},
onSettled: () => queryClient.invalidateQueries({ queryKey }),
```

- Cancel in-flight queries **before** the optimistic write to avoid races.
- Always return `previousData` for rollback.
- Simple mutations (e.g. delete-then-redirect) may skip optimism when the UX doesn't benefit.

<!--
Fill in:
- One key factory per real domain in your app.
- Which mutations use optimistic updates vs. plain invalidation.
-->
