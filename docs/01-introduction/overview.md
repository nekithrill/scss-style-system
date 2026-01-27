## 📖 Overview

A modular SCSS design token system that generates CSS variables with built-in theming support. Perfect for projects using CSS Modules or component-scoped styling.

<br>

### 🧩 What is this system?

This is a **token-first architecture** that separates design decisions from implementation. Instead of hardcoding values throughout your stylesheets, you define them once as tokens (colors, spacing, typography) and use them everywhere via CSS variables.

**The system provides:**

- **Design tokens** - Centralized SCSS variables for colors, spacing, typography, etc.
- **CSS variable generation** - Automatic conversion from tokens to `--css-variables`
- **Built-in theming** - Light/dark mode with validation
- **Utility functions** - px→rem conversion, responsive breakpoints
- **Modular structure** - Use only what you need

---

### ✨ Key features

#### 🎨 OKLCH color system with hue parameters

Change your entire color palette by adjusting a single hue value:

```scss
// Change from purple to blue with one line
$primary-hue: 200deg !default;  // Was: 270deg
```

All 9 shades (100-900) automatically update to the new color.

#### 🔄 Automatic rem conversion

Define values in familiar pixels, get consistent rem units:

```scss
// Define once in pixels
$base-spacing: 8px !default;

// Generated CSS variables automatically use rem
--sp-4: 2rem;  /* 32px */
```

#### 🌗 Theme validation

Built-in schema validation prevents theme errors:

```scss
// Define required structure
$theme-required-keys: (
    text: (...),
    header: (...),
    main: (...)
);

// System validates your themes automatically
@include validate-theme($dark, $theme-required-keys);
```

#### 🧩 Fully modular

Only import what you need:

```scss
// Minimal setup - just tokens
@use './tokens/colors' as *;
@use './tokens/spacing' as *;

// Full setup - with themes and utilities
@use './main' as *;
```

---

### 📦 What's included

#### Design tokens (`/tokens`)

Raw design values defined as SCSS variables:

- **Colors** - OKLCH palettes with hue parameters (primary, secondary, neutral, semantic)
- **Typography** - Font families, sizes, weights
- **Spacing** - 8px grid system (0-8 scale)
- **Borders** - Radius (xs-xl) and stroke widths
- **Shadows** - Elevation system (xs-xl + inset)
- **Animations** - Duration, easing functions, delays
- **Breakpoints** - Responsive design breakpoints (xs-2xl)
- **Z-index** - Stacking order scale

#### Core utilities (`/core`)

SCSS functions and mixins:

- **px-to-rem** - Convert pixel values to rem units
- **breakpoint** - Responsive media query mixin
- **generate-tokens** - Convert SCSS tokens to CSS variables
- **generate-theme** - Generate theme CSS variables
- **validate-theme** - Validate theme structure against schema

#### Base styles (`/base`)

Optional foundational styles:

- **reset** - Modern CSS reset (box-sizing, margins, etc.)
- **variables** - CSS variable generation from tokens
- **globals** - HTML/body defaults (fonts, colors, smooth scroll)
- **fonts** - @font-face declarations
- **focus** - Keyboard navigation focus styles
- **scrollbar** - Custom scrollbar styling
- **selection** - Text selection highlight

#### Theming (`/themes`)

Built-in light/dark mode support:

- **schema** - Define required theme structure
- **light** - Default light theme
- **dark** - Dark mode theme
- **apply** - Theme validation and application

---

### ⚙️ How it works

#### Step 1: Define tokens (SCSS variables)

```scss
// tokens/_colors.scss
$primary-hue: 270deg !default;

$primary: (
    100: oklch(95% 0.06 $primary-hue),
    500: oklch(60% 0.2 $primary-hue),
    900: oklch(12% 0.11 $primary-hue)
) !default;
```

#### Step 2: System generates CSS variables

Modern bundlers (Vite, Next.js) automatically convert tokens to CSS variables:

```css
:root {
    --clr-primary-100: oklch(95% 0.06 270deg);
    --clr-primary-500: oklch(60% 0.2 270deg);
    --clr-primary-900: oklch(12% 0.11 270deg);
}
```

> 💡 **No manual compilation needed** with modern frameworks. For manual compilation setup, see [Getting Started - Option C](getting-started.md#option-c-standalone-htmlcss).

#### Step 3: Use in your components

```scss
// Component.module.scss (with modern bundlers)
.button {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    border-radius: var(--rd-md);
    
    &:hover {
        background: var(--clr-primary-600);
    }
}
```

```jsx
// Button.jsx
import styles from './Button.module.scss';

export function Button({ children }) {
    return <button className={styles.button}>{children}</button>;
}
```

---

### 🎨 Quick customization examples

#### Change brand color

```scss
// tokens/_colors.scss
$primary-hue: 200deg !default;  // Blue instead of purple
```

Result: All primary colors (100-900) become blue automatically.

#### Smaller typography

```scss
// tokens/_typography.scss
$base-font-size: 14px !default;  // Was 16px
```

Result: All heading sizes scale down proportionally.

#### Tighter spacing

```scss
// tokens/_spacing.scss
$base-spacing: 4px !default;  // Was 8px
```

Result: Entire spacing scale becomes more compact (4px, 8px, 12px...).

See [Customizing](../06-usage/customizing.md) for complete guide.

---

### 🏗️ Architecture overview

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

This separation allows you to:
- Define colors once, use in multiple themes
- Switch themes without changing component code
- Maintain visual consistency across modes

See [Architecture](architecture.md) for detailed explanation.

---

### 🔌 Integration methods

The system supports three main usage patterns:

#### Modern bundlers

**Tools:** Vite, Next.js, Webpack, Create React App

```jsx
// main.jsx - Import once
import './styles/main.scss';

// Component.module.scss - Use variables
.card {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
}
```

**Benefits:** Auto-compilation, hot reload, CSS Modules  
**Setup:** → See [Getting Started - Option A](getting-started.md#option-a-react--vite)

#### Manual compilation

**Tools:** Sass CLI for static sites or legacy projects

```bash
sass src/styles/main.scss dist/styles.css
```

```html
<link rel="stylesheet" href="/dist/styles.css">
```

**Benefits:** Simple, no bundler required  
**Setup:** → See [Getting Started - Option C](getting-started.md#option-c-standalone-htmlcss)

#### Direct token import

**Use case:** When you don't need CSS variables or theming

```scss
// Component.module.scss
@use '@/styles/tokens/colors' as colors;
@use '@/styles/tokens/spacing' as spacing;

.button {
    padding: spacing.$sp-4;
    background: map-get(colors.$primary, 500);
}
```

**Benefits:** Compile-time values, no CSS variable overhead  
**Trade-offs:** No theming, no runtime changes  
**Documentation:** See [Direct Token Usage](../06-usage/direct-tokens.md)

---

### 🎯 Use cases

#### ✅ Perfect for

- **Component-based projects** - React, Vue, Svelte with CSS Modules
- **Design systems** - Centralized tokens ensure consistency
- **Multi-theme apps** - Built-in light/dark mode
- **Rapid prototyping** - Change colors/spacing globally with one value

#### ⚠️ Consider alternatives

- **Need utility classes?** → Try [Tailwind CSS](https://tailwindcss.com/)
- **No build step?** → Use plain CSS custom properties
- **Simple project?** → Plain CSS might be simpler

---

### 💭 Project philosophy

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