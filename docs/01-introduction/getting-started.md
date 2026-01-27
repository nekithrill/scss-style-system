## 🚀 Getting started

Get up and running with the SCSS Style System in minutes.

<br>

### 📋 Prerequisites

- **Node.js** and **npm** installed
- **A project** with React + Vite, Next.js, or any SCSS-compatible bundler

> 💡 **No manual compilation needed!** Modern bundlers handle SCSS automatically.

---

### ⚡ Quick setup

#### Step 1: Install Sass

```bash
npm install --save-dev sass
```

#### Step 2: Copy the `styles/` folder to your project

```
your-project/
├── src/
│   └── styles/         ← Copy here
│       ├── tokens/
│       ├── core/
│       ├── base/
│       ├── themes/
│       └── main.scss
```

Done! 🎉

---

### 🔌 Integration

#### Modern bundlers (React, Next.js, Vite)

**1. Import once in your app entry:**

```jsx
// main.jsx or _app.jsx
import './styles/main.scss';
```

**2. Use variables in component styles:**

```scss
// Button.module.scss
.button {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    border-radius: var(--rd-md);
    
    &:hover {
        background: var(--clr-primary-600);
    }
}
```

**3. Import mixins when needed:**

```scss
@use '@/styles/core/mixins/breakpoint' as *;

.container {
    padding: var(--sp-6);
    
    @include breakpoint('md') {
        padding: var(--sp-4);
    }
}
```

<details>
<summary><b>Path alias setup</b> (Vite)</summary>

```js
// vite.config.js
import { defineConfig } from 'vite';
import path from 'path';

export default defineConfig({
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
});
```

Next.js has `@/` alias by default.
</details>

#### Manual compilation (static sites)

```bash
npm install --save-dev sass
npx sass src/styles/main.scss dist/styles.css
```

```html
<link rel="stylesheet" href="/dist/styles.css">
```

---

### 💡 Usage examples

#### Component styling

```scss
.card {
    padding: var(--sp-4);                /* Spacing */
    background: var(--clr-primary-500);  /* Color */
    border-radius: var(--rd-lg);         /* Border */
    box-shadow: var(--shadow-md);        /* Shadow */
    font-size: var(--fs-h3);             /* Typography */
}
```

#### Responsive design

```scss
@use '@/styles/core/mixins/breakpoint' as *;

.container {
    padding: var(--sp-6);
    
    @include breakpoint('md') {
        padding: var(--sp-4);
    }
}
```

#### Theme-aware

```scss
.card {
    background: var(--clr-main-bg);    /* Auto light/dark */
    color: var(--clr-main-text);
}
```

<details>
<summary><b>Available variables</b></summary>

**Colors:**
```css
--clr-primary-100 ... --clr-primary-900
--clr-secondary-100 ... --clr-secondary-900
--clr-neutral-100 ... --clr-neutral-900
--clr-success-bg, --clr-warning-bg, --clr-danger-bg
```

**Spacing:** (8px grid → rem)
```css
--sp-0: 0
--sp-1: 0.5rem    /* 8px */
--sp-2: 1rem      /* 16px */
--sp-4: 2rem      /* 32px */
--sp-6: 3rem      /* 48px */
--sp-8: 4rem      /* 64px */
```

**Typography:**
```css
--ff-primary, --ff-accent, --ff-system
--fw-light, --fw-regular, --fw-medium, --fw-bold
--fs-default, --fs-h1, --fs-h2, --fs-h3, --fs-h4
```

**Borders & Shadows:**
```css
--rd-none, --rd-xs, --rd-sm, --rd-md, --rd-lg, --rd-xl, --rd-pill, --rd-full
--stroke-thin, --stroke-normal, --stroke-thick
--shadow-xs, --shadow-sm, --shadow-md, --shadow-lg, --shadow-xl
```

**Animations:**
```css
--dur-instant, --dur-fast, --dur-normal, --dur-slow
--tf-linear, --tf-ease-in, --tf-ease-out, --tf-ease-in-out
```

See token docs for complete reference: [Colors](../02-tokens/colors.md), [Spacing](../02-tokens/spacing.md), [Typography](../02-tokens/typography.md), [Borders](../02-tokens/borders.md), [Shadows](../02-tokens/shadows.md), [Animations](../02-tokens/animations.md)
</details>

---

### 🎨 Customization

Change your brand color:

```scss
// styles/tokens/_colors.scss
$primary-hue: 200deg !default;  // Blue instead of purple
```

All 9 shades update automatically! 🎉

**More options:**
- **Spacing:** `$base-spacing: 4px` (tighter layout)
- **Typography:** `$base-font-size: 14px` (smaller text)
- **Borders:** Adjust radius in `_borders.scss`

See [Customizing guide](../06-usage/customizing.md) for details.

---

### 🐛 Troubleshooting

**Variables showing as literal strings?**
- Check `sass` installed: `npm list sass`
- Verify `main.scss` imported in app entry
- Restart dev server

**Mixins not working?**
- Check path: `@use '@/styles/core/mixins/breakpoint'`
- Configure path alias in `vite.config.js`

**Styles not updating?**
- Hard refresh: `Ctrl/Cmd + Shift + R`
- Clear cache: `rm -rf node_modules/.vite`