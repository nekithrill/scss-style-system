> **📁 Location:** `styles/tokens/_borders.scss`
> **🧭 Scope:** Borders, outlines and radius system
> **📦 Type:** Token

# 🔲 Border tokens

Define border-radius values for consistent rounding across UI components. From subtle corners on buttons to fully circular avatars.

## 🧠 How it works

Border tokens provide two types of values:

1. **Border-radius tokens (`--rd-*`)** define corner rounding from sharp edges (`none`) to fully circular (`full`). Values are converted to rem units for scalability, except `pill` (9999px for fully rounded ends) and `full` (50% for circles). The prefix `rd` is short for "radius".

2. **Stroke-width tokens (`--stroke-*`)** define border thickness for consistent outlines across components. These stay in pixels as they represent physical device pixels.

The system includes special values:

- `pill` (9999px): Creates fully rounded ends on rectangular elements (badges, pills)
- `full` (50%): Creates perfect circles on square elements (avatars, icon buttons)

## 🚀 Usage

```scss
// Buttons
.button {
	border-radius: var(--rd-md); // 6px - standard rounding

	&.button-sm {
		border-radius: var(--rd-sm); // 4px - compact button
	}

	&.button-pill {
		border-radius: var(--rd-pill); // Fully rounded ends
	}
}

// Cards
.card {
	border-radius: var(--rd-lg); // 10px - soft corners
	border: var(--stroke-thin) solid var(--clr-neutral-200);

	&.card-sharp {
		border-radius: var(--rd-none); // No rounding
	}
}

// Inputs
.input {
	border-radius: var(--rd-sm); // 4px - subtle rounding
	border: var(--stroke-normal) solid var(--clr-neutral-300);
}

// Modals and panels
.modal {
	border-radius: var(--rd-xl); // 14px - prominent rounding
}

// Avatars (must be square)
.avatar {
	width: 40px;
	height: 40px;
	border-radius: var(--rd-full); // 50% - perfect circle
}

// Badges and tags
.badge {
	padding: 4px 12px;
	border-radius: var(--rd-pill); // Rounded ends, straight sides
	border: var(--stroke-thin) solid;
}
```

## ⚙️ Basic configuration

```scss
// tokens/_borders.scss

// Border-radius scale for component rounding
$border-radius: (
	none: 0,       // No rounding - sharp corners
	xs: 2px,       // Minimal - tags, small buttons
	sm: 4px,       // Subtle - inputs, chips
	md: 6px,       // Default - buttons, cards
	lg: 10px,      // Emphasized - larger cards
	xl: 14px,      // Prominent - modals, panels
	pill: 9999px,  // Pill-shaped - badges, tags (stays in px)
	full: 50%      // Circular - avatars (on square elements)
) !default;

// Stroke-width scale for borders
$stroke-width: (
	thin: 1px,     // Subtle borders, dividers
	normal: 2px,   // Standard borders
	thick: 4px     // Emphasized borders, focus rings
) !default;
```

**Generated CSS variables:**

```css
:root {
	/* Border radius (converted to rem) */
	--rd-none: 0;
	--rd-xs: 0.125rem;    /* 2px */
	--rd-sm: 0.25rem;     /* 4px */
	--rd-md: 0.375rem;    /* 6px */
	--rd-lg: 0.625rem;    /* 10px */
	--rd-xl: 0.875rem;    /* 14px */
	--rd-pill: 62.4375rem; /* 9999px */
	--rd-full: 50%;

	/* Stroke width (stays in px) */
	--stroke-thin: 1px;
	--stroke-normal: 2px;
	--stroke-thick: 4px;
}
```

## ❔ Understanding `pill` vs `full`

```scss
// pill (9999px) - for rectangular elements
.tag {
	padding: 4px 16px;
	border-radius: var(--rd-pill); // ✅ Rounded ends
	// Result: [====] pill shape
}

.tag-wrong {
	padding: 4px 16px;
	border-radius: var(--rd-full); // ❌ Creates oval
	// Result: (    ) oval shape
}

// full (50%) - for square elements only
.avatar {
	width: 48px;
	height: 48px;
	border-radius: var(--rd-full); // ✅ Perfect circle
	// Result: (O) circular
}

.avatar-wrong {
	width: 48px;
	height: 48px;
	border-radius: var(--rd-pill); // ❌ Still square corners
	// Result: [  ] barely rounded
}
```

## 🔧 Customization

```scss
// Increase overall roundness
$radius: (
	none: 0,
	xs: 2px,
	sm: 4px,
	md: 8px,   // Increased from 6px
	lg: 12px,  // Increased from 10px
	xl: 16px,  // Increased from 14px
	pill: 9999px,
	full: 50%
);

// Add extra large radius options
$radius: (
	none: 0,
	xs: 2px,
	sm: 4px,
	md: 6px,
	lg: 10px,
	xl: 14px,
	'2xl': 20px,   // New - hero cards
	'3xl': 28px,   // New - feature sections
	pill: 9999px,
	full: 50%
);

// Minimal design (less rounding)
$radius: (
	none: 0,
	xs: 1px,  // Reduced
	sm: 2px,  // Reduced
	md: 4px,  // Reduced
	lg: 6px,  // Reduced
	xl: 8px,  // Reduced
	pill: 9999px,
	full: 50%
);

// Add semantic aliases
$radius: (
	// ... existing values
	'button': 6px,   // Alias for button default
	'card': 10px,    // Alias for card default
	'input': 4px     // Alias for input default
);
```

## ✔️ Best practices

**Choosing radius values:**

- **none (0):** Sharp, modern look - data tables, minimal designs
- **xs-sm (2-4px):** Subtle rounding - inputs, small buttons, tags
- **md (6px):** Standard rounding - most buttons and cards
- **lg-xl (10-14px):** Soft rounding - larger cards, modals
- **pill (9999px):** Fully rounded ends - badges, pills, status indicators
- **full (50%):** Perfect circles - avatars, icon buttons (square only)

**Common patterns:**

```scss
// Consistent component families
.button,
.input,
.select {
	border-radius: var(--rd-md); // All form elements match
}

// Progressive rounding by size
.card-sm {
	border-radius: var(--rd-md); // 6px
}
.card-md {
	border-radius: var(--rd-lg); // 10px
}
.card-lg {
	border-radius: var(--rd-xl); // 14px
}

// Nested elements with smaller radius
.card {
	border-radius: var(--rd-lg); // 10px

	.card-header {
		border-radius: var(--rd-md) var(--rd-md) 0 0; // 6px top only
	}
}
```

**Avoid:**

- ❌ Mixing too many different radius values on one page
- ❌ Using `full: 50%` on non-square elements
- ❌ Random values like `7px`, `13px` - stick to the scale
- ✅ Use 2-3 radius values consistently throughout your design

## ❌ Common mistakes