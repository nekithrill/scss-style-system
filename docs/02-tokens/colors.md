> 📂 **Location:** `styles/tokens/_colors.scss`
> 🎯 **Scope:** Color palette — brand and semantic
> 🏷️ **Type:** Token

# 🎨 Color tokens

OKLCH color system for perceptually uniform palettes. Change a single hue variable — all five shades update automatically.

## ⚡️ Usage

```scss
.button {
	background: var(--clr-primary-500);
	color: var(--clr-neutral-100);

	&:hover {
		background: var(--clr-primary-700);
	}
}

.alert-error {
	background: var(--clr-error-100);
	border: 1px solid var(--clr-error-300);
	color: var(--clr-error-700);
}
```

## ⚙️ Configuration

```scss
// Hues for brand colors
$primary-hue: 270deg !default;
$secondary-hue: 248deg !default;
$neutral-hue: 220deg !default;

// Hues for semantic colors
$success-hue: 160deg !default;
$error-hue: 25deg !default;
$warning-hue: 80deg !default;
$info-hue: 260deg !default;

// PRIMARY - Brand colors, accents, interactive elements
$primary: (
	100: oklch(95% 0.06 $primary-hue),
	300: oklch(78% 0.14 $primary-hue),
	500: oklch(60% 0.2 $primary-hue),
	700: oklch(38% 0.16 $primary-hue),
	900: oklch(20% 0.1 $primary-hue)
) !default;

// SECONDARY - Backgrounds, surfaces, cards
$secondary: (
	100: oklch(99% 0.005 $secondary-hue),
	300: oklch(92% 0.008 $secondary-hue),
	500: oklch(82% 0.012 $secondary-hue),
	700: oklch(68% 0.02 $secondary-hue),
	900: oklch(48% 0.032 $secondary-hue)
) !default;

// NEUTRAL - Text, borders, icons, dividers
$neutral: (
	100: oklch(96% 0.008 $neutral-hue),
	300: oklch(78% 0.014 $neutral-hue),
	500: oklch(56% 0.02 $neutral-hue),
	700: oklch(36% 0.016 $neutral-hue),
	900: oklch(18% 0.01 $neutral-hue)
) !default;

// SUCCESS - Positive feedback, confirmations
$success: (
	100: oklch(95% 0.05 $success-hue),
	300: oklch(75% 0.13 $success-hue),
	500: oklch(52% 0.17 $success-hue),
	700: oklch(35% 0.13 $success-hue),
	900: oklch(20% 0.08 $success-hue)
) !default;

// ERROR - Errors, destructive actions
$error: (
	100: oklch(95% 0.04 $error-hue),
	300: oklch(75% 0.14 $error-hue),
	500: oklch(56% 0.22 $error-hue),
	700: oklch(36% 0.16 $error-hue),
	900: oklch(20% 0.1 $error-hue)
) !default;

// WARNING - Alerts, cautionary messages
$warning: (
	100: oklch(96% 0.04 $warning-hue),
	300: oklch(84% 0.12 $warning-hue),
	500: oklch(70% 0.17 $warning-hue),
	700: oklch(44% 0.13 $warning-hue),
	900: oklch(24% 0.08 $warning-hue)
) !default;

// INFO - Information, tips, neutral notifications
$info: (
	100: oklch(95% 0.04 $info-hue),
	300: oklch(74% 0.12 $info-hue),
	500: oklch(56% 0.2 $info-hue),
	700: oklch(36% 0.15 $info-hue),
	900: oklch(20% 0.09 $info-hue)
) !default;

$all-colors: (
	'primary': $primary,
	'secondary': $secondary,
	'neutral': $neutral,
	'success': $success,
	'error': $error,
	'warning': $warning,
	'info': $info
) !default;
```

**Generated variables**

Prefix: `--clr-`

```css
:root {
	--clr-primary-100: oklch(95% 0.06 270deg);
	--clr-primary-300: oklch(78% 0.14 270deg);
	--clr-primary-500: oklch(60% 0.2 270deg);
	--clr-primary-700: oklch(38% 0.16 270deg);
	--clr-primary-900: oklch(20% 0.1 270deg);

	/* secondary, neutral — same pattern */

	--clr-success-100: oklch(95% 0.05 160deg);
	--clr-success-300: oklch(75% 0.13 160deg);
	--clr-success-500: oklch(52% 0.17 160deg);
	--clr-success-700: oklch(35% 0.13 160deg);
	--clr-success-900: oklch(20% 0.08 160deg);

	/* error, warning, info — same pattern */
}
```

**Shade guide:**

| Shade | Typical use |
|-------|-------------|
| 100 | Light backgrounds, subtle surfaces |
| 300 | Borders, icons, secondary elements |
| 500 | Main color — buttons, links, indicators |
| 700 | Hover and active states |
| 900 | Text on light backgrounds |

## 🔧 Customization

**Change brand hue:**

```scss
$primary-hue: 200deg !default; // Blue instead of purple
```

**Replace entire palette:**

```scss
$primary: (
	100: oklch(97% 0.04 210deg),
	300: oklch(85% 0.10 210deg),
	500: oklch(62% 0.18 210deg),
	700: oklch(40% 0.14 210deg),
	900: oklch(22% 0.09 210deg)
) !default;
```

**Add custom palette:**

```scss
$accent-hue: 340deg;

$accent: (
	100: oklch(95% 0.05 $accent-hue),
	300: oklch(78% 0.13 $accent-hue),
	500: oklch(60% 0.20 $accent-hue),
	700: oklch(38% 0.15 $accent-hue),
	900: oklch(20% 0.10 $accent-hue)
) !default;

$all-colors: (
	'primary': $primary,
	'secondary': $secondary,
	'neutral': $neutral,
	'accent': $accent,
	'success': $success,
	'error': $error,
	'warning': $warning,
	'info': $info
) !default;
```