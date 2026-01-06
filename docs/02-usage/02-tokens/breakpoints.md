## 📱 Breakpoint tokens

Define screen width breakpoints for responsive design. Used with the [`breakpoint` mixin](../01-basics/core.md) to create consistent media queries across the project.
```scss
// tokens/_breakpoints.scss

// Breakpoint values for responsive design
$breakpoints: (
	'xs': 360px,   // Extra small devices (small phones)
	'sm': 576px,   // Small devices (phones in landscape)
	'md': 768px,   // Medium devices (tablets)
	'lg': 1024px,  // Large devices (desktops, laptops)
	'xl': 1280px,  // Extra large devices (large desktops)
	'2xl': 1536px  // 2X extra large devices (wide screens)
);
```

<br>

### Customization examples
```scss
// Adjust breakpoint values
$breakpoints: (
	'xs': 320px,   // Smaller phones
	'sm': 640px,   // Adjusted
	'md': 768px,
	'lg': 1024px,
	'xl': 1440px,  // Wider desktops
	'2xl': 1920px  // Full HD screens
);

// Add custom breakpoints
$breakpoints: (
	// ... existing breakpoints
	'tablet-portrait': 600px,  // Specific tablet size
	'laptop': 1366px,          // Common laptop resolution
	'4k': 2560px               // 4K displays
);
```

<br>

### Usage with breakpoint mixin
```scss
// Desktop-first (default)
.container {
	padding: 2rem;

	@include breakpoint('lg') {
		padding: 1.5rem; // ≤ 1024px
	}

	@include breakpoint('md') {
		padding: 1rem;   // ≤ 768px
	}
}

// Mobile-first
.grid {
	display: grid;
	grid-template-columns: 1fr;

	@include breakpoint('sm', true) {
		grid-template-columns: repeat(2, 1fr); // ≥ 576px
	}

	@include breakpoint('lg', true) {
		grid-template-columns: repeat(3, 1fr); // ≥ 1024px
	}
}
```

**Generated CSS:**
```css
/* Desktop-first (default) */
.container {
	padding: 2rem;
}

@media (max-width: 1024px) {
	.container {
		padding: 1.5rem;
	}
}

@media (max-width: 768px) {
	.container {
		padding: 1rem;
	}
}

/* Mobile-first */
.grid {
	display: grid;
	grid-template-columns: 1fr;
}

@media (min-width: 576px) {
	.grid {
		grid-template-columns: repeat(2, 1fr);
	}
}

@media (min-width: 1024px) {
	.grid {
		grid-template-columns: repeat(3, 1fr);
	}
}
```

For detailed mixin documentation and advanced usage patterns, see [Mixins & functions](../01-basics/core.md).