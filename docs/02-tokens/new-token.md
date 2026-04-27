> 🏷️ **Type:** Guide

# ✨ Creating custom tokens

## Create token file

```scss
// tokens/_icon-sizes.scss

$icon-sizes: (
	sm: 16px,
	md: 24px,
	lg: 32px,
	xl: 48px
) !default;
```

## Register in variables

```scss
// config/_variables.scss

@use '../tokens/icon-sizes' as *;

$base-tokens: (
	// ...existing tokens
	icon-sizes: (
		map: $icon-sizes,
		prefix: 'icon'
		// add transform: 'rem' if values should be converted
	)
);
```

## Result

```css
:root {
	--icon-sm: 16px;
	--icon-md: 24px;
	--icon-lg: 32px;
	--icon-xl: 48px;
}
```

## Nested maps

Use nested maps to generate `--prefix-group-key` variables (same pattern as colors):

```scss
$status-colors: (
	'online':  (bg: oklch(95% 0.05 160deg), dot: oklch(52% 0.17 160deg)),
	'away':    (bg: oklch(96% 0.04 80deg),  dot: oklch(70% 0.17 80deg)),
	'offline': (bg: oklch(96% 0.008 220deg), dot: oklch(56% 0.02 220deg))
) !default;

// Generates:
// --status-online-bg, --status-online-dot
// --status-away-bg, --status-away-dot
// --status-offline-bg, --status-offline-dot
```

> Use `transform: 'rem'` for spacing, sizing, and layout values. Do not use it for colors, shadows, z-index, or timing values.