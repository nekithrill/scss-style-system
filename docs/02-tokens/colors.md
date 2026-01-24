> **📁 Location:** `styles/tokens/_colors.scss`
> **📦 Type:** Token

## 🎨 Color tokens

Define the complete color palette using OKLCH color space for perceptual uniformity and consistent lightness across hues.

<br>

### 🧠 How it works

Color tokens are organized into two categories:

**Palette colors** (`primary`, `secondary`, `neutral`) use a 100-900 scale where:
- Lower numbers (100-300) are lighter shades
- Middle range (400-600) are mid-tones  
- Higher numbers (700-900) are darker shades
- The scale provides 9 shades for maximum flexibility

**Semantic colors** (`success`, `warning`, `danger`, `info`) use role-based keys:
- `bg`: Background color for alerts/notifications
- `border`: Border/outline color
- `solid`: Solid fill color (buttons, badges)
- `text`: Text color for high contrast

All colors use **OKLCH format** (`oklch(lightness chroma hue)`) which provides:
- Perceptually uniform lightness (50% looks 50% bright across all hues)
- Wider color gamut than RGB/HSL
- Better for programmatic color manipulation
- Consistent chroma (saturation) control

Colors are generated as CSS custom properties with the `--clr-` prefix:
- `--clr-primary-500`, `--clr-neutral-100`, etc.
- `--clr-success-bg`, `--clr-danger-text`, etc.

---

### 🚀 Usage

```scss
// Using palette colors directly
.button {
	background: var(--clr-primary-500);
	color: var(--clr-neutral-100);
	border: 1px solid var(--clr-primary-600);
	
	&:hover {
		background: var(--clr-primary-600);
	}
}

// Using semantic colors
.alert-success {
	background: var(--clr-success-bg);
	border: 2px solid var(--clr-success-border);
	color: var(--clr-success-text);
}

.alert-danger {
	background: var(--clr-danger-bg);
	border: 2px solid var(--clr-danger-border);
	color: var(--clr-danger-text);
}

// Text with accent
.heading {
	color: var(--clr-neutral-900);
	
	.accent {
		color: var(--clr-primary-500);
	}
}

// Card with neutral colors
.card {
	background: var(--clr-secondary-100);
	border: 1px solid var(--clr-neutral-200);
	color: var(--clr-neutral-800);
}
```

---

### ⚙️ Basic configuration

```scss
// tokens/_colors.scss

// Hues for general colors
$primary-hue: 270deg !default;      // Purple/violet
$secondary-hue: 248deg !default;    // Blue-ish neutrals
$neutral-hue: 220deg !default;      // Cool gray

// Hues for semantic colors  
$success-hue: 160deg !default;      // Green
$warning-hue: 80deg !default;       // Yellow/amber
$danger-hue: 25deg !default;        // Red/orange
$info-hue: 260deg !default;         // Blue/purple

// PRIMARY - Brand colors, accents, interactive elements
$primary: (
	100: oklch(95% 0.06 $primary-hue),
	200: oklch(85% 0.1 $primary-hue),
	300: oklch(75% 0.14 $primary-hue),
	400: oklch(65% 0.17 $primary-hue),
	500: oklch(60% 0.2 $primary-hue),   // Main brand color
	600: oklch(48% 0.2 $primary-hue),
	700: oklch(36% 0.17 $primary-hue),
	800: oklch(24% 0.14 $primary-hue),
	900: oklch(12% 0.11 $primary-hue)
) !default;

// SECONDARY - Backgrounds, surfaces, cards
$secondary: (
	100: oklch(99% 0 $secondary-hue),
	200: oklch(97% 0 $secondary-hue),
	300: oklch(95% 0 $secondary-hue),
	400: oklch(92% 0 $secondary-hue),
	500: oklch(88% 0 $secondary-hue),
	600: oklch(82% 0.01 $secondary-hue),
	700: oklch(74% 0.02 $secondary-hue),
	800: oklch(64% 0.03 $secondary-hue),
	900: oklch(52% 0.04 $secondary-hue)
) !default;

// NEUTRAL - Text, borders, icons, dividers
$neutral: (
	100: oklch(96% 0.01 $neutral-hue),
	200: oklch(85% 0.02 $neutral-hue),
	300: oklch(75% 0.02 $neutral-hue),
	400: oklch(65% 0.03 $neutral-hue),
	500: oklch(56% 0.04 $neutral-hue),
	600: oklch(48% 0.03 $neutral-hue),
	700: oklch(39% 0.03 $neutral-hue),
	800: oklch(30% 0.02 $neutral-hue),
	900: oklch(20% 0.01 $neutral-hue)
) !default;

// SUCCESS - Positive feedback, confirmations
$success: (
	bg: oklch(95% 0.05 $success-hue),
	border: oklch(70% 0.12 $success-hue),
	solid: oklch(50% 0.15 $success-hue),
	text: oklch(30% 0.15 $success-hue)
) !default;

// WARNING - Alerts, cautionary messages
$warning: (
	bg: oklch(95% 0.04 $warning-hue),
	border: oklch(75% 0.12 $warning-hue),
	solid: oklch(77% 0.16 $warning-hue),
	text: oklch(30% 0.12 $warning-hue)
) !default;

// DANGER - Errors, destructive actions
$danger: (
	bg: oklch(95% 0.04 $danger-hue),
	border: oklch(70% 0.12 $danger-hue),
	solid: oklch(64% 0.21 $danger-hue),
	text: oklch(30% 0.15 $danger-hue)
) !default;

// INFO - Information, tips, neutral notifications
$info: (
	bg: oklch(95% 0.04 $info-hue),
	border: oklch(70% 0.11 $info-hue),
	solid: oklch(62% 0.19 $info-hue),
	text: oklch(30% 0.15 $info-hue)
) !default;

// All colors map for CSS variable generation
$all-colors: (
	'primary': $primary,
	'secondary': $secondary,
	'neutral': $neutral,
	'success': $success,
	'warning': $warning,
	'danger': $danger,
	'info': $info
) !default;
```

**Generated CSS variables:**
```css
:root {
	/* Primary palette */
	--clr-primary-100: oklch(95% 0.06 270deg);
	--clr-primary-500: oklch(60% 0.2 270deg);
	--clr-primary-900: oklch(12% 0.11 270deg);
	
	/* Neutral palette */
	--clr-neutral-100: oklch(96% 0.01 220deg);
	--clr-neutral-500: oklch(56% 0.04 220deg);
	--clr-neutral-900: oklch(20% 0.01 220deg);
	
	/* Semantic colors */
	--clr-success-bg: oklch(95% 0.05 160deg);
	--clr-success-border: oklch(70% 0.12 160deg);
	--clr-success-solid: oklch(50% 0.15 160deg);
	--clr-success-text: oklch(30% 0.15 160deg);
	
	/* ... and so on for all colors */
}
```

---

### 🔧 Customization

**Change brand hue:**
```scss
// Make primary color blue instead of purple
$primary-hue: 240deg;  // Blue hue

// Colors automatically update across all shades
$primary: (
	100: oklch(95% 0.06 $primary-hue),  // Light blue
	500: oklch(60% 0.2 $primary-hue),   // Mid blue
	900: oklch(12% 0.11 $primary-hue)   // Dark blue
);
```

**Adjust chroma (saturation):**
```scss
// More vibrant primary colors
$primary: (
	500: oklch(60% 0.25 $primary-hue),  // Higher chroma = more saturated
	// ... other shades
);

// More muted neutral colors
$neutral: (
	500: oklch(56% 0.01 $neutral-hue),  // Lower chroma = less saturated
	// ... other shades
);
```

**Add custom palette:**
```scss
// Add accent color
$accent-hue: 340deg;  // Pink/magenta

$accent: (
	100: oklch(95% 0.06 $accent-hue),
	500: oklch(60% 0.2 $accent-hue),
	900: oklch(12% 0.11 $accent-hue)
) !default;

// Include in generation
$all-colors: (
	'primary': $primary,
	'secondary': $secondary,
	'neutral': $neutral,
	'accent': $accent,  // Add custom palette
	// ... semantic colors
);
```

---

### ✔️ Best practices

**Color usage:**

- Use `primary` for brand elements, CTAs, interactive components
- Use `secondary` for backgrounds, surfaces, subtle elements
- Use `neutral` for text, borders, icons, dividers
- Use semantic colors (`success`, `warning`, `danger`, `info`) for feedback

**Contrast guidelines:**

- `100-300`: Light backgrounds, subtle surfaces
- `400-600`: Mid-tones, borders, disabled states
- `700-900`: Text, icons, high contrast elements

**Accessibility:**

- Ensure 4.5:1 contrast ratio for body text (WCAG AA)
- Ensure 3:1 contrast ratio for large text and UI components
- Test color combinations in both light and dark themes
- Don't rely on color alone to convey information

**OKLCH tips:**

- First value (lightness): 0% = black, 100% = white
- Second value (chroma): 0 = gray, higher = more saturated
- Third value (hue): 0-360deg color wheel position
- Use same lightness for perceptually similar brightness

---

### ❌ Common mistakes

**Don't mix color spaces:**
```scss
// ❌ Bad: mixing OKLCH and HEX
$primary: (
	100: oklch(95% 0.06 270deg),
	500: #6366f1,  // HEX doesn't match OKLCH scale
);

// ✅ Good: consistent OKLCH
$primary: (
	100: oklch(95% 0.06 270deg),
	500: oklch(60% 0.2 270deg),
);
```

**Don't hardcode colors in components:**
```scss
// ❌ Bad: hardcoded color
.button {
	background: oklch(60% 0.2 270deg);
}

// ✅ Good: use token
.button {
	background: var(--clr-primary-500);
}
```

**Don't create arbitrary shades:**
```scss
// ❌ Bad: non-standard scale
$custom: (
	150: oklch(...),  // Breaks 100-900 convention
	350: oklch(...),
	550: oklch(...)
);

// ✅ Good: use standard scale
$custom: (
	100: oklch(...),
	500: oklch(...),
	900: oklch(...)
);
```