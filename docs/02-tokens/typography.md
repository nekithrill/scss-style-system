> 📂 **Location:** `styles/tokens/_typography.scss`
> 🎯 **Scope:** Font families, sizes, weights, line heights, letter spacings
> 🏷️ **Type:** Token

# ✍️ Typography tokens

Type system built on a configurable base size. Change `$base-font-size` — all heading sizes scale proportionally.

## ⚡️ Usage

```scss
.card-title {
	font-family: var(--ff-accent);
	font-size: var(--fs-h3);
	font-weight: var(--fw-bold);
	line-height: var(--lh-tight);
}

.label {
	font-size: var(--fs-default);
	font-weight: var(--fw-medium);
	letter-spacing: var(--ls-wide);
}

.code {
	font-family: var(--ff-mono);
	font-size: var(--fs-h6);
	line-height: var(--lh-loose);
}
```

## ⚙️ Configuration

```scss
// Font families — prefix: --ff-
$font-families: (
	primary: (
		'Inter',
		system-ui,
		sans-serif
	),
	accent: (
		Georgia,
		'Times New Roman',
		serif
	),
	mono: (
		'Courier New',
		Courier,
		monospace
	),
	system: (
		system-ui,
		-apple-system,
		'Segoe UI',
		'Roboto',
		sans-serif
	)
) !default;

// Font weights — prefix: --fw-
$font-weights: (
	light: 300,
	regular: 400,
	medium: 500,
	bold: 700,
	extra-bold: 900
) !default;

// Font sizes — prefix: --fs-
$base-font-size: 16px !default;

$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 2,
	h2: $base-font-size * 1.75,
	h3: $base-font-size * 1.5,
	h4: $base-font-size * 1.25,
	h5: $base-font-size * 1.125,
	h6: $base-font-size * 1
) !default;

// Line heights — prefix: --lh-
$line-heights: (
	compact: 1,
	tight: 1.25,
	normal: 1.5,
	loose: 2
) !default;

// Letter spacings — prefix: --ls-
$letter-spacings: (
	tighter: -0.05em,
	tight: -0.02em,
	normal: 0,
	wide: 0.05em,
	wider: 0.1em
) !default;
```

**Generated variables**

```css
:root {
	--ff-primary: 'Inter', system-ui, sans-serif;
	--ff-accent: Georgia, 'Times New Roman', serif;
	--ff-mono: 'Courier New', Courier, monospace;
	--ff-system: system-ui, -apple-system, 'Segoe UI', 'Roboto', sans-serif;

	--fw-light: 300;
	--fw-regular: 400;
	--fw-medium: 500;
	--fw-bold: 700;
	--fw-extra-bold: 900;

	--fs-default: 1rem; /* 16px */
	--fs-h1: 2rem; /* 32px */
	--fs-h2: 1.75rem; /* 28px */
	--fs-h3: 1.5rem; /* 24px */
	--fs-h4: 1.25rem; /* 20px */
	--fs-h5: 1.125rem; /* 18px */
	--fs-h6: 1rem; /* 16px */

	--lh-compact: 1;
	--lh-tight: 1.25;
	--lh-normal: 1.5;
	--lh-loose: 2;

	--ls-tighter: -0.05em;
	--ls-tight: -0.02em;
	--ls-normal: 0;
	--ls-wide: 0.05em;
	--ls-wider: 0.1em;
}
```

## 🔧 Customization

**Change base size** — all headings scale proportionally:

```scss
$base-font-size: 18px !default;
```

**Change fonts** — update families and load them in `_fonts.scss`:

```scss
$font-families: (
	primary: (
		'Roboto',
		system-ui,
		sans-serif
	),
	accent: (
		'Playfair Display',
		serif
	),
	mono: (
		'Fira Code',
		monospace
	),
	system: (
		system-ui,
		-apple-system,
		sans-serif
	)
) !default;
```

**Adjust type scale:**

```scss
$font-sizes: (
	default: $base-font-size,
	h1: $base-font-size * 2.5,
	h2: $base-font-size * 2,
	h3: $base-font-size * 1.5,
	h4: $base-font-size * 1.25,
	h5: $base-font-size * 1.125,
	h6: $base-font-size * 1
) !default;
```
