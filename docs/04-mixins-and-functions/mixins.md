> **📁 Location:** `styles/core/mixins/*.scss`
> **🧭 Scope:** Stylesheet generation and system-level abstractions
> **📦 Type:** Core

# ⚙️ Mixins

Reusable style patterns for responsive design, token generation, and theme management.

## breakpoint

**Purpose:** Generate responsive media queries from design tokens with mobile-first or desktop-first approach.

**Location:** `styles/core/mixins/_breakpoint.scss`

### ✍️ Signature

```scss
@mixin breakpoint($size, $min-width: false);
```

### 🧩 Parameters

- `$size` (String) - Breakpoint key from `$breakpoints` map (`'xs'`, `'sm'`, `'md'`, `'lg'`, `'xl'`, `'2xl'`)
- `$min-width` (Boolean, optional) - `true` for mobile-first (min-width), `false` for desktop-first (max-width). Default: `false`

### 🧠 How it works

1. **Lookup:** Retrieves breakpoint value from `$breakpoints` map using the `$size` key
2. **Validation:** Throws error if breakpoint key doesn't exist, listing available options
3. **Query generation:** Creates either `min-width` or `max-width` media query based on `$min-width` flag
4. **Content injection:** Inserts provided styles inside the media query using `@content`

**Error handling:** If invalid breakpoint provided:

```scss
@include breakpoint('tablet');
// Error: ⚠️ Breakpoint 'tablet' not found. Available: xs, sm, md, lg, xl, 2xl
```

### 🚀 Usage

```scss
@use '@/styles/core/mixins/breakpoint' as *;

.component {
	padding: var(--sp-4);

	// Desktop-first (default): applies when viewport ≤ 768px
	@include breakpoint('md') {
		padding: var(--sp-2);
	}

	// Mobile-first: applies when viewport ≥ 1024px
	@include breakpoint('lg', true) {
		padding: var(--sp-6);
	}
}
```

**Generated CSS:**

```css
.component {
	padding: 2rem;
}

@media (max-width: 768px) {
	.component {
		padding: 1rem;
	}
}

@media (min-width: 1024px) {
	.component {
		padding: 3rem;
	}
}
```

**Advanced examples:**

```scss
// Responsive grid
.grid {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: var(--sp-4);

	@include breakpoint('lg') {
		grid-template-columns: repeat(3, 1fr); // ≤ 1024px
	}

	@include breakpoint('md') {
		grid-template-columns: repeat(2, 1fr); // ≤ 768px
	}

	@include breakpoint('sm') {
		grid-template-columns: 1fr; // ≤ 576px
	}
}

// Mobile-first navigation
.nav {
	display: none; // Hidden on mobile

	@include breakpoint('md', true) {
		display: flex; // Show on tablet and up
	}
}

// Complex responsive component
.card {
	padding: var(--sp-6);
	font-size: var(--fs-h3);

	@include breakpoint('lg') {
		padding: var(--sp-4);
		font-size: var(--fs-h4);
	}

	@include breakpoint('sm') {
		padding: var(--sp-2);
		font-size: var(--fs-h5);
	}
}
```

### ✔️ Best practices

- ✅ **Do:** Use desktop-first (default) for progressive enhancement
- ✅ **Do:** Use mobile-first when starting with mobile design
- ✅ **Do:** Be consistent - don't mix approaches in same component
- ✅ **Do:** Reference breakpoint tokens, never hardcode values
- ❌ **Don't:** Use random px values: `@media (max-width: 768px)`
- ❌ **Don't:** Mix mobile-first and desktop-first in same element
- ❌ **Don't:** Create too many breakpoints (3-4 is usually enough)

```scss
// ✅ Good: Consistent desktop-first
.element {
	width: 100%;

	@include breakpoint('lg') { width: 75%; }
	@include breakpoint('md') { width: 50%; }
}

// ❌ Bad: Mixing approaches
.element {
	@include breakpoint('md', true) { ... }  // Mobile-first
	@include breakpoint('lg') { ... }        // Desktop-first
}

// ✅ Good: Mobile-first throughout
.element {
	width: 100%;

	@include breakpoint('md', true) { width: 75%; }
	@include breakpoint('lg', true) { width: 50%; }
}
```

## generate-tokens

**Purpose:** Generate CSS custom properties from design token maps with automatic structure detection and optional px → rem conversion.

**Location:** `styles/core/mixins/_generate-tokens.scss`

### ✍️ Signature

```scss
@mixin generate-tokens($tokens);
```

### 🧩 Parameters

- `$tokens` (Map) - Token configuration where each group contains:
  - `map` (Map, required) - Token values
  - `prefix` (String, required) - CSS variable prefix
  - `transform` (String, optional) - Set to `'rem'` to convert px to rem

### 🧠 How it works

1. **Group iteration:** Loops through each token group in the configuration map
2. **Validation:** Checks for required `map` and `prefix` keys, throws error if missing
3. **Structure detection:** Automatically determines if map is nested or flat:
   - **Nested:** First value is a map → generates `--prefix-palette-shade` (e.g., `--clr-primary-500`)
   - **Flat:** First value is not a map → generates `--prefix-key` (e.g., `--sp-4`)
4. **Transformation:** If `transform: 'rem'` specified, applies `px-to-rem()` function
5. **Variable generation:** Creates CSS custom properties with proper naming

**Structure detection examples:**

```scss
// Nested map detected
$colors: (
	'primary': (
		100: #e0e7ff,
		500: #6366f1
	)
);
// → --clr-primary-100, --clr-primary-500

// Flat map detected
$spacing: (
	1: 8px,
	2: 16px
);
// → --sp-1, --sp-2
```

**Error handling:**

```scss
$tokens: (
	colors: (
		map: $colors // Missing 'prefix'!
	)
);

@include generate-tokens($tokens);
// Error: generate-tokens: Group 'colors' missing 'prefix' key
```

### 🚀 Usage

```scss
@use '@/styles/core/mixins/generate-tokens' as *;

$base-tokens: (
	colors: (
		map: $all-colors,
		prefix: 'clr'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	)
);

:root {
	@include generate-tokens($base-tokens);
}
```

**Generated CSS:**

```css
:root {
	/* Colors (nested map) */
	--clr-primary-100: oklch(95% 0.06 270deg);
	--clr-primary-500: oklch(60% 0.2 270deg);
	--clr-neutral-100: oklch(96% 0.01 220deg);

	/* Spacing (flat map with rem transform) */
	--sp-0: 0;
	--sp-1: 0.5rem; /* 8px → rem */
	--sp-2: 1rem; /* 16px → rem */
	--sp-4: 2rem; /* 32px → rem */
}
```

**Advanced examples:**

```scss
// Complete token setup
@use '../tokens/colors' as *;
@use '../tokens/spacing' as *;
@use '../tokens/typography' as *;
@use '../tokens/borders' as *;
@use '../core/mixins/generate-tokens' as *;

$base-tokens: (
	colors: (
		map: $all-colors,
		prefix: 'clr'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	),
	font-sizes: (
		map: $font-sizes,
		prefix: 'fs',
		transform: 'rem'
	),
	font-weights: (
		map: $font-weights,
		prefix: 'fw'
	),
	radius: (
		map: $border-radius,
		prefix: 'rd',
		transform: 'rem'
	)
);

:root {
	@include generate-tokens($base-tokens);
}
```

### ✔️ Best practices

- ✅ **Do:** Always include `prefix` for namespacing
- ✅ **Do:** Use `transform: 'rem'` for spacing, sizing, typography
- ✅ **Do:** Keep prefixes short and consistent (`clr`, `sp`, `rd`)
- ❌ **Don't:** Transform colors, weights, shadows, or unitless values
- ❌ **Don't:** Use long prefixes like `color` or `spacing`
- ❌ **Don't:** Forget to import token maps before using

```scss
// ✅ Good: Proper token configuration
$base-tokens: (
	spacing: (
		map: $spacing,
		prefix: 'sp',
		// Short prefix
		transform: 'rem' // Convert to rem
	),
	colors: (
		map: $all-colors,
		prefix: 'clr' // No transform for colors
	)
);

// ❌ Bad: Wrong configuration
$base-tokens: (
	spacing: (
		map: $spacing,
		prefix: 'spacing',
		// Too long
		transform: 'rem'
	),
	colors: (
		map: $all-colors,
		prefix: 'clr',
		transform: 'rem' // Don't transform colors!
	)
);
```