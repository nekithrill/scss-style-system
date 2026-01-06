## ⚙️ Core utilities

Core mixins and functions for token generation, theming, and responsive design.

<br>

## Mixins

### `breakpoint` - Responsive media queries

Generate media queries from design tokens with mobile-first or desktop-first approach.

**Location:** `core/mixins/_breakpoint.scss`

**Signature:**
```scss
@mixin breakpoint($size, $min-width: false)
```

**Parameters:**
- `$size` (string) - Breakpoint key from `$breakpoints` token map
- `$min-width` (boolean, optional) - `true` for mobile-first (min-width), `false` for desktop-first (max-width). Default: `false`

**Usage:**
```scss
@use '@/styles/core/mixins/breakpoint' as *;

.component {
	padding: var(--sp-4);
	
	// Desktop-first (max-width)
	@include breakpoint('md') {
		padding: var(--sp-2);  // Applies when viewport ≤ 768px
	}
	
	// Mobile-first (min-width)
	@include breakpoint('lg', true) {
		padding: var(--sp-6);  // Applies when viewport ≥ 1024px
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

**Error handling:**
```scss
@include breakpoint('tablet');
// Error: ⚠️ Breakpoint 'tablet' not found. Available: xs, sm, md, lg, xl, 2xl
```

---

### `generate-tokens` - Design token variables

Generate CSS variables from design token maps with automatic structure detection and optional px → rem conversion.

**Location:** `core/mixins/_generate-tokens.scss`

**Signature:**
```scss
@mixin generate-tokens($tokens)
```

**Parameters:**
- `$tokens` (map) - Token configuration with groups

**Token structure:**
```scss
$tokens: (
	group-name: (
		map: $map-data,      // Required: token values
		prefix: 'prefix',    // Required: CSS variable prefix
		transform: 'rem'     // Optional: convert px to rem
	)
)
```

**Usage:**
```scss
// Setup tokens
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
	font-weights: (
		map: $font-weights,
		prefix: 'fw'
	)
);

// Generate variables
:root {
	@include generate-tokens($base-tokens);
}
```

**Generated CSS:**
```css
:root {
	/* Nested maps (colors) - detects automatically */
	--clr-primary-100: #e0e7ff;
	--clr-primary-500: #6366f1;
	--clr-neutral-100: #f5f5f5;
	--clr-neutral-900: #171717;
	
	/* Flat maps with transform (spacing) */
	--sp-0: 0;
	--sp-1: 0.5rem;    /* 8px → rem */
	--sp-2: 1rem;      /* 16px → rem */
	--sp-4: 2rem;      /* 32px → rem */
	
	/* Flat maps without transform (weights) */
	--fw-regular: 400;
	--fw-bold: 700;
}
```

**How it works:**

1. **Auto-detects structure:**
   - Nested maps (colors with shades) → `--prefix-palette-shade`
   - Flat maps (spacing, weights) → `--prefix-key`

2. **Optional transformation:**
   - `transform: 'rem'` converts px values to rem
   - Uses base font size of 16px

3. **Error handling:**
   - Missing `map` or `prefix` throws error
   - Invalid values are returned as-is

---

### `generate-theme` - Theme variables

Generate CSS custom properties from theme maps with recursive structure support.

**Location:** `core/mixins/_generate-theme.scss`

**Signature:**
```scss
@mixin generate-theme($map, $prefix: 'clr')
```

**Parameters:**
- `$map` (map) - Theme map with nested structure
- `$prefix` (string, optional) - CSS variable prefix. Default: `'clr'`

**Special key handling:**
- `_` key → generates base variable (`--clr-main-bg`)
- Other keys → generate variants (`--clr-main-bg-hover`)
- Nested maps → recurse with updated prefix

**Usage:**
```scss
// Define theme
$dark: (
	header: (
		bg: (
			_: var(--clr-neutral-900),
			hover: var(--clr-neutral-800)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	),
	main: (
		bg: (
			_: var(--clr-neutral-800)
		)
	)
);

// Generate theme variables
[data-theme='dark'] {
	@include generate-theme($dark);
}
```

**Generated CSS:**
```css
[data-theme='dark'] {
	--clr-header-bg: var(--clr-neutral-900);
	--clr-header-bg-hover: var(--clr-neutral-800);
	--clr-header-text: var(--clr-neutral-100);
	--clr-main-bg: var(--clr-neutral-800);
}
```

**Supports nested structures:**
```scss
$theme: (
	product: (
		card: (
			bg: (
				_: #fff
			),
			border: (
				_: #e5e5e5
			)
		),
		price: (
			regular: (
				_: #171717
			),
			discount: (
				_: #dc2626
			)
		)
	)
);
```

**Generates:**
```css
--clr-product-card-bg: #fff;
--clr-product-card-border: #e5e5e5;
--clr-product-price-regular: #171717;
--clr-product-price-discount: #dc2626;
```

---

### `validate-theme` - Theme structure validator

Validate theme maps against schema structure. Checks required keys and warns about unexpected keys.

**Location:** `core/mixins/_validate-theme.scss`

**Signature:**
```scss
@mixin validate-theme($theme-map, $required-keys, $allowed-leaf-keys, $parent: null)
```

**Parameters:**
- `$theme-map` (map) - Theme map to validate
- `$required-keys` (map) - Required keys structure from schema
- `$allowed-leaf-keys` (list) - Whitelisted keys at deepest level (`_`, `hover`, `active`, etc.)
- `$parent` (string, optional) - Internal recursion path (don't pass manually)

**Usage:**
```scss
@use 'themes/schema' as *;

// Validate before generating
@include validate-theme($dark, $theme-required-keys, $theme-leaf-keys);

// Then generate
:root {
	@include generate-theme($dark);
}
```

**Validation checks:**

**1. Required keys check (error):**
```scss
// ❌ Missing required key
$light: (
	text: (...),
	header: (...)
	// footer: (...) ← MISSING!
);

@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);
// Error: ⚠️ Theme map is missing required key `footer`!
```

**2. Leaf keys check (warning):**
```scss
// ⚠️ Unexpected key (typo)
$light: (
	header: (
		bg: (
			_: #fff,
			hovered: #eee  // ← Typo: should be 'hover'
		)
	)
);

@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);
// Warning: ⚠️ Theme map contains unexpected key `header.bg.hovered` that is not in the schema or leaf keys whitelist!
```

**What's NOT validated:**
- Presence of `_` base value (optional by design)
- Value types (doesn't check if CSS is valid)
- Value references (doesn't check if `var(--clr-invalid)` exists)

---

<br>

## Functions

### `px-to-rem` - Unit converter

Convert pixel values to rem units based on base font size.

**Location:** `core/functions/_px-to-rem.scss`

**Signature:**
```scss
@function px-to-rem($value, $base: 16)
```

**Parameters:**
- `$value` (number | list) - Value in px, list of values, or zero
- `$base` (number, optional) - Base font-size in pixels (must be unitless or in px). Default: `16`

**Returns:**
- Number or list in rem units

**Features:**
- Converts px to rem based on base font size (default 16px)
- Zero values return `0` (any unit: `0`, `0px`, `0em`, `0%`, `0rem`)
- Non-px units are returned as-is (%, em, rem, etc.)
- Very large values (5000px+) stay in px (used for pill borders: 9999px)
- Works recursively on lists

**Usage:**
```scss
@use 'core/functions/px-to-rem' as *;

// Single values
$spacing: px-to-rem(16px);    // 1rem
$margin: px-to-rem(24px);     // 1.5rem
$zero: px-to-rem(0);          // 0
$zero-px: px-to-rem(0px);     // 0

// Non-px units (returned as-is)
$percent: px-to-rem(50%);     // 50%
$em: px-to-rem(2em);          // 2em
$rem: px-to-rem(1.5rem);      // 1.5rem

// Very large values (stay in px)
$pill: px-to-rem(9999px);     // 9999px (not converted)
$large: px-to-rem(5000px);    // 5000px (not converted)

// Lists (recursive)
$padding: px-to-rem(10px 20px 30px);  // 0.625rem 1.25rem 1.875rem
$shadow: px-to-rem(0 4px 8px);        // 0 0.25rem 0.5rem
$mixed: px-to-rem(4px 9999px);        // 0.25rem 9999px

// Custom base per-call
$value: px-to-rem(32px, 20);  // 1.6rem (32 / 20 = 1.6)
```

**Customizing default base:**

If your project uses a different base font-size (e.g., 18px instead of 16px):

1. Open `core/functions/_px-to-rem.scss`
2. Change the function signature:
```scss
   @function px-to-rem($value, $base: 18) {  // Changed from 16 to 18
```
3. All conversions will now use 18px as the base

> 💡 **Note:** This affects all rem conversions system-wide. Only change if your entire project uses a non-standard base font-size.

**Special handling:**

The function automatically handles edge cases:

- **Zero values:** `0`, `0px`, `0em`, `0%`, `0rem` → `0`
- **Non-px units:** `50%`, `2em`, `1.5rem` → returned as-is
- **Very large values:** `5000px+` → stay in px (e.g., `9999px` for pill borders)
- **Lists:** Processes each value recursively

This ensures pill-shaped borders (`border-radius: 9999px`) and similar edge cases work correctly without conversion.


<br>

## Best Practices

**Breakpoint mixin:**
- Use desktop-first (default) for progressive enhancement
- Use mobile-first (`true` flag) when starting with mobile design
- Always reference breakpoint tokens, never hardcode values

**Token generation:**
- Always include `prefix` for namespacing
- Use `transform: 'rem'` for spacing, sizing, and layout tokens
- Don't transform colors, weights, shadows, or unitless values

**Theme generation:**
- Validate themes before generation in development
- Use semantic component names (not technical names)
- Include `_` base value when element needs default state

**px-to-rem conversion:**
- Used automatically by `generate-tokens` mixin
- Don't use directly unless building custom utilities
- Default 16px base aligns with browser defaults
- Change default base only if your project requires it (rare)