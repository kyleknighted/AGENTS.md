# Styling Conventions

Pick one styling approach and apply it consistently. This skeleton assumes **CSS Modules + a design system's layout props**; adapt if you use Tailwind, styled-components, etc.

```css
/* ComponentName.module.css */
.container { border-radius: var(--radius-2); }
.containerActive { composes: container; border-color: var(--accent-9); }
```

- **Layout/spacing via the design system first** — use component props (`gap`, `px`, `py`, `mt`) rather than bespoke CSS for spacing.
- **CSS Modules** for what props can't express: animations (`@keyframes`), pseudo-classes (`:hover`, `:focus`), scrollbars, media queries.
- **Theme via CSS variables** — always `var(--gray-1)`, `var(--accent-9)`, etc. **Never hardcode colors.**
- **`:global()` sparingly** — reaching into a library's internal class names is fragile across upgrades; isolate and comment it.
- **Prefer CSS Modules over inline styles.** Small one-off inline styles are fine for truly dynamic values (computed widths); avoid them for anything needing pseudo-classes, media queries, or reuse.

<!--
Fill in:
- The chosen styling system and any hard bans (e.g. "no Tailwind", "no inline colors").
- The theme token conventions for this project.
-->
