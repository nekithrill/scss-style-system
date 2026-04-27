> 📁 **Location:** `styles/config/_variables.scss`
> 🎯 **Scope:** CSS custom properties generation
> 🏷️ **Type:** Basic

# 🏭 Variables generation

Central configuration that generates all CSS custom properties from design tokens. This is the single place that controls what variables get output.

## ⚙️ Configuration

```scss
// styles/config/_variables.scss

@use '../tokens/colors' as *;
@use '../tokens/typography' as *;
@use '../tokens/spacing' as *;
@use '../tokens/borders' as *;
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
	line-heights: (
		map: $line-heights,
		prefix: 'lh'
	),
	letter-spacings: (
		map: $letter-spacings,
		prefix: 'ls'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	),
	border-radius: (
		map: $border-radius,
		prefix: 'br',
		transform: 'rem'
	),
	border-width: (
		map: $border-width,
		prefix: 'bw'
	),
	shadows: (
		map: $shadows,
		prefix: 'shadow'
	),
	duration: (
		map: $duration,
		prefix: 'dur'
	),
	easing: (
		map: $easing,
		prefix: 'tf'
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

Each group requires `map` and `prefix`. `transform: 'rem'` converts px values to rem — use it for spacing, sizing, and typography. Do not use it for colors, shadows, z-index, or timing values.

## 🔧 Customization

**Remove unused group:**

```scss
$base-tokens: (
	colors: (...),
	spacing: (...),
	// Remove shadows, animations, etc. if not needed
);
```

**Add custom token group:**

```scss
@use '../tokens/my-tokens' as *;

$base-tokens: (
	// ...existing groups
	my-tokens: (
		map: $my-map,
		prefix: 'my',
		transform: 'rem' // optional
	)
);
```

**Change prefix:**

```scss
colors: (
	map: $all-colors,
	prefix: 'color' // Instead of 'clr'
),
```