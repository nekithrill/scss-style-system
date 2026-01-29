> **📁 Location:** `styles/tokens/_spacing.scss`
> **🧭 Scope:** Layout spacing and component paddings
> **📦 Type:** Token

# 📏 Spacing tokens

Define consistent spacing values based on an 8px grid system for padding, margin, and gaps.

## 🧠 How it works

Spacing tokens follow an **8px grid system** - a widely-used design standard where all spacing values are multiples of 8 pixels. This creates visual rhythm and consistency across your interface.

**The scale (`--sp-*`)** ranges from `0` (no space) to `8` (64px), providing 9 spacing options. Each step is a multiple of the base spacing unit:

- `sp-1` = 1 × 8px = 8px
- `sp-2` = 2 × 8px = 16px
- `sp-3` = 3ы × 8px = 24px
- And so on...

**Base spacing variable** (`$base-spacing`) is set to 8px by default. Change this one value to scale the entire spacing system proportionally. For example, setting it to 10px would make `sp-1` = 10px, `sp-2` = 20px, etc.

**Rem conversion:** All spacing values are converted to rem units (e.g., 8px → 0.5rem) to respect user browser font size preferences and improve accessibility.

**Why 8px?** Most screen dimensions are divisible by 8, making layouts pixel-perfect across devices. It's also small enough for fine-tuning but large enough to create visible differences between spacing levels.

## 🚀 Usage

```scss
// Padding and margin
.container {
	padding: var(--sp-4);  // 32px / 2rem
	margin-bottom: var(--sp-6);  // 48px / 3rem
}

.button {
	padding: var(--sp-2) var(--sp-4);  // 16px 32px / 1rem 2rem
}

// Gaps in grid/flexbox
.grid {
	display: grid;
	gap: var(--sp-3);  // 24px / 1.5rem
	grid-template-columns: repeat(3, 1fr);
}

.flex-container {
	display: flex;
	gap: var(--sp-2);  // 16px / 1rem
}

// Combined spacing
.card {
	padding: var(--sp-4);
	margin: var(--sp-3) 0;
	
	.card-header {
		margin-bottom: var(--sp-3);
	}
	
	.card-body {
		padding: var(--sp-2);
	}
}

// No spacing
.flush {
	margin: var(--sp-0);   // 0
	padding: var(--sp-0);  // 0
}
```

## ⚙️ Basic configuration

```scss
// tokens/_spacing.scss

$base-spacing: 8px !default;

$spacing: (
	0: 0,                      // No spacing
	1: $base-spacing * 1,      // 8px - Tight spacing
	2: $base-spacing * 2,      // 16px - Small spacing
	3: $base-spacing * 3,      // 24px - Medium spacing
	4: $base-spacing * 4,      // 32px - Large spacing
	5: $base-spacing * 5,      // 40px - Extra large
	6: $base-spacing * 6,      // 48px - 2x large
	7: $base-spacing * 7,      // 56px - 3x large
	8: $base-spacing * 8       // 64px - Maximum spacing
);
```

**Generated CSS variables:**

```css
:root {
	--sp-0: 0;
	--sp-1: 0.5rem;    /* 8px */
	--sp-2: 1rem;      /* 16px */
	--sp-3: 1.5rem;    /* 24px */
	--sp-4: 2rem;      /* 32px */
	--sp-5: 2.5rem;    /* 40px */
	--sp-6: 3rem;      /* 48px */
	--sp-7: 3.5rem;    /* 56px */
	--sp-8: 4rem;      /* 64px */
}
```

## 🔧 Customization

**Change base unit:**

```scss
// Use 10px base instead of 8px
$base-spacing: 10px;

// Result:
// sp-1 = 10px (0.625rem)
// sp-2 = 20px (1.25rem)
// sp-4 = 40px (2.5rem)
```

**Add more granular steps:**

```scss
$base-spacing: 8px;

$spacing: (
	0: 0,
	1: $base-spacing * 0.5,    // 4px - Half step
	2: $base-spacing * 1,      // 8px
	3: $base-spacing * 1.5,    // 12px - Between step
	4: $base-spacing * 2,      // 16px
	5: $base-spacing * 3,      // 24px
	6: $base-spacing * 4,      // 32px
	8: $base-spacing * 6,      // 48px
	10: $base-spacing * 8      // 64px
);
```

**Add extra large spacing:**

```scss
$spacing: (
	0: 0,
	1: $base-spacing * 1,
	2: $base-spacing * 2,
	3: $base-spacing * 3,
	4: $base-spacing * 4,
	5: $base-spacing * 5,
	6: $base-spacing * 6,
	7: $base-spacing * 7,
	8: $base-spacing * 8,
	10: $base-spacing * 10,    // 80px - Hero sections
	12: $base-spacing * 12,    // 96px - Large gaps
	16: $base-spacing * 16     // 128px - Section spacing
);
```

**Minimal spacing scale:**

```scss
// If you need fewer options
$spacing: (
	0: 0,
	sm: $base-spacing * 1,     // 8px
	md: $base-spacing * 2,     // 16px
	lg: $base-spacing * 4,     // 32px
	xl: $base-spacing * 6      // 48px
);
```

## ✔️ Best practices

**Choosing spacing values:**

- Use `sp-0` to remove spacing (flush layouts)
- Use `sp-1` (8px) for tight spacing (list items, chip gaps)
- Use `sp-2` (16px) for small spacing (button padding, small margins)
- Use `sp-3` (24px) for medium spacing (card padding, section gaps)
- Use `sp-4` (32px) for large spacing (container padding, component margins)
- Use `sp-5` to `sp-8` for extra-large spacing (section padding, hero areas)

**Consistent spacing patterns:**

```scss
// ✅ Good: Consistent vertical rhythm
.section {
	padding: var(--sp-8) 0;
	
	.heading {
		margin-bottom: var(--sp-4);
	}
	
	.paragraph {
		margin-bottom: var(--sp-3);
	}
	
	.subheading {
		margin-top: var(--sp-6);
		margin-bottom: var(--sp-3);
	}
}

// ✅ Good: Component internal spacing
.card {
	padding: var(--sp-4);
	gap: var(--sp-3);
	
	.card-title {
		margin-bottom: var(--sp-2);
	}
	
	.card-content {
		padding: var(--sp-2);
	}
}
```

**Responsive spacing:**

```scss
@use '@/styles/core/mixins/breakpoint' as *;

.container {
	padding: var(--sp-6);
	
	@include breakpoint('md') {
		padding: var(--sp-4);  // Smaller on tablets
	}
	
	@include breakpoint('sm') {
		padding: var(--sp-2);  // Minimal on mobile
	}
}
```

**Grid and flexbox gaps:**

```scss
// ✅ Good: Use gap instead of margins
.grid {
	display: grid;
	gap: var(--sp-4);  // Consistent spacing between all items
	grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

// ❌ Avoid: Manual margins between grid items
.grid-item {
	margin: var(--sp-2);  // Creates uneven gaps
}
```

## ❌ Common mistakes

**Don't mix spacing scales:**

```scss
// ❌ Bad: Random values breaking the 8px grid
.element {
	padding: 12px 20px;  // Not multiples of 8
	margin: 15px 25px;
}

// ✅ Good: Use token system
.element {
	padding: var(--sp-2) var(--sp-3);  // 16px 24px
	margin: var(--sp-2) var(--sp-4);   // 16px 32px
}
```

**Don't hardcode spacing values:**

```scss
// ❌ Bad: Hardcoded values
.card {
	padding: 2rem;
	margin-bottom: 1.5rem;
}

// ✅ Good: Use tokens
.card {
	padding: var(--sp-4);
	margin-bottom: var(--sp-3);
}
```

**Don't create arbitrary spacing:**

```scss
// ❌ Bad: Breaking the grid system
$spacing: (
	1: 8px,
	2: 16px,
	3: 20px,   // ← Not a multiple of 8!
	4: 32px
);

// ✅ Good: Stick to multiples
$spacing: (
	1: 8px,
	2: 16px,
	3: 24px,   // ← Multiple of 8
	4: 32px
);
```

**Don't forget about 0:**

```scss
// ❌ Bad: Hardcoding zero
.flush-element {
	margin: 0;
	padding: 0;
}

// ✅ Good: Use sp-0 for consistency
.flush-element {
	margin: var(--sp-0);
	padding: var(--sp-0);
}
```

**Don't use spacing for sizes:**

```scss
// ❌ Bad: Using spacing tokens for component dimensions
.button {
	width: var(--sp-8);   // Confusing - spacing for size?
	height: var(--sp-4);
}

// ✅ Good: Create size tokens separately or use explicit values
.button {
	width: auto;
	height: 40px;  // Or create separate size tokens
	padding: var(--sp-2) var(--sp-4);  // Spacing for padding
}
```