## 🏗️ Architecture

The system is built on a **two-layer token architecture** that separates design decisions from implementation:

**Layer 1: Design Tokens** - Raw design values (colors, spacing, typography)  
**Layer 2: Semantic Themes** - Context-aware mappings for different themes

This separation allows you to:

- Define colors once, use them in multiple themes
- Switch themes without changing component styles
- Maintain consistency across light/dark modes

<br>

## Layer 1: Design Tokens

**Purpose:** Store all raw design values in one place.

**Location:** `/tokens/*.scss`

Design tokens are the foundation — they contain actual values like colors, spacing, and typography settings. These never change between themes.

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
	/* Available globally, but not necessarily used directly in components */
	--clr-primary-100: oklch(95% 0.06 270deg);
	--clr-primary-500: oklch(60% 0.2 270deg);
	--clr-primary-900: oklch(12% 0.11 270deg);
	--clr-neutral-100: oklch(96% 0.01 220deg);
	--clr-neutral-500: oklch(56% 0.04 220deg);
	--clr-neutral-900: oklch(20% 0.01 220deg);
}
```

<br>

## Layer 2: Semantic Themes

**Purpose:** Map design tokens to semantic, context-aware variables.

**Location:** `/themes/*.scss`

Themes define what each semantic variable means in different contexts (light/dark mode). They reference design tokens and create meaningful names like `--clr-main-bg` instead of `--clr-neutral-100`.

> 💡 **Note:** The underscore (`_`) represents the base/default value for a property. Modifiers like `hover`, `active` extend from this base.

**Example:**
```scss
// themes/_light.scss
$light: (
	main: (
		bg: (
			_: var(--clr-neutral-100),     // Base: Light background
			hover: var(--clr-neutral-200)   // Modifier: Hover state
		),
		text: (
			_: var(--clr-neutral-900)      // Base: Dark text
		)
	),
	header: (
		bg: (
			_: var(--clr-primary-500)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	)
);

// themes/_dark.scss
$dark: (
	main: (
		bg: (
			_: var(--clr-neutral-900),     // Base: Dark background
			hover: var(--clr-neutral-800)   // Modifier: Hover state
		),
		text: (
			_: var(--clr-neutral-100)      // Base: Light text
		)
	),
	header: (
		bg: (
			_: var(--clr-primary-700)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	)
);
```

<br>

## How components use the system

The system is **flexible** - you can use it in different ways depending on your project needs.

> 💡 **Note:** Design tokens (spacing, radius, typography, etc.) work the same everywhere and can be used directly in any approach. Semantic theme variables are optional and primarily used for colors and backgrounds that change between themes.

---

### Option 1: Direct token usage (simple projects)

For small projects or prototypes, you can use design tokens directly in components:

```scss
.card {
	background: var(--clr-neutral-100);
	color: var(--clr-neutral-900);
	border-radius: var(--rd-md);
	padding: var(--sp-4);
}
```

**When to use:**

- Small projects without theming
- Prototypes and MVPs
- Single-theme applications
- When simplicity matters more than flexibility

**Benefits:**

- Less abstraction, more straightforward
- Fewer files to manage
- Direct control over values

---

### Option 2: Semantic theme variables (complex projects)

For projects with multiple themes (light/dark mode, brand variations), use semantic theme variables **for colors** while keeping direct tokens for everything else:

```scss
.card {
	// Theme variables (colors/backgrounds that change)
	background: var(--clr-main-bg);
	color: var(--clr-main-text);

	// Direct tokens (same across all themes)
	border-radius: var(--rd-md);
	padding: var(--sp-4);

	&:hover {
		background: var(--clr-main-bg-hover);
	}
}
```

**When to use:**

- Multi-theme applications (light/dark mode)
- Brand variations or white-label products
- When you need to switch themes dynamically
- Large projects with complex theming needs

**Benefits:**

- Theme switching without rewriting styles
- Semantic naming for better clarity
- Centralized theme management
- No need to create theme variables for spacing, radius, etc.

**What NOT to theme:**

Avoid creating semantic variables for values that don't change between themes (spacing, radius, typography, shadows, z-index) - use direct tokens instead.

---

**Why this works:**

- Colors and backgrounds change between themes → use semantic variables
- Spacing, radius, typography stay the same → use tokens directly
- Best of both worlds: flexibility where needed, simplicity where possible

<br>

## Architecture Flow

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
        │    --theme-main-bg            │
        │    --theme-main-text          │
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
