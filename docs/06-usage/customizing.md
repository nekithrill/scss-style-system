# 🎨 Customizing the system

Learn how to adapt the design system to match your brand and design requirements.

## 🧠 How customization works

All design values in the system are defined with SCSS `!default` flag, which means you can override them before they're set:

```scss
// Your custom values
$primary-hue: 200deg;         // Override before import
$base-spacing: 4px;

// Import system (uses your values)
@use 'styles/tokens/colors' as *;
@use 'styles/tokens/spacing' as *;
```

**Key principle:** Customize tokens at the source → Changes propagate throughout the entire system automatically.

## 🎨 Customizing colors

### Change brand color (easiest)

```scss
// tokens/_colors.scss

// Change hue parameter
$primary-hue: 200deg !default;     // Blue (was 270deg purple)
$secondary-hue: 150deg !default;   // Green (was 180deg cyan)
```

**Result:** All 9 shades (100-900) update automatically to the new color!

### Adjust color intensity

```scss
// Increase chroma for more vibrant colors
$primary-chroma: 0.25 !default;    // Was 0.2

// Adjust lightness range
$primary-lightness: (
    100: 98%,    // Lighter
    500: 55%,    // Slightly darker
    900: 10%     // Much darker
) !default;
```

### Use custom color palette

```scss
// Replace entire palette
$primary: (
    100: oklch(97% 0.05 210deg),
    200: oklch(92% 0.08 210deg),
    300: oklch(85% 0.12 210deg),
    400: oklch(75% 0.16 210deg),
    500: oklch(60% 0.20 210deg),    // Base color
    600: oklch(50% 0.18 210deg),
    700: oklch(40% 0.15 210deg),
    800: oklch(30% 0.12 210deg),
    900: oklch(20% 0.08 210deg)
) !default;
```

### Custom semantic colors

```scss
$semantic-colors: (
    success: (
        bg: oklch(95% 0.08 150deg),
        text: oklch(25% 0.12 150deg),
        solid: oklch(55% 0.18 150deg)
    ),
    // Custom: add "pending" state
    pending: (
        bg: oklch(95% 0.08 60deg),
        text: oklch(25% 0.12 60deg),
        solid: oklch(55% 0.18 60deg)
    )
) !default;
```

## ✍️ Customizing typography

### Change base font size

```scss
// tokens/_typography.scss

$base-font-size: 14px !default;  // Was 16px

// All sizes scale down:
// h1: 26.25px (was 30px)
// h2: 21px (was 24px)
// default: 14px (was 16px)
```

### Adjust type scale

```scss
$font-sizes: (
    default: $base-font-size,
    h1: $base-font-size * 2.5,    // Larger (was 1.875)
    h2: $base-font-size * 2,      // Larger (was 1.5)
    h3: $base-font-size * 1.5,    // Same
    h4: $base-font-size * 1.25,   // Same
    h5: $base-font-size * 1,      // Same
    h6: $base-font-size * 0.875   // Same
) !default;
```

### Use custom fonts

```scss
$font-families: (
    primary: 'Inter',              // Was JetBrains
    accent: 'Playfair Display',    // Was Tektur
    system: (system-ui, sans-serif)
) !default;
```

Don't forget to load fonts in `base/_fonts.scss`:

```scss
@font-face {
    font-family: 'Inter';
    src: url('/fonts/Inter-Regular.woff2') format('woff2');
    font-weight: 400;
    font-display: swap;
}
```

## 📏 Customizing spacing

### Change base unit

```scss
// tokens/_spacing.scss

$base-spacing: 4px !default;  // Tighter (was 8px)

// Generated scale:
// sp-1: 4px (was 8px)
// sp-2: 8px (was 16px)
// sp-4: 16px (was 32px)
```

### Add custom spacing values

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
    // Custom: add extra large values
    10: $base-spacing * 10,    // 80px
    12: $base-spacing * 12,    // 96px
    16: $base-spacing * 16     // 128px
) !default;
```

## 🔲 Customizing borders

### Adjust border radius scale

```scss
// tokens/_borders.scss

$border-radius: (
    none: 0,
    xs: 2px,     // Smaller (was 4px)
    sm: 4px,     // Smaller (was 6px)
    md: 6px,     // Smaller (was 8px)
    lg: 8px,     // Smaller (was 12px)
    xl: 12px,    // Smaller (was 16px)
    pill: 9999px,
    full: 50%
) !default;
```

### Custom stroke widths

```scss
$stroke-width: (
    thin: 1px,
    normal: 2px,
    thick: 3px,       // Thicker (was 4px)
    extra-thick: 6px  // New
) !default;
```

## 🌫️ Customizing shadows

### Change shadow intensity

```scss
// tokens/_shadows.scss

$base-shadow: rgb(0 0 0 / 15%) !default;  // Darker (was 10%)
```

### Adjust shadow scale

```scss
$shadows: (
    xs: 0 1px 2px $base-shadow,
    sm: 0 2px 4px $base-shadow,       // Stronger
    md: 0 4px 8px $base-shadow,       // Stronger
    lg: 0 8px 16px $base-shadow,      // Stronger
    xl: 0 16px 32px $base-shadow,     // Stronger
    inset: inset 0 2px 4px $base-shadow
) !default;
```

## ⏱️ Customizing animations

### Adjust timing

```scss
// tokens/_animations.scss

$duration: (
    instant: 0ms,
    fast: 100ms,     // Faster (was 150ms)
    normal: 200ms,   // Faster (was 300ms)
    slow: 400ms,     // Faster (was 500ms)
    slower: 600ms    // Faster (was 700ms)
) !default;
```

### Custom easing functions

```scss
$easing: (
    linear: linear,
    ease-in: ease-in,
    ease-out: ease-out,
    ease-in-out: ease-in-out,
    bounce: cubic-bezier(0.68, -0.55, 0.265, 1.55),
    // Custom: smooth elastic
    elastic: cubic-bezier(0.175, 0.885, 0.32, 1.275)
) !default;
```

## 📱 Customizing breakpoints

```scss
// tokens/_breakpoints.scss

$breakpoints: (
    xs: 320px,     // Smaller (was 360px)
    sm: 640px,     // Larger (was 576px)
    md: 768px,     // Same
    lg: 1024px,    // Same
    xl: 1280px,    // Same
    '2xl': 1920px  // Larger (was 1536px)
) !default;
```

## 🏔️ Customizing z-index

```scss
// tokens/_z-index.scss

$z-index: (
    base: 0,
    content: 100,
    header: 200,
    sidebar: 200,
    footer: 200,
    dropdown: 300,
    sticky: 400,
    modal: 500,
    tooltip: 600,
    notification: 700,
    // Custom: add debug layer
    debug: 9999
) !default;
```

## 🔧 Advanced customization

### Override specific token groups

```scss
// your-custom-tokens.scss

// Only override what you need
$primary-hue: 200deg;
$base-spacing: 4px;
$base-font-size: 14px;

// Import system with overrides
@use 'styles/main' as *;
```

### Create custom token file

```scss
// tokens/_custom.scss

$custom-tokens: (
    'card-padding': 24px,
    'nav-height': 64px,
    'sidebar-width': 280px
) !default;
```

Add to `base/_variables.scss`:

```scss
@use '../tokens/custom' as *;

$base-tokens: (
    // ... existing tokens
    custom: (
        map: $custom-tokens,
        prefix: 'custom'
    )
);
```

Usage:

```scss
.card {
    padding: var(--custom-card-padding);  // 24px → 1.5rem
}
```

## ✔️ Best practices

- ✅ **Do:** Override tokens before importing
- ✅ **Do:** Keep customizations in a separate file
- ✅ **Do:** Test changes across all breakpoints
- ✅ **Do:** Document your customizations
- ❌ **Don't:** Edit system files directly (use !default)
- ❌ **Don't:** Mix units (stick to px, let system convert to rem)
- ❌ **Don't:** Override too many values (maintain consistency)

```scss
// ✅ Good: Clean override
$primary-hue: 200deg;
$base-spacing: 4px;
@use 'styles/main' as *;

// ❌ Bad: Editing system files
// styles/tokens/_colors.scss
$primary-hue: 200deg;  // Direct edit
```