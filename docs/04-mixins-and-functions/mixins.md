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

## generate-theme

**Purpose:** Generate CSS custom properties from theme maps with recursive structure support for semantic color variables.

**Location:** `styles/core/mixins/_generate-theme.scss`

### ✍️ Signature

```scss
@mixin generate-theme($map, $prefix: 'clr');
```

### 🧩 Parameters

- `$map` (Map) - Theme map with nested structure
- `$prefix` (String, optional) - CSS variable prefix. Default: `'clr'`

**Special key handling:**

- `_` key → base variable (`--clr-main-bg`)
- Other keys → variant variables (`--clr-main-bg-hover`)
- Nested maps → recursive processing with updated prefix

### 🧠 How it works

1. **Map validation:** Checks if input is a map, throws error if not
2. **Key iteration:** Loops through each key-value pair
3. **Special key handling:**
   - If key is `_` → generate base variable without suffix
   - If value is map → recurse with updated prefix (`prefix-key`)
   - Otherwise → generate leaf variable with key suffix (`prefix-key`)
4. **Prefix building:** Concatenates parts with hyphens for proper CSS variable names

**Prefix evolution:**

```scss
$theme: (
	product: (
		// prefix: 'clr'
		card: (
				// prefix: 'clr-product'
				bg: (
						// prefix: 'clr-product-card'
						_: #fff // → --clr-product-card-bg
					)
			)
	)
);
```

### 🚀 Usage

```scss
@use '@/styles/core/mixins/generate-theme' as *;

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

**Advanced examples:**

```scss
// Complex theme with multiple levels
$light: (
	text: (
		_: var(--clr-neutral-900),
		accent: var(--clr-primary-500),
		muted: var(--clr-neutral-600)
	),
	button: (
		primary: (
			bg: (
				_: var(--clr-primary-500),
				hover: var(--clr-primary-600),
				active: var(--clr-primary-700),
				disabled: var(--clr-neutral-300)
			),
			text: (
				_: var(--clr-neutral-100)
			)
		),
		secondary: (
			bg: (
				_: var(--clr-secondary-200),
				hover: var(--clr-secondary-300)
			),
			text: (
				_: var(--clr-neutral-900)
			)
		)
	)
);

:root {
	@include generate-theme($light);
}

// Generates:
// --clr-text: var(--clr-neutral-900);
// --clr-text-accent: var(--clr-primary-500);
// --clr-text-muted: var(--clr-neutral-600);
// --clr-button-primary-bg: var(--clr-primary-500);
// --clr-button-primary-bg-hover: var(--clr-primary-600);
// --clr-button-primary-bg-active: var(--clr-primary-700);
// --clr-button-primary-bg-disabled: var(--clr-neutral-300);
// --clr-button-primary-text: var(--clr-neutral-100);
// --clr-button-secondary-bg: var(--clr-secondary-200);
// --clr-button-secondary-bg-hover: var(--clr-secondary-300);
// --clr-button-secondary-text: var(--clr-neutral-900);
```

### 📝 Variants Handling

The `generate-theme` mixin has special handling for the `variants` key to keep CSS variable names clean.

**Special key handling:**

- `_` key → base variable (`--clr-button-bg`)
- `variants` key → **skipped in naming**, processes nested variants directly
- Other maps → standard recursive processing with updated prefix
- Other values → leaf variables

**Example with variants:**

```scss
$theme: (
	button: (
		bg: (
			_: gray,
			hover: lightgray
		),
		text: (_: black),
		variants: (
			primary: (
				bg: (_: blue, hover: darkblue),
				text: (_: white)
			),
			danger: (
				bg: (_: red),
				text: (_: white)
			)
		)
	)
);

@include generate-theme($theme);
```

**Generated CSS:**

```css
/* Base button */
--clr-button-bg: gray;
--clr-button-bg-hover: lightgray;
--clr-button-text: black;

/* Primary variant - NOTE: NO 'variants' in name! */
--clr-button-primary-bg: blue;
--clr-button-primary-bg-hover: darkblue;
--clr-button-primary-text: white;

/* Danger variant */
--clr-button-danger-bg: red;
--clr-button-danger-text: white;
```

**Why skip `variants` in naming?**

Without special handling, you'd get:
- `--clr-button-variants-primary-bg` ❌ Too long
- `--clr-button-primary-bg` ✅ Clean and semantic

**Usage in CSS:**

```scss
.button {
	background: var(--clr-button-bg);
	color: var(--clr-button-text);
	
	&:hover {
		background: var(--clr-button-bg-hover);
	}
	
	&--primary {
		background: var(--clr-button-primary-bg);
		color: var(--clr-button-primary-text);
		
		&:hover {
			background: var(--clr-button-primary-bg-hover);
		}
	}
	
	&--danger {
		background: var(--clr-button-danger-bg);
		color: var(--clr-button-danger-text);
	}
}
```

**Best practices with variants:**

✅ **Do:**
- Use `variants` for alternative component styles
- Keep variant names semantic (`primary`, `secondary`, `danger`)
- Include states inside variants when needed

❌ **Don't:**
- Nest `variants` inside `variants` (too deep)
- Use `variants` for simple states (use direct nesting)
- Create too many variants (3-5 is usually enough)

```scss
// ✅ Good: Variants with states
button: (
	bg: (_: ..., hover: ...),
	variants: (
		primary: (
			bg: (_: ..., hover: ...),
			text: (_: ...)
		)
	)
)

// ❌ Bad: States as variants
button: (
	variants: (
		hover: (bg: (...)),  // Wrong! Use direct nesting
		active: (bg: (...))
	)
)

// ❌ Bad: Nested variants
button: (
	variants: (
		primary: (
			variants: (  // Too deep!
				outlined: (...)
			)
		)
	)
)
```

### ✔️ Best practices

- ✅ **Do:** Validate themes before generation in development
- ✅ **Do:** Use semantic component names (`header`, `button-primary`)
- ✅ **Do:** Include `_` base value when element needs default state
- ✅ **Do:** Group related states together (`bg` with all its variants)
- ❌ **Don't:** Use technical names like `div1`, `section2`
- ❌ **Don't:** Create too deep nesting (3-4 levels max)
- ❌ **Don't:** Mix semantics (`button-hover` should be `button: { bg: { hover } }`)

```scss
// ✅ Good: Semantic structure
$theme: (
	button: (
		primary: (
			bg: (
				_: ...,
				hover: ...,
				active: ...
			),
			text: (
				_: ...
			)
		)
	)
);

// ❌ Bad: Flat structure losing context
$theme: (
	'button-primary-bg': ...,
	'button-primary-bg-hover': ...,
	'button-primary-text': ...
);

// ❌ Bad: Too deep nesting
$theme: (
	section: (
		container: (
			row: (
				column: (
					element: (
						bg: (
							_: ...
						) // Too deep!
					)
				)
			)
		)
	)
);
```

## validate-theme

**Purpose:** Validate theme structure against schema, ensuring required keys are present.

**Location:** `styles/core/mixins/_validate-theme.scss`

### ✍️ Signature

```scss
@mixin validate-theme($theme, $schema, $path: null);
```

### 🧩 Parameters

- `$theme` (Map) - Theme to validate
- `$schema` (Map) - Required structure from schema
- `$path` (String | Null, optional) - Internal recursion path (auto-generated, don't pass manually)

### 🧠 How it works

1. **Schema iteration:** Loops through required keys in schema
2. **Existence check:** Verifies each required key exists in theme, throws error with full path if missing
3. **Path tracking:** Builds dot-notation path (`button.bg.text`) for clear error messages
4. **Recursive validation:** For nested maps, validates structure recursively
5. **Type safety:** Ensures both schema value and theme value are maps before recursing

**Key points:**
- Only validates **structure** (presence of required keys)
- Does NOT validate state names (hover, active, etc.) - any state names are allowed
- Does NOT validate variant names - any variant names are allowed
- Does NOT validate values or CSS correctness
- Errors stop compilation, making structural issues impossible to miss

### 🚀 Usage

```scss
@use '@/styles/themes/schema' as *;
@use '@/styles/core/mixins/validate-theme' as *;

// Validate before generating
@include validate-theme($light, $theme-schema);

// Then generate
:root {
	@include generate-theme($light);
}
```

### 📋 Examples

**Valid theme (passes validation):**

```scss
// Schema
$theme-schema: (
	button: (
		bg: (),
		text: ()
	),
	card: (
		bg: ()
	)
);

// Theme
$valid: (
	button: (
		bg: (_: ...),
		text: (_: ...)
	),
	card: (
		bg: (_: ...)
	)
);

@include validate-theme($valid, $theme-schema);
// ✅ Passes
```

**Invalid theme (validation error):**

```scss
// Schema
$theme-schema: (
	button: (
		bg: (),
		text: ()
	)
);

// Theme
$invalid: (
	button: (
		bg: (_: ...)
		// Missing: text
	)
);

@include validate-theme($invalid, $theme-schema);
// ❌ Error: Missing required key: button.text
```

**Theme with custom states (valid):**

```scss
// Schema
$theme-schema: (
	button: (
		bg: (),
		text: ()
	)
);

// Theme with custom state names
$custom-states: (
	button: (
		bg: (
			_: ...,
			hovr: ...,           // Custom state name - OK!
			pressed: ...,        // Custom state name - OK!
			spinning: ...        // Custom state name - OK!
		),
		text: (_: ...)
	)
);

@include validate-theme($custom-states, $theme-schema);
// ✅ Passes - state names are not validated
```

**Theme with variants (valid):**

```scss
// Schema (same)
$theme-schema: (
	button: (
		bg: (),
		text: ()
	)
);

// Theme with variants
$with-variants: (
	button: (
		bg: (_: ...),
		text: (_: ...),
		variants: (
			mega: (              // Custom variant - OK!
				bg: (_: ...),
				text: (_: ...)
			)
		)
	)
);

@include validate-theme($with-variants, $theme-schema);
// ✅ Passes - variant names are not validated
```

### ✔️ Best practices

- ✅ **Do:** Run validation in development only
- ✅ **Do:** Fix errors immediately (missing required keys)
- ✅ **Do:** Keep schema minimal (only truly required sections)
- ✅ **Do:** Use any state names that make sense for your project
- ✅ **Do:** Use any variant names that match your design system
- ❌ **Don't:** Skip validation (catches structural errors early)
- ❌ **Don't:** Run validation in production builds
- ❌ **Don't:** Add too many required keys to schema

```scss
// ✅ Good: Development-only validation
@if $environment == 'development' {
	@include validate-theme($theme, $theme-schema);
}

:root {
	@include generate-theme($theme);
}

// ❌ Bad: Always validating (slow in production)
@include validate-theme($theme, $theme-schema);
:root {
	@include generate-theme($theme);
}
```

### 📌 What's validated

✅ **Validated:**
- Presence of required keys from schema
- Nested structure matches schema

❌ **NOT validated:**
- State names (`hover`, `active`, custom names) - completely flexible
- Variant names (`primary`, `danger`, custom names) - completely flexible
- Presence of `_` base value (optional by design)
- Property values (doesn't check if CSS is valid)
- Value references (doesn't check if `var(--clr-invalid)` exists)

### ❌ Common mistakes

**Not updating schema when adding sections:**

```scss
// ❌ Bad: Added sidebar to theme but not schema
$theme: (
	button: (...),
	sidebar: (...)  // Not in schema - won't be validated!
);

// ✅ Good: Update schema first
$theme-schema: (
	button: (...),
	sidebar: (...)  // Now validated
);
```

**Expecting state validation:**

```scss
// ❌ Wrong expectation: "This will catch typos in state names"
$theme: (
	button: (
		bg: (
			_: ...,
			hovr: ...  // Typo, but WON'T be caught - states not validated
		)
	)
);

// ✅ Correct: Only structure is validated
// State names are your choice - use any names you want
```