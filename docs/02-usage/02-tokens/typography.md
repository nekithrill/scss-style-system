## 🖋️ Typography tokens

Define font families, weights, and sizes for consistent typography across your project. The system uses a scalable approach with a base font size and multipliers, making it easy to adjust the entire type scale at once.

---

### Customizing Font Families

```scss
// tokens/_typography.scss

$font-families: (
	primary: 'YourFont, system-ui, sans-serif',  // Body text
	accent: 'YourAccent, Georgia, serif',        // Headings
	mono: '"Fira Code", Consolas, monospace'     // Code blocks
);
```

---

### Customizing Font Weights

```scss
$font-weights: (
	thin: 100,        // Add if needed
	light: 300,
	regular: 400,
	medium: 500,
	semibold: 600,   // Add if needed
	bold: 700,
	extra-bold: 900
);
```

---

### Customizing Font Sizes

The system uses a **base font size** with **multipliers** for headings, making it easy to scale your entire typography system.

```scss
@use 'sass:math';

/// Base font size (change this to scale entire system)
$base-font-size: 16px;

/// Heading size multipliers (relative to base)
$font-size-multipliers: (
	h1: 1.875,  // 30px (16 * 1.875)
	h2: 1.5,    // 24px (16 * 1.5)
	h3: 1.25,   // 20px (16 * 1.25)
	h4: 1.125,  // 18px (16 * 1.125)
	h5: 1,      // 16px (16 * 1)
	h6: 0.875   // 14px (16 * 0.875)
);

/// Generated font sizes
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * map.get($font-size-multipliers, h1),
	h2: $base-font-size * map.get($font-size-multipliers, h2),
	h3: $base-font-size * map.get($font-size-multipliers, h3),
	h4: $base-font-size * map.get($font-size-multipliers, h4),
	h5: $base-font-size * map.get($font-size-multipliers, h5),
	h6: $base-font-size * map.get($font-size-multipliers, h6)
);
```

---

### Usage

```css
body {
	font-family: var(--ff-primary);
	font-size: var(--fs-default);
	font-weight: var(--fw-regular);
}

h1 {
	font-size: var(--fs-h1);
	font-weight: var(--fw-bold);
}
```

---

#### Scale entire typography system

```scss
/// Change base size → all headings scale proportionally
$base-font-size: 18px;

/// Result:
/// h1: 33.75px (18 * 1.875)
/// h2: 27px    (18 * 1.5)
/// h3: 22.5px  (18 * 1.25)
/// h4: 20.25px (18 * 1.125)
/// h5: 18px    (18 * 1)
/// h6: 15.75px (18 * 0.875)
```

---

#### Adjust heading hierarchy

```scss
/// More dramatic scale
$font-size-multipliers: (
	h1: 2.5,   // 40px - much larger
	h2: 2,     // 32px
	h3: 1.5,   // 24px
	h4: 1.25,  // 20px
	h5: 1,     // 16px
	h6: 0.875  // 14px
);

/// More subtle scale
$font-size-multipliers: (
	h1: 1.5,    // 24px - closer to body
	h2: 1.375,  // 22px
	h3: 1.25,   // 20px
	h4: 1.125,  // 18px
	h5: 1,      // 16px
	h6: 0.875   // 14px
);
```

---

#### Add custom sizes

```scss
$font-size-multipliers: (
	h1: 1.875,
	h2: 1.5,
	h3: 1.25,
	h4: 1.125,
	h5: 1,
	h6: 0.875,
	small: 0.875,  // ← New (14px)
	tiny: 0.75,    // ← New (12px)
	large: 1.25,   // ← New (20px)
	xl: 1.5        // ← New (24px)
);

$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * map.get($font-size-multipliers, h1),
	h2: $base-font-size * map.get($font-size-multipliers, h2),
	h3: $base-font-size * map.get($font-size-multipliers, h3),
	h4: $base-font-size * map.get($font-size-multipliers, h4),
	h5: $base-font-size * map.get($font-size-multipliers, h5),
	h6: $base-font-size * map.get($font-size-multipliers, h6),
	small: $base-font-size * map.get($font-size-multipliers, small),
	tiny: $base-font-size * map.get($font-size-multipliers, tiny),
	large: $base-font-size * map.get($font-size-multipliers, large),
	xl: $base-font-size * map.get($font-size-multipliers, xl)
);
```
