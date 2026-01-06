## 🖋️ Typography tokens

Define font families, weights, and sizes for consistent typography across your project. The system uses a scalable approach with a base font size and multipliers, making it easy to adjust the entire type scale at once.
```scss
// tokens/_typography.scss

// Font families for body text and headings
$font-families: (
	primary: 'JetBrains, sans-serif',  // use your font-family
	accent: 'Tektur, sans-serif'       // use your font-family
);

// Font weight scale
$font-weights: (
	light: 300,
	regular: 400,
	medium: 500,
	bold: 700,
	extra-bold: 900
);

// Base font size (change this to scale entire system)
$base-font-size: 16px;

// Font sizes calculated from base using multipliers
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 1.875,  // 30px
	h2: $base-font-size * 1.5,    // 24px
	h3: $base-font-size * 1.25,   // 20px
	h4: $base-font-size * 1.125,  // 18px
	h5: $base-font-size * 1,      // 16px
	h6: $base-font-size * 0.875   // 14px
);
```

> 💡 **Note:** Font sizes are automatically converted to rem in `base/_variables.scss`

<br>

### Generated CSS variables
```css
:root {
	/* Font families */
	--ff-primary: 'JetBrains, sans-serif';
	--ff-accent: 'Tektur, sans-serif';

	/* Font weights */
	--fw-light: 300;
	--fw-regular: 400;
	--fw-medium: 500;
	--fw-bold: 700;
	--fw-extra-bold: 900;

	/* Font sizes (converted to rem) */
	--fs-default: 1rem;      /* 16px */
	--fs-h1: 1.875rem;       /* 30px */
	--fs-h2: 1.5rem;         /* 24px */
	--fs-h3: 1.25rem;        /* 20px */
	--fs-h4: 1.125rem;       /* 18px */
	--fs-h5: 1rem;           /* 16px */
	--fs-h6: 0.875rem;       /* 14px */
}
```

<br>

### Usage examples
```scss
body {
	font-family: var(--ff-primary);
	font-size: var(--fs-default);
	font-weight: var(--fw-regular);
}

h1 {
	font-family: var(--ff-accent);  // Accent font for headings
	font-size: var(--fs-h1);
	font-weight: var(--fw-bold);
}

h2 {
	font-family: var(--ff-accent);
	font-size: var(--fs-h2);
	font-weight: var(--fw-medium);
}

.small-text {
	font-size: var(--fs-h6);
	font-weight: var(--fw-light);
}

.emphasis {
	font-weight: var(--fw-extra-bold);
}
```

<br>

### Customization examples

**Change font families:**
```scss
// Custom fonts
$font-families: (
	primary: 'Inter, system-ui, sans-serif',
	accent: 'Playfair Display, Georgia, serif'
);

// Single font family
$font-families: (
	primary: 'Roboto, sans-serif',
	accent: 'Roboto, sans-serif'  // Same as primary
);
```

**Adjust font weights:**
```scss
// Add more weights
$font-weights: (
	thin: 100,
	light: 300,
	regular: 400,
	medium: 500,
	semibold: 600,  // New
	bold: 700,
	extra-bold: 900
);

// Minimal weights
$font-weights: (
	regular: 400,
	bold: 700
);
```

**Scale entire typography system:**
```scss
// Larger base → all headings scale proportionally
$base-font-size: 18px;

// Result:
// default: 18px (18 * 1)
// h1: 33.75px (18 * 1.875)
// h2: 27px (18 * 1.5)
// h3: 22.5px (18 * 1.25)
// h4: 20.25px (18 * 1.125)
// h5: 18px (18 * 1)
// h6: 15.75px (18 * 0.875)
```

**Adjust heading hierarchy:**
```scss
// More dramatic scale
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 2.5,   // 40px - much larger
	h2: $base-font-size * 2,     // 32px
	h3: $base-font-size * 1.5,   // 24px
	h4: $base-font-size * 1.25,  // 20px
	h5: $base-font-size * 1,     // 16px
	h6: $base-font-size * 0.875  // 14px
);

// More subtle scale
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 1.5,    // 24px - closer to body
	h2: $base-font-size * 1.375,  // 22px
	h3: $base-font-size * 1.25,   // 20px
	h4: $base-font-size * 1.125,  // 18px
	h5: $base-font-size * 1,      // 16px
	h6: $base-font-size * 0.875   // 14px
);
```

**Add custom sizes:**
```scss
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 1.875,
	h2: $base-font-size * 1.5,
	h3: $base-font-size * 1.25,
	h4: $base-font-size * 1.125,
	h5: $base-font-size * 1,
	h6: $base-font-size * 0.875,
	xs: $base-font-size * 0.75,   // New: 12px
	sm: $base-font-size * 0.875,  // New: 14px
	lg: $base-font-size * 1.125,  // New: 18px
	xl: $base-font-size * 1.25    // New: 20px
);
```

<br>

### Best practices

**Font families:**

- Use `primary` for body text, paragraphs, and UI elements
- Use `accent` for headings and emphasis (optional - can be same as primary)
- Always provide fallback fonts: `'YourFont, system-ui, sans-serif'`

**Font weights:**

- `light` (300): Subheadings, captions
- `regular` (400): Body text, default
- `medium` (500): Slight emphasis, navigation
- `bold` (700): Headings, strong emphasis
- `extra-bold` (900): Display text, hero sections

**Font sizes:**

- Keep `$base-font-size` at 16px for accessibility (browser default)
- Use multipliers between 1.1-2.5 for good hierarchy
- Maintain consistent ratio between sizes (e.g., 1.2x scale)
- Test readability on different screen sizes

**Common patterns:**
```scss
// Consistent headings
h1, h2, h3, h4, h5, h6 {
	font-family: var(--ff-accent);
	font-weight: var(--fw-bold);
	line-height: 1.2;
}

// Responsive typography
.hero-title {
	font-size: var(--fs-h3);  // 20px on mobile

	@include breakpoint('md', true) {
		font-size: var(--fs-h1);  // 30px on desktop
	}
}

// Body text variants
.body {
	font-size: var(--fs-default);
	font-weight: var(--fw-regular);
}

.body-large {
	font-size: var(--fs-h5);
	font-weight: var(--fw-regular);
}

.body-small {
	font-size: var(--fs-h6);
	font-weight: var(--fw-regular);
}
```