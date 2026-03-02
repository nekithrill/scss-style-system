# 📖 Overview

A modular SCSS design token system that generates CSS variables with built-in theming support. Perfect for projects using CSS Modules or component-scoped styling.

## 🧩 What is this system?

This is a **token-first architecture** that separates design decisions from implementation. Instead of hardcoding values throughout your stylesheets, you define them once as tokens (colors, spacing, typography) and use them everywhere via CSS variables.

**The system provides:**

- **Design tokens** - Centralized SCSS variables for colors, spacing, typography, etc.
- **CSS variable generation** - Automatic conversion from tokens to `--css-variables`
- **Built-in theming** - Light/dark mode via CSS custom properties
- **Utility functions** - px→rem conversion, responsive breakpoints
- **Modular structure** - Use only what you need

## ✨ Key features

### 🎨 OKLCH color system with hue parameters

Change your entire color palette by adjusting a single hue value:

```scss
// Change from purple to blue with one line
$primary-hue: 200deg !default; // Was: 270deg
```

All 9 shades (100-900) automatically update to the new color.

### 🔄 Automatic rem conversion

Define values in familiar pixels, get consistent rem units:

```scss
// Define once in pixels
$base-spacing: 8px !default;

// Generated CSS variables automatically use rem
--sp-4: 2rem; /* 32px */
```

### 🌗 Simple theming

Themes are plain CSS custom properties - no mixins or schema required:

```scss
// themes/_light.scss
:root {
    --clr-text: var(--clr-neutral-900);
    --clr-main-bg: var(--clr-secondary-100);
}

// themes/_dark.scss
[data-theme='dark'] {
    --clr-text: var(--clr-neutral-100);
    --clr-main-bg: var(--clr-neutral-900);
}
```

### 🧩 Fully modular

Only import what you need:

```scss
// Minimal setup - just tokens
@use './tokens/colors' as *;
@use './tokens/spacing' as *;

// Full setup - with themes and utilities
@use './main' as *;
```

## 📦 What's included

### Design tokens (`/tokens`)

Raw design values defined as SCSS variables:

- **Colors** - OKLCH palettes with hue parameters (primary, secondary, neutral, semantic)
- **Typography** - Font families, sizes, weights
- **Spacing** - 8px grid system (0-8 scale)
- **Borders** - Radius (xs-xl) and stroke widths
- **Shadows** - Elevation system (xs-xl + inset)
- **Animations** - Duration, easing functions, delays
- **Breakpoints** - Responsive design breakpoints (xs-2xl)
- **Z-index** - Stacking order scale

### Core utilities (`/core`)

SCSS functions and mixins:

- **px-to-rem** - Convert pixel values to rem units
- **breakpoint** - Responsive media query mixin
- **generate-tokens** - Convert SCSS tokens to CSS variables

### Base styles (`/base`)

Optional foundational styles:

- **reset** - Modern CSS reset (box-sizing, margins, etc.)
- **variables** - CSS variable generation from tokens
- **globals** - HTML/body defaults (fonts, colors, smooth scroll)
- **fonts** - @font-face declarations
- **focus** - Keyboard navigation focus styles
- **scrollbar** - Custom scrollbar styling
- **selection** - Text selection highlight

### Theming (`/themes`)

Built-in light/dark mode support:

- **light** - Default light theme (`:root`)
- **dark** - Dark mode theme (`[data-theme='dark']`)

## ⚙️ How it works

### Step 1: Define tokens (SCSS variables)

```scss
// tokens/_colors.scss
$primary-hue: 270deg !default;

$primary: (
    100: oklch(95% 0.06 $primary-hue),
    500: oklch(60% 0.2 $primary-hue),
    900: oklch(12% 0.11 $primary-hue)
) !default;
```

### Step 2: System generates CSS variables

```css
:root {
    --clr-primary-100: oklch(95% 0.06 270deg);
    --clr-primary-500: oklch(60% 0.2 270deg);
    --clr-primary-900: oklch(12% 0.11 270deg);
}
```

> 💡 **Tip**
> No manual compilation needed with modern frameworks. For manual compilation setup, see [Getting Started](getting-started.md).

### Step 3: Use in your components

```scss
.button {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    border-radius: var(--rd-md);

    &:hover {
        background: var(--clr-primary-600);
    }
}
```

## 🎨 Quick customization examples

### Change brand color

```scss
// tokens/_colors.scss
$primary-hue: 200deg !default; // Blue instead of purple
```

### Smaller typography

```scss
// tokens/_typography.scss
$base-font-size: 14px !default; // Was 16px
```

### Tighter spacing

```scss
// tokens/_spacing.scss
$base-spacing: 4px !default; // Was 8px
```

See [Customizing](../06-usage/customizing.md) for complete guide.

## 🏗️ Architecture overview

The system uses a **two-layer architecture**:

**Layer 1: Design Tokens** → Raw values that never change
**Layer 2: Semantic Themes** → Context-aware mappings that adapt to themes

```
┌─────────────────────────────────────────────┐
│  Layer 1: Design Tokens                     │
│  (Immutable - Same in all themes)           │
│                                             │
│  $primary: (100: ..., 500: ..., 900: ...)   │
│  $neutral: (100: ..., 500: ..., 900: ...)   │
├─────────────────────────────────────────────┤
│  Layer 2: Semantic Themes                   │
│  (Mutable - Changes per theme)              │
│                                             │
│  Light: --clr-text: var(--clr-neutral-900)  │
│  Dark:  --clr-text: var(--clr-neutral-100)  │
└─────────────────────────────────────────────┘
```

See [Architecture](architecture.md) for detailed explanation.

## 🎯 Use cases

### ✅ Perfect for

- **Component-based projects** - React, Vue, Svelte with CSS Modules
- **Design systems** - Centralized tokens ensure consistency
- **Multi-theme apps** - Built-in light/dark mode
- **Rapid prototyping** - Change colors/spacing globally with one value

### ⚠️ Consider alternatives

- **Need utility classes?** → Try [Tailwind CSS](https://tailwindcss.com/)
- **No build step?** → Use plain CSS custom properties
- **Simple project?** → Plain CSS might be simpler

## 💭 Project philosophy

**Principles:**

1. **Tokens first** - All design decisions start with tokens
2. **Progressive enhancement** - Start minimal, add features as needed
3. **CSS Modules ready** - Works seamlessly with scoped styles
4. **Zero runtime** - Pure CSS variables, no JavaScript required
5. **Modular by default** - Every file is optional (except main.scss)

**Non-goals:**

- ❌ Not a CSS framework (no pre-built components)
- ❌ Not utility-first (no `.mt-4`, `.text-center` classes)
- ❌ Not opinionated about styling approach (use however you want)
