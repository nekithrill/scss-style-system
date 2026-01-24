> **📁 Location:** `styles/base/_variables.scss`
> **📦 Type:** Basic

## 🏭 CSS Variables generation

Central configuration that generates all CSS custom properties from design tokens.

<br>

### 🧠 How it works

This file orchestrates the entire token system by:

1. **Importing all tokens:** Colors, typography, spacing, borders, shadows, animations, z-index
2. **Importing generation mixin:** The `generate-tokens` mixin that converts Sass maps to CSS variables
3. **Configuring token groups:** Maps each token set to a prefix and optional transform
4. **Generating variables:** Calls the mixin in `:root` to create all CSS custom properties

**Key concept:** This is the single source of truth for what CSS variables get generated. Add/remove token groups here to control output.

---

### 🚀 Usage

```scss
// Variables are generated automatically
// Use them in your styles:

.card {
	padding: var(--sp-4);
	border-radius: var(--rd-md);
	background: var(--clr-primary-500);
	box-shadow: var(--shadow-md);
	font-size: var(--fs-h3);
	font-weight: var(--fw-bold);
}
```

---

### ⚙️ Configuration

```scss
// base/_variables.scss

@use '../tokens/colors' as *;
@use '../tokens/typography' as *;
@use '../tokens/spacing' as *;
@use '../tokens/borders' as *;
@use '../tokens/shadows' as *;
@use '../tokens/animations' as *;
@use '../tokens/z-index' as *;
@use '../core/mixins/generate-tokens' as *;

$base-tokens: (
	colors: (map: $all-colors, prefix: 'clr'),
	font-families: (map: $font-families, prefix: 'ff'),
	font-weights: (map: $font-weights, prefix: 'fw'),
	font-sizes: (map: $font-sizes, prefix: 'fs', transform: 'rem'),
	spacing: (map: $spacing, prefix: 'sp', transform: 'rem'),
	radius: (map: $border-radius, prefix: 'rd', transform: 'rem'),
	stroke: (map: $stroke-width, prefix: 'stroke'),
	shadows: (map: $shadows, prefix: 'shadow'),
	duration: (map: $duration, prefix: 'dur'),
	easing: (map: $easing, prefix: 'tf'),
	delay: (map: $delay, prefix: 'delay'),
	z-index: (map: $z-index, prefix: 'z')
);

:root {
	@include generate-tokens($base-tokens);
}
```

---

### 🔧 Customization

```scss
// Add new token group
@use '../tokens/my-custom-tokens' as *;

$base-tokens: (
	// ... existing tokens
	custom: (
		map: $my-custom-map,
		prefix: 'custom',
		transform: 'rem'  // Optional
	)
);

// Remove unused token group
$base-tokens: (
	colors: (...),
	spacing: (...),
	// Removed: shadows, animations, etc.
);

// Change prefix
$base-tokens: (
	colors: (
		map: $all-colors,
		prefix: 'color'  // Instead of 'clr'
	)
);
```

---

### ✔️ Best practices

- ✅ **Do:** Use short, consistent prefixes
- ✅ **Do:** Apply 'rem' transform to spacing/sizing tokens
- ✅ **Do:** Keep all token generation in one place
- ✅ **Do:** Import only tokens you use
- ❌ **Don't:** Transform colors or unitless values
- ❌ **Don't:** Use long prefixes (increases CSS size)
- ❌ **Don't:** Duplicate token generation

---

### ❌ Common mistakes

**Wrong transform usage:**
```scss
// ❌ Bad: Transforming colors
colors: (
	map: $all-colors,
	prefix: 'clr',
	transform: 'rem'  // Colors don't need rem!
),

// ✅ Good: Transform only spacing/sizing
spacing: (
	map: $spacing,
	prefix: 'sp',
	transform: 'rem'
),
```

**Forgetting to import tokens:**
```scss
// ❌ Bad: Using undefined variable
$base-tokens: (
	spacing: (
		map: $spacing,  // Where does $spacing come from?
		prefix: 'sp'
	)
);

// ✅ Good: Import first
@use '../tokens/spacing' as *;

$base-tokens: (
	spacing: (
		map: $spacing,
		prefix: 'sp'
	)
);
```