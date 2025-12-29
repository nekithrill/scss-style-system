## 📱 Responsive design

Create adaptive layouts that work seamlessly across all screen sizes using breakpoint tokens and the responsive mixin system. Supports both desktop-first and mobile-first approaches.

---

### Breakpoints

```scss
// tokens/_breakpoints.scss
$breakpoints: (
	'xs': 360px,   // Extra small devices
	'sm': 576px,   // Small devices (phones)
	'md': 768px,   // Medium devices (tablets)
	'lg': 1024px,  // Large devices (desktops)
	'xl': 1280px,  // Extra large devices
	'2xl': 1536px  // 2X extra large devices
);
```

---

### Using the Breakpoint Mixin

The `breakpoint` mixin simplifies responsive design with automatic media query generation. It supports both desktop-first (max-width) and mobile-first (min-width) strategies.

> 💡 The mixin currently defaults to desktop-first approach (max-width). For mobile-first, you need to pass `true` as the second parameter. This API may be simplified in future versions to make mobile-first easier to use without the explicit flag.

#### Desktop-first (max-width)

```scss
@use '../core/mixins/breakpoint' as *;

.container {
	padding: var(--sp-4);   // Desktop: 32px

	@include breakpoint('lg') {
		padding: var(--sp-3);  // < 1024px: 24px
	}

	@include breakpoint('md') {
		padding: var(--sp-2);  // < 768px: 16px
	}
}
```

#### Mobile-first (min-width)

```scss
.container {
	padding: var(--sp-1); // Mobile: 8px

	@include breakpoint('sm', true) {
		padding: var(--sp-2); // >= 576px: 16px
	}

	@include breakpoint('lg', true) {
		padding: var(--sp-4); // >= 1024px: 32px
	}
}
```

#### Responsive grid

```scss
.grid {
	display: grid;
	gap: var(--sp-4);
	grid-template-columns: repeat(4, 1fr);

	@include breakpoint('lg') {
		grid-template-columns: repeat(3, 1fr);
	}

	@include breakpoint('md') {
		grid-template-columns: repeat(2, 1fr);
	}

	@include breakpoint('sm') {
		grid-template-columns: 1fr;
	}
}
```
