# 🏗️ Architecture

The system uses a two-layer architecture that separates raw values from context-aware usage.

## 📚 Layers

**Layer 1: Design tokens** — concrete values, same in every theme.

```scss
// tokens/_colors.scss
$neutral: (
	100: oklch(96% 0.008 220deg),
	900: oklch(18% 0.01 220deg)
) !default;
```

Generated as CSS custom properties in `:root`:

```css
--clr-neutral-100: oklch(96% 0.008 220deg);
--clr-neutral-900: oklch(18% 0.01 220deg);
```

**Layer 2: Semantic theme variables** — context-aware, change per theme.

```scss
// themes/_light.scss
:root { --clr-text: var(--clr-neutral-900); }

// themes/_dark.scss
[data-theme='dark'] { --clr-text: var(--clr-neutral-100); }
```

Components reference semantic variables, not raw tokens:

```scss
body { color: var(--clr-text); } // ← adapts to any theme automatically
```

## 🌊 Flow

```
┌─────────────────────────────────────────────────────────┐
│ Design tokens  (tokens/*.scss)                          │
│                                                         │
│ $primary: (500: oklch(60% 0.2 270deg))                  │
│ $spacing: (4: 32px)                                     │
└──────────────────────────┬──────────────────────────────┘
                           ↓ generate-tokens mixin
┌─────────────────────────────────────────────────────────┐
│ CSS custom properties  (:root)                          │
│                                                         │
│ --clr-primary-500: oklch(60% 0.2 270deg)                │
│ --sp-4: 2rem                                            │
└──────────┬───────────────────────────────┬──────────────┘
           │                               │
           ↓ optional                      ↓ direct
┌─────────────────────┐       ┌────────────────────────────┐
│ Semantic themes     │       │ Component styles           │
│                     │       │                            │
│ --clr-bg            │       │ .card {                    │
│ --clr-text          │       │   padding: var(--sp-4);    │
│ --clr-focus         │       │   color: var(--clr-text);  │
└─────────────────────┘       │ }                          │
                              └────────────────────────────┘
```

## 🚦 Imports order

```scss
// 1. Tokens
@use './tokens/animations' as *;
@use './tokens/breakpoints' as *;
@use './tokens/colors' as *;
@use './tokens/borders' as *;
@use './tokens/shadows' as *;
@use './tokens/spacing' as *;
@use './tokens/typography' as *;
@use './tokens/z-index' as *;

// 2. Core (mixins & functions)
@use './core/functions/px-to-rem' as *;
@use './core/mixins/breakpoint' as *;
@use './core/mixins/generate-tokens' as *;

// 3. Config
@use './config/variables' as *;

// 4. Base styles
@use './base/reset' as *;
@use './base/fonts' as *;
@use './base/globals' as *;
@use './base/focus' as *;
@use './base/scrollbar' as *;
@use './base/selection' as *;

// 5. Themes
@use './themes/light' as *;
@use './themes/dark' as *;
```

Order matters — `variables` must come before `themes` and `globals`, as those files reference the generated CSS custom properties.