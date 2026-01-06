## 🎨 Color tokens

Define color palettes using any CSS color format (HEX, RGB, HSL, OKLCH). OKLCH is recommended for perceptual uniformity and predictable lightness progression, but you can use whatever format works best for your project.
```scss
// tokens/_colors.scss

// PRIMARY - Brand colors, accents, interactive elements
// Range: 100 (lightest) → 900 (darkest)
// Format: Use any CSS color format (HEX, RGB, HSL, OKLCH)
$primary: (
	100: oklch(95% 0.06 270deg),
	200: oklch(85% 0.1 270deg),
	300: oklch(75% 0.14 270deg),
	400: oklch(65% 0.17 270deg),
	500: oklch(60% 0.2 270deg),   // Base brand color
	600: oklch(48% 0.2 270deg),
	700: oklch(36% 0.17 270deg),
	800: oklch(24% 0.14 270deg),
	900: oklch(12% 0.11 270deg)
);

// SECONDARY - Backgrounds, surfaces, cards
// Light-biased for subtle backgrounds
$secondary: (
	100: oklch(99% 0 248deg),
	200: oklch(97% 0 248deg),
	300: oklch(95% 0 248deg),
	400: oklch(92% 0 248deg),
	500: oklch(88% 0 248deg),
	600: oklch(82% 0.01 248deg),
	700: oklch(74% 0.02 249deg),
	800: oklch(64% 0.03 249deg),
	900: oklch(52% 0.04 249deg)
);

// NEUTRAL - Text, borders, icons, dividers
// Low chroma for true neutral grays
$neutral: (
	100: oklch(96% 0.01 220deg),
	200: oklch(85% 0.02 220deg),
	300: oklch(75% 0.02 220deg),
	400: oklch(65% 0.03 220deg),
	500: oklch(56% 0.04 220deg),
	600: oklch(48% 0.03 220deg),
	700: oklch(39% 0.03 220deg),
	800: oklch(30% 0.02 220deg),
	900: oklch(20% 0.01 220deg)
);

// SUCCESS - Positive feedback, confirmations
// Keys: bg (alert background), border (outline), solid (button), text (label)
$success: (
	bg: oklch(95% 0.05 160deg),
	border: oklch(70% 0.12 160deg),
	solid: oklch(50% 0.15 160deg),
	text: oklch(30% 0.15 160deg)
);

// WARNING - Alerts, cautionary messages
$warning: (
	bg: oklch(95% 0.04 80deg),
	border: oklch(75% 0.12 75deg),
	solid: oklch(77% 0.16 70deg),
	text: oklch(30% 0.12 70deg)
);

// DANGER - Errors, destructive actions
$danger: (
	bg: oklch(95% 0.04 20deg),
	border: oklch(70% 0.12 25deg),
	solid: oklch(64% 0.21 25deg),
	text: oklch(30% 0.15 25deg)
);

// INFO - Information, tips, neutral notifications
$info: (
	bg: oklch(95% 0.04 260deg),
	border: oklch(70% 0.11 260deg),
	solid: oklch(62% 0.19 260deg),
	text: oklch(30% 0.15 260deg)
);

// All colors map for CSS variable generation
$all-colors: (
	'primary': $primary,
	'secondary': $secondary,
	'neutral': $neutral,
	'success': $success,
	'warning': $warning,
	'danger': $danger,
	'info': $info
);
```

<br>

### Generated CSS variables
```css
/* Nested palettes (100-900) */
--clr-primary-100: oklch(95% 0.06 270deg);
--clr-primary-500: oklch(60% 0.2 270deg);
--clr-primary-900: oklch(12% 0.11 270deg);

/* Semantic colors (bg, border, solid, text) */
--clr-success-bg: oklch(95% 0.05 160deg);
--clr-success-solid: oklch(50% 0.15 160deg);
--clr-danger-text: oklch(30% 0.15 25deg);
```

<br>

### Usage examples
```scss
// Direct usage with generated variables
.button {
	background-color: var(--clr-primary-500);
	color: var(--clr-neutral-100);
	border: 1px solid var(--clr-primary-600);

	&:hover {
		background-color: var(--clr-primary-600);
	}
}

// Alert components
.alert-success {
	background-color: var(--clr-success-bg);
	border: 1px solid var(--clr-success-border);
	color: var(--clr-success-text);
}

// Text hierarchy
.heading {
	color: var(--clr-neutral-900); // Dark text
}

.body-text {
	color: var(--clr-neutral-700); // Medium text
}

.caption {
	color: var(--clr-neutral-500); // Light text
}

// Usage in theme modules
// Reference color tokens to create semantic theme variables
$dark: (
	header: (
		bg: (
			_: var(--clr-neutral-900), // Dark background
			hover: var(--clr-neutral-800)
		),
		text: (
			_: var(--clr-neutral-100)  // Light text
		)
	),
	main: (
		bg: (
			_: var(--clr-neutral-800),
			hover: var(--clr-neutral-700)
		),
		text: (
			_: var(--clr-neutral-200)
		)
	),
	button: (
		primary: (
			_: var(--clr-primary-600),
			hover: var(--clr-primary-500)
		)
	)
);
```

<br>

### Color format options

You can use any CSS color format that suits your workflow:
```scss
// HEX format
$primary: (
	100: #f5f3ff,
	500: #8b5cf6,
	900: #3b0764
);

// RGB format
$primary: (
	100: rgb(245, 243, 255),
	500: rgb(139, 92, 246),
	900: rgb(59, 7, 100)
);

// HSL format
$primary: (
	100: hsl(270, 100%, 98%),
	500: hsl(270, 91%, 65%),
	900: hsl(270, 87%, 21%)
);

// OKLCH format (recommended)
$primary: (
	100: oklch(95% 0.06 270deg),
	500: oklch(60% 0.2 270deg),
	900: oklch(12% 0.11 270deg)
);
```

<br>

### Why OKLCH? (optional, but recommended)

OKLCH (Oklab Lightness Chroma Hue) provides perceptually uniform color manipulation:

**Format:** `oklch(L% C H)`

- **L (Lightness):** 0% (black) → 100% (white)
- **C (Chroma):** 0 (gray) → 0.4+ (vivid) - saturation/intensity
- **H (Hue):** 0°-360° - color wheel position

**Benefits over HSL/RGB:**

- Consistent perceived brightness across hues
- Predictable lightness progression (90% always looks lighter than 80%)
- Better color mixing and interpolation
- Wider color gamut support

**When to use OKLCH:**

- Building design systems with many color variations
- Need consistent visual weight across different hues
- Want predictable lightness scales

**When to stick with HEX/RGB/HSL:**

- Working with existing brand colors
- Team is unfamiliar with OKLCH
- Simple projects with few color variations

<br>

### Customization examples
```scss
// Using HEX colors (from existing brand)
$primary: (
	100: #e0e7ff,
	200: #c7d2fe,
	300: #a5b4fc,
	400: #818cf8,
	500: #6366f1,   // Brand color
	600: #4f46e5,
	700: #4338ca,
	800: #3730a3,
	900: #312e81
);

// Mix formats (if needed)
$primary: (
	100: #e0e7ff,                 // From brand guidelines
	500: oklch(60% 0.2 270deg),   // Generated for consistency
	900: rgb(49, 46, 129)         // From existing codebase
);

// Add accent color
$accent: (
	100: #ffedd5,
	500: #f97316,
	900: #7c2d12
);

$all-colors: (
	// ... existing colors
	'accent': $accent // Add to generation
);

// Custom semantic color
$premium: (
	bg: white,  // White background
	solid: gold, // Gold button
	text: brown  // Brown text
);

$all-colors: (
	// ... existing colors
	'premium': $premium
);
```

<br>

### Color palette structure

**Scale-based (100-900):**

- Use for colors with many variations (primary, neutral)
- Provides full tonal range for different contexts
- 500 typically represents base/default shade

**Semantic (bg, border, solid, text):**

- Use for state colors (success, warning, danger, info)
- Each key serves specific UI purpose
- Maintains consistent visual hierarchy

<br>

### Removing unused colors
```scss
// Minimal setup (only brand + neutrals)
$all-colors: (
	'primary': $primary,
	'neutral': $neutral // Removed: secondary, success, warning, danger, info
);

// Dark theme only
$all-colors: (
	'primary': $primary,
	'neutral': $neutral,
	'danger': $danger // Keep for errors
	// Removed: secondary, success, warning, info
);
```

<br>

### Best practices

**Lightness values (if using OKLCH):**

- 95%+ for backgrounds
- 70-85% for borders/dividers
- 50-65% for interactive elements
- 20-40% for text

**General color guidelines:**

- Use lighter shades (100-300) for backgrounds
- Use medium shades (400-600) for interactive elements
- Use darker shades (700-900) for text
- Test colors in both light and dark themes (if you use them)