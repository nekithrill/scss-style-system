# 📖 Overview

A modular SCSS design token system that generates CSS custom properties with built-in theming support. Designed for component-based projects using CSS Modules or scoped styles.

## 🧠 What is this system?

A **token-first architecture** that separates design decisions from implementation. Instead of hardcoding values throughout stylesheets, you define them once as tokens and reference them everywhere via CSS custom properties.

```scss
// Without tokens — values scattered everywhere
.button { padding: 16px; background: #7c3aed; border-radius: 6px; }
.card   { padding: 16px; background: #7c3aed; border-radius: 6px; }

// With tokens — single source of truth
.button { padding: var(--sp-2); background: var(--clr-primary-500); border-radius: var(--rd-md); }
.card   { padding: var(--sp-2); background: var(--clr-primary-500); border-radius: var(--rd-md); }
```

See [Architecture](architecture.md) for detailed explanation.

## ✨ Key features

### OKLCH color system

Colors defined in OKLCH — a perceptually uniform color space. Each palette is controlled by a single hue variable. All five shades update automatically:

```scss
$primary-hue: 200deg !default; // Change one value → all shades update
```

### Automatic rem conversion

Spacing, typography, and border tokens are defined in familiar pixels and output as rem:

```css
--sp-2: 1rem;   /* 16px */
--sp-4: 2rem;   /* 32px */
--fs-h1: 2rem;  /* 32px */
```

### Light / dark theming

Themes are plain CSS custom properties. No mixins or JavaScript required:

```scss
:root            { --clr-bg: var(--clr-secondary-100); }
[data-theme='dark'] { --clr-bg: var(--clr-secondary-900); }
```

### Modular structure

Every file is optional. Import only what you need:

```scss
@use './tokens/colors' as *;   // Just colors
@use './main' as *;             // Everything
```

## 📦 What's included

### Tokens (`/tokens`)

| Group | Prefix | Description |
|-------|--------|-------------|
| Colors | `--clr-` | OKLCH palettes — brand and semantic |
| Typography | `--fs-`, `--ff-`, `--fw-`, `--lh-`, `--ls-` | Sizes, families, weights, line heights, letter spacings |
| Spacing | `--sp-` | 8px grid, 10 steps |
| Borders | `--br-`, `--bw-` | Radius and width |
| Shadows | `--shadow-` | Elevation scale |
| Animations | `--dur-`, `--tf-`, `--delay-` | Duration, easing, delay |
| Z-index | `--z-` | Stacking context |
| Breakpoints | — | Used via mixin only |

### Core utilities (`/core`)

- `px-to-rem` — converts px to rem at compile time
- `breakpoint` — responsive media query mixin (mobile-first by default)
- `generate-tokens` — converts SCSS maps to CSS custom properties

### Base styles (`/base`)

Optional foundational styles, each file independent:

- `_reset.scss` — modern CSS reset
- `_globals.scss` — html/body defaults
- `_fonts.scss` — `@font-face` template
- `_focus.scss` — keyboard navigation focus styles
- `_scrollbar.scss` — custom scrollbar
- `_selection.scss` — text selection highlight
- `_variables.scss` — CSS variable generation

### Themes (`/themes`)

- `_light.scss` — light theme (`:root`)
- `_dark.scss` — dark theme (`[data-theme='dark']`)

## ❔ When to use

Works well for component-based projects (React, Vue, Svelte) with CSS Modules, and for projects that need consistent light/dark theming without a utility-first approach.

If you need utility classes (`.mt-4`, `.text-center`), [Tailwind CSS](https://tailwindcss.com/) is a better fit. If there's no build step, plain CSS custom properties may be simpler.