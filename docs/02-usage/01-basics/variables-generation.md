## 📦 Variables generation

Automatically generates CSS custom properties (variables) from design tokens using a centralized configuration. The system handles both nested maps (like color palettes) and flat maps (like spacing values), with optional unit transformation from pixels to rem.

> 💡 **Transform option:** Use `transform: 'rem'` for any variable group to automatically convert pixel values to rem units.

> 💡 **Default prefixes:** Every variable group has its own prefix which you can customize:
> - colors `--clr`
> - font-family `--ff`
> - font-weight `--fw`
> - font-size `--fs`
> - spacing `--sp`
> - radius `--rd`
> - shadows `--shadow`
> - duration `--dur`
> - easing `--ease`
> - delay `--delay`
> - z-index `--z`

<br>

### Token configuration
```scss
// tokens/_index.scss

@use '../tokens/colors' as *;
@use '../tokens/typography' as *;
@use '../tokens/spacing' as *;
@use '../tokens/radius' as *;
@use '../tokens/shadows' as *;
@use '../tokens/animations' as *;
@use '../tokens/z-index' as *;
@use '../core/mixins/generate-tokens' as *;

$base-tokens: (
	colors: (
		map: $all-colors,
		prefix: 'clr'
	),
	font-families: (
		map: $font-families,
		prefix: 'ff'
	),
	font-weights: (
		map: $font-weights,
		prefix: 'fw'
	),
	font-sizes: (
		map: $font-sizes,
		prefix: 'fs',
		transform: 'rem'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	),
	radius: (
		map: $radius,
		prefix: 'rd',
		transform: 'rem'
	),
	shadows: (
		map: $shadows,
		prefix: 'shadow',
	),
	duration: (
		map: $duration,
		prefix: 'dur'
	),
	easing: (
		map: $easing,
		prefix: 'ease'
	),
	delay: (
		map: $delay,
		prefix: 'delay'
	),
	z-index: (
		map: $z-index,
		prefix: 'z'
	)
);

:root {
	@include generate-tokens($base-tokens);
}
```

<br>

### How it works

The `generate-tokens` mixin processes token groups and outputs CSS variables:

**Token group structure:**
```scss
group-name: (
	map: $token-values,    // Required: source data
	prefix: 'var-prefix',  // Required: CSS variable prefix
	transform: 'rem'       // Optional: convert px to rem
);
```

**Nested maps** (e.g., colors with shades):
```scss
$colors: (
	'primary': (
		100: #e0e7ff,
		500: #6366f1
	),
	'success': (
		bg: #d1fae5,
		solid: #10b981
	)
);

// Output:
// --clr-primary-100: #e0e7ff;
// --clr-primary-500: #6366f1;
// --clr-success-bg: #d1fae5;
// --clr-success-solid: #10b981;
```

**Flat maps** (e.g., spacing, font weights):
```scss
$spacing: (
	1: 4px,
	2: 8px,
	4: 16px
);

// Output (with transform: 'rem'):
// --sp-1: 0.25rem;
// --sp-2: 0.5rem;
// --sp-4: 1rem;
```

<br>

### Adding new token groups
```scss
// 1. Create token file
// tokens/_borders.scss
$borders: (
	thin: 1px,
	medium: 2px,
	thick: 4px
);

// 2. Import and add to configuration
@use '../tokens/borders' as *;

$base-tokens: (
	// ... existing tokens
	borders: (
		map: $borders,
		prefix: 'border',
		transform: 'rem'  // Optional
	)
);

// 3. Generated output:
// --border-thin: 0.0625rem;
// --border-medium: 0.125rem;
// --border-thick: 0.25rem;
```

<br>

### Mixin reference
```scss
/// Generate CSS variables from design token maps
/// @param {Map} $tokens - Token configuration with groups

@mixin generate-tokens($tokens) {
	// Automatically detects:
	// - Nested structure (colors with shades)
	// - Flat structure (spacing, weights)
	// - Applies px-to-rem transformation when needed
}
```

**Features:**

- Auto-detects nested vs flat map structure
- Validates required keys (`map`, `prefix`)
- Optional `px` to `rem` conversion
- Consistent naming convention
- Single source of truth for design tokens