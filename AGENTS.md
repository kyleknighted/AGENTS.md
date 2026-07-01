# Repository Guidelines

<!--
This file is the canonical instruction set for coding agents.
Keep it concrete: prefer commands, paths, and enforceable rules over vague advice.
Every rule should be checkable — an agent (or a linter) should be able to tell if it was followed.
-->

## Project Structure & Module Organization

- `<src-dir>/` contains <framework/app description>.
- `<src-dir>/<routes|pages>/` holds <routing/entry-point description>.
- `<src-dir>/<components|context|utils|types>/` organize <UI, state, helpers, shared types>.
- `<generated-types-file>` defines <how contract/generated types are used>; prefer reusing these over redefining shapes.
- `<tests-dir>/` contains <test framework> specs; `<tests-dir>/helpers/` holds shared fixtures.
- `<docs-dir>/` contains <handbook/reference>; review relevant pages before changing those areas.
- `agent-os/standards/` contains agent-facing coding standards by domain; see `agent-os/standards/index.yml` for the full index.
- Build outputs land in `<build-output-dir>/`.
- <Note any submodules, vendored packages, or auto-synced files and how they stay in sync.>

## Build, Test, and Development Commands

<!-- List the exact commands. One line each: `command`: what it does + any non-obvious flags/ports. -->
- `<dev command>`: Run the local dev server (<tool>, port <n>).
- `<build command>`: Production build + typecheck.
- `<typecheck command>`: Type check only.
- `<lint command>`: Lint (+ auto-fix scope).
- `<format command>`: Formatting.
- `<unit test command>`: Run unit tests.
- `<e2e test command>`: Run end-to-end tests.
- `<coverage command>`: Coverage for <scope>.

## Coding Style & Naming Conventions

- Language/module system: <e.g. TypeScript + React, ES modules>.
- Indentation & quotes: <e.g. 2-space, single quotes — managed by formatter>.
- Naming: <PascalCase for components, camelCase for hooks/utils, etc.>.
- File placement: <where reusable functions, types, and route-specific logic live>.
- Preferred libraries: <e.g. use `date-fns` for all date work; import UI from `<ui-package>`, not `<underlying-lib>` directly>.
- Type-safety rules (with rationale + allowed exceptions):
  <!--
  This is where your AGENTS.md shines — spell out bans and their escape hatches.
  Example pattern:
  - Avoid `any`/`unknown` without validation + a comment explaining why it's safe.
  - No arbitrary type assertions (`as`). Narrow with guards/discriminated unions/`satisfies`/runtime validation.
    Allowed exceptions, in priority order:
      1. `as const` — always allowed.
      2. Test mocks.
      3. Runtime-validated casts — must include a `// Safe: <reason>` comment referencing the guard.
      4. Unvalidated casts (last resort) — must include a `// TODO: <issue-link>` tracking the type gap.
  -->
- API work: prefer existing typed helpers / generated contract types over ad hoc `fetch` parsing.
- Preserve existing <design-system/UI> patterns unless the task explicitly calls for a broader change.

## Testing Guidelines

- Frameworks: <unit framework> for deterministic logic (`<scope>`), <e2e framework> for user flows (`<tests-dir>/*.spec`).
- Naming & placement: <spec file naming convention and directory>.
- Keep specs focused on user flows; shared utilities go in `<tests-dir>/helpers/`.
- Run `<coverage command>` when changing <shared utils / env / deterministic logic>.
- Run `<e2e command>` before PRs touching <routed flows / UI state>.

### <Special Testing Scenario> <!-- e.g. SSE streaming, websockets, workers -->
<!--
Document non-obvious testing gotchas here — the traps that cost hours.
Include: why the naive approach fails, the correct approach, and any protocol/contract details
(event names, response shapes) the test must match.
-->

## Commit & Pull Request Guidelines

- Commit messages: <style — e.g. short, imperative, lowercase>. Keep commits scoped to one concern.
- PRs include: brief summary, screenshots for UI changes, linked issues when applicable.
- <Note any auto-updated files / pre-commit hooks and the manual fallback if hooks are skipped.>
- Local PR gates should usually cover: `<lint>`, `<typecheck>`, `<coverage>`, and relevant `<e2e/build>` commands.

## Security & Configuration Notes

- Secrets management: <how local secrets are provided; what must be present before running>.
- Environment-driven config: <what is env-driven; do not hardcode local overrides>.
- API docs / contracts live at `<location>`; consult directly and keep generated types aligned.

## Historical Reference <!-- optional; useful during migrations -->

- <Where to look when behavior is unclear (prior app, parity docs, etc.).>

## Documentation Requirements

- `AGENTS.md` is the canonical agent instruction file; keep other agent entry points aligned to it.
- New/updated contracts or long-lived workflows affecting the broader team must ship with a matching `<docs-dir>/` update in the same change.
- Agent-instruction-only policies may live solely in `AGENTS.md` if they add no obligations for human workflows.

## Skills & Tooling Workflow <!-- optional -->

- Treat installed skills/MCP servers as first-class tools; use a matching skill's instructions before ad hoc approaches.
- Enable Agent OS by keeping `agent-os/standards/` in your repo and referencing `agent-os/standards/index.yml` from this file.
- <Design-to-code flow, component-doc MCP servers, or other required tool workflows.>

## <Domain> PR Checklist <!-- optional; e.g. UI PR Checklist -->

- [ ] Relevant skills/tools were used (or documented why not).
- [ ] <Domain-specific import/convention checks.>
- [ ] Screenshots/recordings included for visible changes.
- [ ] Ran `<typecheck>` and targeted tests before requesting review.
