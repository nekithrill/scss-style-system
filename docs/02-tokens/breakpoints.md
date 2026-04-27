> 📁 **Location:** `styles/tokens/_breakpoints.scss`
> 🎯 **Scope:** Responsive breakpoints
> 🏷️ **Type:** Token

# 📱 Breakpoint tokens

Screen width thresholds for the `breakpoint` mixin. Not converted to CSS variables — used at compile time only.

## ⚡️ Usage

```scss
.container {
	padding: var(--sp-4);

	// Mobile-first (default): applies when viewport ≥ breakpoint
	@include breakpoint('lg') {
		padding: var(--sp-6);
	}
}

.grid {
	grid-template-columns: 1fr;

	@include breakpoint('md') {
		grid-template-columns: repeat(2, 1fr);
	}

	@include breakpoint('lg') {
		grid-template-columns: repeat(4, 1fr);
	}
}
```

## ⚙️ Configuration

```scss
$breakpoints: (
	'xs':  360px,   // Small phones
	'sm':  576px,   // Large phones
	'md':  768px,   // Tablets
	'lg':  1024px,  // Laptops
	'xl':  1280px,  // Desktops
	'2xl': 1536px   // Large desktops
) !default;
```

> Breakpoints are consumed by the `breakpoint` mixin and not output as CSS variables. See [Mixins](../04-mixins-and-functions/mixins.md) for usage.

## 🔧 Customization

```scss
$breakpoints: (
	'xs':  320px,  // Decreased
	'sm':  640px,  // Increased
	'md':  768px,
	'lg':  1024px,
	'xl':  1440px, // Increased
	'2xl': 1920px  // Increased
) !default;
```