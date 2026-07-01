# AGENTS.md

A project-agnostic template and starting point for `AGENTS.md` — the canonical instruction file for coding agents.

## What is AGENTS.md?

`AGENTS.md` is a structured, machine-readable file placed at the root of your repository. It gives coding agents (like GitHub Copilot, OpenAI Codex, and similar tools) the context they need to work effectively inside your codebase without requiring repeated prompting or guesswork.

Think of it as your project's onboarding document — written for agents instead of humans, but useful to humans too.

## Why does it matter?

Without an `AGENTS.md`, agents must infer your project's conventions, commands, and constraints from the code alone — leading to inconsistent style, broken builds, and wasted review cycles.

With a well-maintained `AGENTS.md`, agents can:

- **Run the right commands** — know exactly how to build, lint, test, and typecheck your project.
- **Follow your conventions** — naming, file placement, preferred libraries, and type-safety rules.
- **Avoid known pitfalls** — documented gotchas, banned patterns, and required escape hatches.
- **Stay in sync** — understand which files are auto-generated, vendored, or synced externally.
- **Respect your PR process** — commit message style, required gates, and checklist items.

## Usage

1. Copy `AGENTS.md` from this repository into the root of your project.
2. Replace every `<placeholder>` with the specifics of your stack and workflow.
3. Remove or comment out any sections that don't apply to your project.
4. Keep it up to date as your project evolves — treat it like any other source file.

### Tips for a good AGENTS.md

- **Be concrete.** Prefer exact commands, file paths, and enforceable rules over vague guidance.
- **Be checkable.** Every rule should be something an agent (or a linter) can verify was followed.
- **Be explicit about exceptions.** If a rule has escape hatches, document them alongside the rule.
- **Document the non-obvious.** Focus on things that can't be inferred from reading the code — historical context, tooling quirks, protocol details, banned patterns with rationale.

## Template sections

| Section | Purpose |
|---|---|
| **Project Structure** | Where things live and how they're organized |
| **Build, Test & Dev Commands** | Exact CLI commands the agent should use |
| **Coding Style & Naming** | Language, formatting, naming conventions, type-safety rules |
| **Testing Guidelines** | Frameworks, file placement, coverage gates, non-obvious gotchas |
| **Commit & PR Guidelines** | Message style, PR content, pre-merge gates |
| **Security & Configuration** | Secrets handling, environment config, API contracts |
| **Historical Reference** | Where to look when behavior is unclear |
| **Documentation Requirements** | When and where to update docs |
| **Skills & Tooling Workflow** | MCP servers, design-to-code flows, required tool integrations |
| **Domain PR Checklist** | Per-change checklist items for specific areas (e.g. UI) |

## License

MIT
