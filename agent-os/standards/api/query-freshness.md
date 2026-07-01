# Query Freshness Tiers

Use centralized stale-time constants. **Do not hardcode stale times** at call sites.

```ts
import {
  STATIC_STALE_TIME,
  SLOW_STALE_TIME,
  DEFAULT_STALE_TIME,
  REALTIME_STALE_TIME,
} from '@/lib/queryFreshness';
```

| Tier | Suggested value | Use for |
|------|-----------------|---------|
| `STATIC_STALE_TIME` | `Infinity` | Static/sample data that never changes at runtime |
| `SLOW_STALE_TIME` | ~5 min | Admin-managed config that rarely changes |
| `DEFAULT_STALE_TIME` | ~30s | General-purpose baseline |
| `REALTIME_STALE_TIME` | `0` | Lists that must look fresh on back-navigation |

- Pick a **small set of named tiers** and reuse them; one-off numbers drift out of sync.
- `staleTime: 0` is a **UX choice** (refetch on navigation), not a polling mechanism.
- `staleTime` only governs *background* refetches — you must still **invalidate on mutation**, even for slow-tier data.
- Decide `refetchOnWindowFocus` globally (disabling it avoids flicker on tab switch) and document the choice.

<!--
Fill in:
- The constants module path and the actual values you chose.
- The global refetch-on-focus decision and why.
-->
