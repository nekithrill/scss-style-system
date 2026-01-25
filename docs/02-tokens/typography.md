> **📁 Location:** `styles/tokens/_typography.scss`
> **🧭 Scope:** Text styles, font scales and typographic rhythm
> **📦 Type:** Token

## ✍️ Typography tokens

Define font families, weights, and sizes for consistent typography across your interface.

<br>

### 🧠 How it works

Typography tokens are organized into three categories:

**Font family tokens (`--ff-*`)** define typeface stacks for different purposes:
- `primary`: Main brand font (used in examples: JetBrains)
- `accent`: Decorative/heading font (used in examples: Tektur)
- `system`: Fallback system font stack for reliability

**Font weight tokens (`--fw-*`)** provide standardized weight values from light (300) to extra-bold (900). These ensure consistent text emphasis across components.

**Font size tokens (`--fs-*`)** define a typographic scale based on a configurable base size (default: 16px):
- `default`: Base body text size
- `h1` through `h6`: Heading sizes in descending order
- All sizes are calculated as multiples of the base size
- Values are converted to rem for accessibility

**Base font size** (`$base-font-size`) serves as the foundation - changing this one value scales the entire typography system proportionally.

---

### 🚀 Usage

```scss
// Basic text styling
body {
	font-family: var(--ff-primary);
	font-size: var(--fs-default);
	font-weight: var(--fw-regular);
}

// Headings
h1 {
	font-family: var(--ff-accent);
	font-size: var(--fs-h1);
	font-weight: var(--fw-bold);
}

h2 {
	font-family: var(--ff-accent);
	font-size: var(--fs-h2);
	font-weight: var(--fw-bold);
}

// Buttons with different weights
.button {
	font-family: var(--ff-primary);
	font-size: var(--fs-default);
	font-weight: var(--fw-medium);
	
	&.button-bold {
		font-weight: var(--fw-bold);
	}
}

// Cards with mixed typography
.card {
	.card-title {
		font-family: var(--ff-accent);
		font-size: var(--fs-h3);
		font-weight: var(--fw-bold);
	}
	
	.card-subtitle {
		font-size: var(--fs-h5);
		font-weight: var(--fw-medium);
		color: var(--clr-neutral-600);
	}
	
	.card-body {
		font-size: var(--fs-default);
		font-weight: var(--fw-regular);
	}
}

// System font fallback
.code-block {
	font-family: var(--ff-system);
	font-size: var(--fs-h6);
	font-weight: var(--fw-regular);
}
```

---

### ⚙️ Basic configuration

```scss
// tokens/_typography.scss

// Font families - customize with your brand fonts
$font-families: (
	primary: 'JetBrains',    // Main brand font
	accent: 'Tektur',        // Headings/decorative
	system: (                // Fallback system fonts
		system-ui,
		-apple-system,
		'Segoe UI',
		Roboto,
		sans-serif
	)
) !default;

// Font weights
$font-weights: (
	light: 300,        // Light text, captions
	regular: 400,      // Body text, default
	medium: 500,       // Emphasized text, button labels
	bold: 700,         // Headings, strong emphasis
	extra-bold: 900    // Maximum emphasis
) !default;

// Base size for scaling entire system
$base-font-size: 16px !default;

// Font sizes (multiples of base)
$font-sizes: (
	default: $base-font-size,           // 16px - Body text
	h1: $base-font-size * 1.875,        // 30px - Main heading
	h2: $base-font-size * 1.5,          // 24px - Section heading
	h3: $base-font-size * 1.25,         // 20px - Subsection heading
	h4: $base-font-size * 1.125,        // 18px - Small heading
	h5: $base-font-size * 1,            // 16px - Tiny heading
	h6: $base-font-size * 0.875         // 14px - Label/caption
);
```

**Generated CSS variables:**
```css
:root {
	/* Font families */
	--ff-primary: 'JetBrains';
	--ff-accent: 'Tektur';
	--ff-system: system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
	
	/* Font weights */
	--fw-light: 300;
	--fw-regular: 400;
	--fw-medium: 500;
	--fw-bold: 700;
	--fw-extra-bold: 900;
	
	/* Font sizes (converted to rem) */
	--fs-default: 1rem;        /* 16px */
	--fs-h1: 1.875rem;         /* 30px */
	--fs-h2: 1.5rem;           /* 24px */
	--fs-h3: 1.25rem;          /* 20px */
	--fs-h4: 1.125rem;         /* 18px */
	--fs-h5: 1rem;             /* 16px */
	--fs-h6: 0.875rem;         /* 14px */
}
```

---

### 🔧 Customization

**Change brand fonts:**
```scss
$font-families: (
	primary: 'Inter',           // Modern sans-serif
	accent: 'Playfair Display', // Elegant serif
	system: (system-ui, sans-serif)
) !default;
```

**Adjust base font size:**
```scss
// Larger base size (18px)
$base-font-size: 18px;

// Result:
// h1: 33.75px (18 × 1.875)
// h2: 27px (18 × 1.5)
// default: 18px
```

**Modify type scale:**
```scss
// More dramatic scale
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 2.5,      // 40px - Larger
	h2: $base-font-size * 2,        // 32px - Larger
	h3: $base-font-size * 1.5,      // 24px
	h4: $base-font-size * 1.25,     // 20px
	h5: $base-font-size * 1,        // 16px
	h6: $base-font-size * 0.875     // 14px
);

// More subtle scale
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 1.5,      // 24px - Smaller
	h2: $base-font-size * 1.25,     // 20px - Smaller
	h3: $base-font-size * 1.125,    // 18px
	h4: $base-font-size * 1,        // 16px
	h5: $base-font-size * 0.875,    // 14px
	h6: $base-font-size * 0.75      // 12px
);
```

**Add custom sizes:**
```scss
$font-sizes: (
	default: $base-font-size,
	// Heading sizes...
	h1: $base-font-size * 1.875,
	h2: $base-font-size * 1.5,
	h3: $base-font-size * 1.25,
	h4: $base-font-size * 1.125,
	h5: $base-font-size * 1,
	h6: $base-font-size * 0.875,
	// Custom sizes
	small: $base-font-size * 0.75,      // 12px - Fine print
	caption: $base-font-size * 0.875,   // 14px - Image captions
	lead: $base-font-size * 1.125,      // 18px - Lead paragraph
	display: $base-font-size * 3        // 48px - Hero text
);
```

**Add more font weights:**
```scss
$font-weights: (
	thin: 100,
	extra-light: 200,
	light: 300,
	regular: 400,
	medium: 500,
	semi-bold: 600,
	bold: 700,
	extra-bold: 800,
	black: 900
) !default;
```

---

### ✔️ Best practices

**Font family usage:**
- Use `primary` for body text, UI elements, most content
- Use `accent` for headings, titles, brand elements
- Use `system` as fallback or for performance-critical text

**Font weight guidelines:**
- `light` (300): Light text, de-emphasized content
- `regular` (400): Default body text
- `medium` (500): Buttons, labels, emphasized text
- `bold` (700): Headings, strong emphasis
- `extra-bold` (900): Maximum impact, hero text

**Font size hierarchy:**
```scss
// ✅ Good: Clear hierarchy
.hero {
	h1 {
		font-size: var(--fs-h1);  // Largest
		font-weight: var(--fw-extra-bold);
	}
	
	.subtitle {
		font-size: var(--fs-h3);  // Medium
		font-weight: var(--fw-regular);
	}
	
	.description {
		font-size: var(--fs-default);  // Base
		font-weight: var(--fw-regular);
	}
}
```

**Responsive typography:**
```scss
@use '@/styles/core/mixins/breakpoint' as *;

h1 {
	font-size: var(--fs-h1);
	
	@include breakpoint('md') {
		font-size: var(--fs-h2);  // Smaller on tablets
	}
	
	@include breakpoint('sm') {
		font-size: var(--fs-h3);  // Even smaller on mobile
	}
}
```

**Combining tokens:**
```scss
// ✅ Good: Semantic component styling
.button {
	font-family: var(--ff-primary);
	font-size: var(--fs-default);
	font-weight: var(--fw-medium);
	padding: var(--sp-2) var(--sp-4);
	border-radius: var(--rd-md);
	
	&.button-lg {
		font-size: var(--fs-h4);
		font-weight: var(--fw-bold);
		padding: var(--sp-3) var(--sp-6);
	}
}
```

**Loading custom fonts:**
```scss
// Remember to load fonts in _fonts.scss
@font-face {
	font-family: 'JetBrains';
	src: url('/fonts/JetBrains-Regular.woff2') format('woff2');
	font-weight: 400;
	font-display: swap;  // Improve performance
}

@font-face {
	font-family: 'JetBrains';
	src: url('/fonts/JetBrains-Bold.woff2') format('woff2');
	font-weight: 700;
	font-display: swap;
}
```

---

### ❌ Common mistakes

**Don't hardcode typography values:**
```scss
// ❌ Bad: Hardcoded values
.heading {
	font-family: 'Arial', sans-serif;
	font-size: 24px;
	font-weight: 700;
}

// ✅ Good: Use tokens
.heading {
	font-family: var(--ff-accent);
	font-size: var(--fs-h2);
	font-weight: var(--fw-bold);
}
```

**Don't skip the type scale:**
```scss
// ❌ Bad: Arbitrary sizes breaking the scale
.text-large {
	font-size: 22px;  // Not in the scale
}

.text-small {
	font-size: 13px;  // Not in the scale
}

// ✅ Good: Use existing scale or add to tokens
.text-large {
	font-size: var(--fs-h3);  // 20px - from scale
}

.text-small {
	font-size: var(--fs-h6);  // 14px - from scale
}
```

**Don't use too many font families:**
```scss
// ❌ Bad: Too many fonts
$font-families: (
	primary: 'Font1',
	secondary: 'Font2',
	accent: 'Font3',
	special: 'Font4',
	display: 'Font5'  // Performance and consistency issues
);

// ✅ Good: 2-3 fonts maximum
$font-families: (
	primary: 'Inter',           // Body text
	accent: 'Playfair Display', // Headings
	system: (system-ui, sans-serif)  // Fallback
);
```

**Don't forget font weight availability:**
```scss
// ❌ Bad: Using weights your font doesn't have
.text {
	font-family: var(--ff-accent);
	font-weight: var(--fw-medium);  // What if accent font doesn't have weight 500?
}

// ✅ Good: Use weights your fonts support
// If accent font only has 400 and 700:
.text {
	font-family: var(--ff-accent);
	font-weight: var(--fw-regular);  // 400 ✓
}

.heading {
	font-family: var(--ff-accent);
	font-weight: var(--fw-bold);  // 700 ✓
}
```

**Don't ignore line-height:**
```scss
// ❌ Bad: Font size without line-height
h1 {
	font-size: var(--fs-h1);
	// Line-height will be browser default (might be too tight)
}

// ✅ Good: Set appropriate line-height
h1 {
	font-size: var(--fs-h1);
	line-height: 1.2;  // Tighter for headings
}

body {
	font-size: var(--fs-default);
	line-height: 1.6;  // More relaxed for body text
}
```