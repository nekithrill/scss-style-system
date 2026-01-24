>  **📁 Location:** `styles/tokens/_breakpoints.scss`
> **📦 Type:** Token

## 📱 Breakpoint tokens

Define responsive breakpoints for consistent media queries across the project. From mobile-first to large desktop screens.

<br>

### 🧠 How it works

Breakpoint tokens define screen width thresholds used with the `breakpoint` mixin to create responsive layouts. The system uses a mobile-first scale from `xs` (360px) to `2xl` (1536px).

These tokens are consumed by the `breakpoint` mixin which generates `min-width` or `max-width` media queries depending on your approach:
- **Desktop-first** (default): Styles apply when viewport is ≤ breakpoint
- **Mobile-first**: Styles apply when viewport is ≥ breakpoint

Breakpoints are defined in pixels and converted by the browser automatically - no rem conversion needed here.

---

### 🚀 Usage

```scss
@use '@/styles/core/mixins/breakpoint' as *;

.container {
	padding: var(--sp-8);
	
	// Desktop-first: applies on tablet and smaller
	@include breakpoint('md') {
		padding: var(--sp-4);  // ≤ 768px
	}
	
	// Mobile-first: applies on desktop and larger
	@include breakpoint('lg', true) {
		padding: var(--sp-12);  // ≥ 1024px
	}
}

// Responsive grid
.grid {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: var(--sp-4);
	
	@include breakpoint('lg') {
		grid-template-columns: repeat(3, 1fr);  // ≤ 1024px
	}
	
	@include breakpoint('md') {
		grid-template-columns: repeat(2, 1fr);  // ≤ 768px
	}
	
	@include breakpoint('sm') {
		grid-template-columns: 1fr;  // ≤ 576px
	}
}
```

---

### ⚙️ Basic configuration

```scss
// tokens/_breakpoints.scss

$breakpoints: (
	'xs': 360px,   // Small phones
	'sm': 576px,   // Large phones
	'md': 768px,   // Tablets
	'lg': 1024px,  // Laptops
	'xl': 1280px,  // Desktops
	'2xl': 1536px  // Large desktops
) !default;
```

**Note:** These values are NOT converted to CSS variables. They're used directly by the `breakpoint` mixin at compile time.

---

### 🔧 Customization

```scss
// Adjust for your target devices
$breakpoints: (
	'xs': 320px,    // Very small phones
	'sm': 640px,    // Updated mobile
	'md': 768px,    // Keep tablet
	'lg': 1024px,   // Keep laptop
	'xl': 1440px,   // Larger desktop
	'2xl': 1920px   // Full HD screens
);

// Add custom breakpoints
$breakpoints: (
	// ... existing values
	'3xl': 2560px,  // 4K screens
	'print': 8.5in  // Print layout
);

// Minimal set (2-3 breakpoints)
$breakpoints: (
	'mobile': 640px,
	'tablet': 1024px,
	'desktop': 1440px
);
```

---

### ✔️ Best practices

**Choosing breakpoints:**

- Use `xs` (360px) for small phone optimizations
- Use `sm` (576px) for mobile phones in portrait
- Use `md` (768px) for tablets and small laptops
- Use `lg` (1024px) for laptops and desktops
- Use `xl` (1280px) for large desktops
- Use `2xl` (1536px) for extra-large screens

**General guidelines:**

- Start with `mobile-first` or `desktop-first`, be consistent
- Test at breakpoint boundaries (e.g., `767px`, `768px`, `769px`)
- Avoid too many breakpoints - 3-4 is usually enough
- Use content-based breakpoints when component needs it
- Don't target specific devices - design for ranges

**Common patterns:**

```scss
// Mobile-first approach (recommended)
.element {
	// Mobile styles (default)
	width: 100%;
	
	@include breakpoint('md', true) {
		width: 50%;  // Tablet and up
	}
	
	@include breakpoint('lg', true) {
		width: 33.33%;  // Desktop and up
	}
}

// Desktop-first approach
.element {
	// Desktop styles (default)
	width: 33.33%;
	
	@include breakpoint('lg') {
		width: 50%;  // Laptop and down
	}
	
	@include breakpoint('md') {
		width: 100%;  // Tablet and down
	}
}
```

---

### ❌ Common mistakes

**Don't hardcode pixel values:**
```scss
// ❌ Bad: hardcoded breakpoint
@media (max-width: 768px) {
	.element { ... }
}

// ✅ Good: use tokens
@include breakpoint('md') {
	.element { ... }
}
```

**Don't mix approaches:**
```scss
// ❌ Bad: mixing mobile-first and desktop-first
.element {
	@include breakpoint('md', true) { ... }  // Mobile-first
	@include breakpoint('lg') { ... }        // Desktop-first
}

// ✅ Good: consistent approach
.element {
	@include breakpoint('md', true) { ... }  // Both mobile-first
	@include breakpoint('lg', true) { ... }
}
```

**Don't create device-specific breakpoints:**
```scss
// ❌ Bad: targeting specific devices
$breakpoints: (
	'iphone-se': 375px,
	'iphone-pro': 428px,
	'ipad-mini': 768px
);

// ✅ Good: range-based breakpoints
$breakpoints: (
	'sm': 576px,   // Covers most phones
	'md': 768px,   // Covers tablets
	'lg': 1024px   // Covers laptops
);
```