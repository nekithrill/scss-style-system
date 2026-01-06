## 📏 Spacing tokens

Define consistent spacing values based on an 8px grid system. All spacing is calculated from `$base-spacing` for easy scaling across the entire project.
```scss
// tokens/_spacing.scss

// Base spacing unit (8px system)
// Change this to scale the entire spacing system
$base-spacing: 8px;

// Spacing scale calculated from base spacing
$spacing: (
	0: 0,
	1: $base-spacing * 1,  // 8px
	2: $base-spacing * 2,  // 16px
	3: $base-spacing * 3,  // 24px
	4: $base-spacing * 4,  // 32px
	5: $base-spacing * 5,  // 40px
	6: $base-spacing * 6,  // 48px
	7: $base-spacing * 7,  // 56px
	8: $base-spacing * 8   // 64px
);
```

> 💡 **Note:** Spacing values are automatically converted to rem in `base/_variables.scss`

<br>

### Generated CSS variables
```css
:root {
	--sp-0: 0;       /* 0 */
	--sp-1: 0.5rem;  /* 8px */
	--sp-2: 1rem;    /* 16px */
	--sp-3: 1.5rem;  /* 24px */
	--sp-4: 2rem;    /* 32px */
	--sp-5: 2.5rem;  /* 40px */
	--sp-6: 3rem;    /* 48px */
	--sp-7: 3.5rem;  /* 56px */
	--sp-8: 4rem;    /* 64px */
}
```

<br>

### Usage examples
```scss
// Component spacing
.button {
	padding: var(--sp-1) var(--sp-2); // 8px 16px - compact button
}

.card {
	padding: var(--sp-3);       // 24px - comfortable padding
	margin-bottom: var(--sp-4); // 32px - space between cards
}

// Layout spacing
.container {
	padding-inline: var(--sp-2);  // 16px - mobile padding

	@include breakpoint('md', true) {
		padding-inline: var(--sp-4);  // 32px - desktop padding
	}
}

.section {
	padding-block: var(--sp-6);  // 48px - section vertical spacing

	@include breakpoint('lg', true) {
		padding-block: var(--sp-8);  // 64px - larger screens
	}
}

// Flexbox/Grid gaps
.flex-container {
	display: flex;
	gap: var(--sp-2);  // 16px - space between items
}

.grid {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	gap: var(--sp-3);  // 24px - grid gap
}

// Typography spacing
.heading {
	margin-bottom: var(--sp-2); // 16px - heading to paragraph
}

.paragraph {
	margin-bottom: var(--sp-3); // 24px - paragraph to paragraph
}

// Form elements
.form-group {
	margin-bottom: var(--sp-3); // 24px - space between fields
}

.input {
	padding: var(--sp-1) var(--sp-2); // 8px 16px - input padding
}
```

<br>

### Spacing scale guide
```scss
// Visual reference for spacing values
// --sp-0: 0     |
// --sp-1: 8px   |■
// --sp-2: 16px  |■■
// --sp-3: 24px  |■■■
// --sp-4: 32px  |■■■■
// --sp-5: 40px  |■■■■■
// --sp-6: 48px  |■■■■■■
// --sp-7: 56px  |■■■■■■■
// --sp-8: 64px  |■■■■■■■■
```

<br>

### Customization examples

**Switch to 4px base (more granular control):**
```scss
$base-spacing: 4px;

$spacing: (
	0: 0,
	1: $base-spacing * 1,    // 4px
	2: $base-spacing * 2,    // 8px
	3: $base-spacing * 3,    // 12px
	4: $base-spacing * 4,    // 16px
	6: $base-spacing * 6,    // 24px
	8: $base-spacing * 8,    // 32px
	12: $base-spacing * 12,  // 48px
	16: $base-spacing * 16   // 64px
);
```

**Add larger spacing values for hero sections:**
```scss
$spacing: (
	0: 0,
	1: $base-spacing * 1,    // 8px
	2: $base-spacing * 2,    // 16px
	3: $base-spacing * 3,    // 24px
	4: $base-spacing * 4,    // 32px
	5: $base-spacing * 5,    // 40px
	6: $base-spacing * 6,    // 48px
	7: $base-spacing * 7,    // 56px
	8: $base-spacing * 8,    // 64px
	10: $base-spacing * 10,  // New: 80px
	12: $base-spacing * 12,  // New: 96px
	16: $base-spacing * 16,  // New: 128px
	20: $base-spacing * 20   // New: 160px
);
```

**Add fractional spacing for fine-tuning:**
```scss
@use 'sass:math';

$spacing: (
	0: 0,
	'0.5': math.div($base-spacing, 2),  // 4px - hairline spacing
	1: $base-spacing * 1,               // 8px
	'1.5': $base-spacing * 1.5,         // 12px
	2: $base-spacing * 2,               // 16px
	'2.5': $base-spacing * 2.5,         // 20px
	3: $base-spacing * 3,               // 24px
	4: $base-spacing * 4,               // 32px
	5: $base-spacing * 5,               // 40px
	6: $base-spacing * 6,               // 48px
	7: $base-spacing * 7,               // 56px
	8: $base-spacing * 8                // 64px
);
```

**Add semantic aliases for clarity:**
```scss
$spacing: (
	// Numeric scale
	0: 0,
	1: $base-spacing * 1,
	2: $base-spacing * 2,
	3: $base-spacing * 3,
	4: $base-spacing * 4,
	5: $base-spacing * 5,
	6: $base-spacing * 6,
	7: $base-spacing * 7,
	8: $base-spacing * 8,

	// Semantic aliases
	'xs': $base-spacing * 1,  // 8px
	'sm': $base-spacing * 2,  // 16px
	'md': $base-spacing * 3,  // 24px
	'lg': $base-spacing * 4,  // 32px
	'xl': $base-spacing * 6   // 48px
);

// Usage with aliases
.card {
	padding: var(--sp-md); // 24px - clearer intent
}
```

<br>

### Best practices

**Choosing spacing values:**

- **0:** No spacing - reset margins
- **1 (8px):** Tight spacing - button padding, icon gaps
- **2 (16px):** Small spacing - between related items
- **3 (24px):** Medium spacing - between sections, card padding
- **4 (32px):** Large spacing - between major sections
- **5-6 (40-48px):** Section spacing - vertical rhythm
- **7-8 (56-64px):** Hero spacing - large layouts

**Common patterns:**
```scss
// Consistent component spacing
.component {
	// Internal spacing (padding): smaller values
	padding: var(--sp-2); // 16px

	// External spacing (margin): larger values
	margin-bottom: var(--sp-4); // 32px
}

// Responsive spacing (scale up on larger screens)
.section {
	padding: var(--sp-3); // 24px mobile

	@include breakpoint('md', true) {
		padding: var(--sp-5); // 40px tablet
	}

	@include breakpoint('lg', true) {
		padding: var(--sp-6); // 48px desktop
	}
}

// Nested spacing (smaller for nested elements)
.card {
	padding: var(--sp-4); // 32px outer

	.card-section {
		padding: var(--sp-2); // 16px inner
	}
}
```

**Grid alignment:**
```scss
// Everything aligns to 8px grid
.layout {
	padding: var(--sp-3); // 24px ✅ divisible by 8
	gap: var(--sp-2);     // 16px ✅ divisible by 8
}

.misaligned {
	padding: 18px;  // ❌ breaks grid (not divisible by 8)
	margin: 13px;   // ❌ arbitrary value
}
```

**Avoid:**

- ❌ Arbitrary values like `15px`, `23px`, `37px`
- ❌ Mixing spacing systems (8px and 5px grids)
- ❌ Using too many different spacing values
- ✅ Stick to the scale for consistent rhythm
- ✅ Use 3-5 spacing values for most designs