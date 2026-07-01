# Two-Tier Data Loading

Routes **prefetch** in the loader; components **hydrate** from cache. Both tiers use the **same query-options factory** so they share a cache key and fire a single request.

## Tier 1: Route Loader (prefetch)

```ts
export const Route = createFileRoute('/')({
  loader: ({ context }) => {
    const token = getLoaderToken();
    if (token) {
      void context.queryClient.prefetchQuery(resourceLoaderOptions(token));
    }
  },
  component: ResourcePage,
});
```

## Tier 2: Component Query (hydrate)

```ts
const { data } = useQuery(resourceLoaderOptions(token));
```

- **One shared options factory** for both tiers guarantees cache-key alignment and no duplicate fetch.
- Loaders **fire-and-forget** (`void prefetchQuery`); the component query resolves from cache or awaits.
- If auth/params are unavailable in the loader, skip prefetch — the component query still handles it.

## Loader Auth Bridge

Loaders run **outside React**, so they can't use React auth hooks. Bridge auth into module scope.

- A small sync component writes current auth into a module-level cache.
- Loaders read it via plain getters (`getLoaderToken()`), not hooks.
- Treat this as a pragmatic bridge, not the ideal design.

<!--
Fill in:
- The options-factory naming convention and an example.
- The loader auth-bridge module, if this app's loaders need auth.
-->
