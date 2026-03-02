# 🏗️ Architecture

The system is built on a **two-layer token architecture** that separates design decisions from implementation:

**Layer 1: Design Tokens** - Raw design values (colors, spacing, typography)  
**Layer 2: Semantic Themes** - Context-aware CSS variable mappings for different themes

This separation allows you to:

- Define colors once, use them in multiple themes
- Switch themes without changing component styles
- Maintain consistency across light/dark modes

## Layer 1: Design Tokens

**Location:** `/tokens/*.scss`

Design tokens are the foundation - they contain actual values like colors, spacing, and typography settings. These never change between themes.

**Example:**

```scss
// tokens/_colors.scss
$primary: (
	100: oklch(95% 0.06 270deg),
	500: oklch(60% 0.2 270deg),
	900: oklch(12% 0.11 270deg)
);

$neutral: (
	100: oklch(96% 0.01 220deg),
	500: oklch(56% 0.04 220deg),
	900: oklch(20% 0.01 220deg)
);
```

**Generated CSS variables:**

```css
:root {
	--clr-primary-100: oklch(95% 0.06 270deg);
	--clr-primary-500: oklch(60% 0.2 270deg);
	--clr-primary-900: oklch(12% 0.11 270deg);
	--clr-neutral-100: oklch(96% 0.01 220deg);
	--clr-neutral-500: oklch(56% 0.04 220deg);
	--clr-neutral-900: oklch(20% 0.01 220deg);
}
```

## Layer 2: Semantic Themes

**Location:** `/themes/*.scss`

Themes directly declare CSS custom properties that reference design tokens. Light theme is defined in `:root`, dark theme in `[data-theme='dark']`.

**Example:**

```scss
// themes/_light.scss
:root {
	--clr-main-bg: var(--clr-neutral-100);
	--clr-main-bg-hover: var(--clr-neutral-200);
	--clr-main-text: var(--clr-neutral-900);

	--clr-header-bg: var(--clr-primary-500);
	--clr-header-text: var(--clr-neutral-100);
}

// themes/_dark.scss
[data-theme='dark'] {
	--clr-main-bg: var(--clr-neutral-900);
	--clr-main-bg-hover: var(--clr-neutral-800);
	--clr-main-text: var(--clr-neutral-100);

	--clr-header-bg: var(--clr-primary-700);
	--clr-header-text: var(--clr-neutral-100);
}
```

## How components use the system

> ℹ️ **Note**
> Design tokens (spacing, radius, typography, etc.) work the same everywhere and can be used directly. Semantic theme variables are used for colors and backgrounds that change between themes.

### Option 1: Direct token usage (simple projects)

```scss
.card {
	background: var(--clr-neutral-100);
	color: var(--clr-neutral-900);
	border-radius: var(--rd-md);
	padding: var(--sp-4);
}
```

### Option 2: Semantic theme variables (multi-theme projects)

```scss
.card {
	background: var(--clr-main-bg);
	color: var(--clr-main-text);
	border-radius: var(--rd-md);
	padding: var(--sp-4);

	&:hover {
		background: var(--clr-main-bg-hover);
	}
}
```

---

### Architecture Flow

```
┌─────────────────────────────────────────────────────────┐
│ 1. Design Tokens (tokens/*.scss)                        │
│    Define raw values                                    │
│    ↓                                                    │
│    $primary: (500: oklch(...))                          │
│    $spacing: (1: 8px, 2: 16px, ...)                     │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│ 2. Generated CSS Variables (in :root)                   │
│    ↓                                                    │
│    --clr-primary-500: oklch(...)                        │
│    --sp-1: 0.5rem                                       │
│    --rd-md: 0.375rem                                    │
└─────────────────────────────────────────────────────────┘
                        ↓
        ┌───────────────┴───────────────┐
        │                               │
        │    ┌──────────────────┐       │
        │    │ OPTIONAL LAYER   │       │
        │    │ Theme mapping    │       │
        │    └────────┬─────────┘       │
        │             ↓                 │
        │    --clr-main-bg              │
        │    --clr-main-text            │
        └───────────────┬───────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│ 3. Component Styles                                     │
│                                                         │
│    // Option 1: Direct tokens (simple projects)         │
│    .card {                                              │
│      background: var(--clr-neutral-100);                │
│      padding: var(--sp-4);                              │
│    }                                                    │
│                                                         │
│    // Option 2: Semantic themes (multi-theme projects)  │
│    .card {                                              │
│      background: var(--clr-main-bg);     ← Theme        │
│      padding: var(--sp-4);               ← Token        │
│    }                                                    │
└─────────────────────────────────────────────────────────┘
```
