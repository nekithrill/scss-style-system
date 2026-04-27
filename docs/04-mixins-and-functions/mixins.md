> 📁 **Location:** `styles/core/mixins/`
> 🎯 **Scope:** Responsive design and token generation
> 🏷️ **Type:** Core

# ⚙️ Mixins

## breakpoint

Generate responsive media queries from breakpoint tokens.

**Location:** `styles/core/mixins/_breakpoint.scss`

### Signature

```scss
@mixin breakpoint($size, $min-width: true)
```

### Parameters

- `$size` — breakpoint key: `'xs'`, `'sm'`, `'md'`, `'lg'`, `'xl'`, `'2xl'`
- `$min-width` — `true` for mobile-first `min-width` (default), `false` for desktop-first `max-width`

### Usage

```scss
@use '@/styles/core/mixins/breakpoint' as *;

// Mobile-first (default) — applies when viewport ≥ breakpoint
.container {
	padding: var(--sp-2);

	@include breakpoint('md') {
		padding: var(--sp-4);
	}

	@include breakpoint('lg') {
		padding: var(--sp-6);
	}
}

// Desktop-first — applies when viewport ≤ breakpoint
.sidebar {
	width: 280px;

	@include breakpoint('lg', false) {
		width: 240px;
	}

	@include breakpoint('md', false) {
		display: none;
	}
}
```

**Generated CSS:**

```css
.container { padding: 1rem; }

@media (min-width: 768px) {
	.container { padding: 2rem; }
}

@media (min-width: 1024px) {
	.container { padding: 3rem; }
}
```

If an invalid breakpoint key is passed, the mixin throws a compile-time error listing available options.

---

## generate-tokens

Convert SCSS token maps to CSS custom properties.

**Location:** `styles/core/mixins/_generate-tokens.scss`

### Signature

```scss
@mixin generate-tokens($tokens)
```

### Parameters

`$tokens` — map where each group contains:

| Key | Required | Description |
|-----|----------|-------------|
| `map` | ✅ | SCSS map of token values |
| `prefix` | ✅ | CSS variable prefix |
| `transform` | — | Set to `'rem'` to convert px values |

### How it works

The mixin auto-detects map structure:

- **Flat map** → `--prefix-key`
- **Nested map** → `--prefix-group-shade`

```scss
// Flat → --sp-1, --sp-2
$spacing: (
	1: 8px, 
	2: 16px
);

// Nested → --clr-primary-100, --clr-primary-500
$all-colors: (
	'primary': (
		100: oklch(...), 
		500: oklch(...))
);
```

### Usage

```scss
@use '../core/mixins/generate-tokens' as *;

$base-tokens: (
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	),
	colors: (
		map: $all-colors,
		prefix: 'clr'
	)
);

:root {
	@include generate-tokens($base-tokens);
}
```

See [Variables generation](../03-basics/variables-generation.md) for the full configuration.