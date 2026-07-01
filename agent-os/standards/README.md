# Agent-Facing Coding Standards (Skeleton Kit)

These files are **project-agnostic skeletons**: each encodes common baseline rules for its topic plus `<!-- Fill in -->` markers for the details that vary per project. Use them as a jumping-off point when starting a new codebase.

## How to use

1. **Point your agent instructions at this folder.** Reference `index.yml` from your `AGENTS.md` so agents discover the standards by domain.
2. **Fill in the markers.** Search for `<!-- Fill in` and replace placeholders (paths like `@/lib/...`, names like `apiRequest`, and example tokens) with this project's real specifics.
3. **Delete what doesn't apply.** e.g. drop `api/thin-proxy-routes.md` if the app calls its backend directly, or `api/tenant-scoping.md` if it isn't multi-tenant. Remove the matching `index.yml` entry too.
4. **Add new standards** as patterns emerge — keep each file focused on one rule, and keep `index.yml` in sync.

## Format convention

Each standard follows the same shape:

- A one-line **rule** at the top.
- A minimal **code example** (generic names — adapt to the stack).
- **Bullet points** of rationale, sharp edges, and exceptions.
- Cross-links to related standards via `[[file-name]]`.
- A closing `<!-- Fill in -->` block listing the project-specific details to supply.

## Domains

- `api/` — data fetching, client wrapper, caching, proxy/tenant concerns.
- `routing/` — providers, layout slots, access control, params, data loading.
- `testing/` — E2E auth bypass, mocking, streaming, visual snapshots, unit coverage.
- `ui/` — styling, design-system layering, empty/loading states, layout gotchas.
