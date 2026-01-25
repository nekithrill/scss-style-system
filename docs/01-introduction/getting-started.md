## 🚀 Getting started

Get up and running with the SCSS Style System in minutes.

<br>

### Prerequisites

- **Node.js** and **npm** installed
- **A project** with one of:
  - React + Vite
  - Next.js
  - Any bundler with SCSS support (Webpack, Parcel, etc.)

> 💡 **No manual compilation needed!** Modern bundlers handle SCSS automatically.

---

### Quick Setup (2 steps)

#### 1. Install Sass

```bash
npm install --save-dev sass
```

That's it! Your bundler (Vite, Next.js, etc.) will automatically compile SCSS.

#### 2. Copy the `styles/` folder to your project

```
your-project/
├── src/
│   └── styles/         ← Copy here (or anywhere in src/)
│       ├── tokens/
│       ├── core/
│       ├── base/
│       ├── themes/
│       └── main.scss
```

Done! CSS variables are now available. 🎉

---

### Integration Methods

<details open>
<summary><b>Option A: React + Vite</b> (Most Common)</summary>

**1. Import base styles once** (in `main.jsx` or `App.jsx`):

```jsx
// src/main.jsx
import './styles/main.scss';  // Import once globally
import App from './App';

// ... rest of your setup
```

**2. Use CSS variables in component styles:**

```scss
// src/components/Card/Card.module.scss
.card {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    border-radius: var(--rd-md);
    
    &:hover {
        background: var(--clr-primary-600);
    }
}
```

```jsx
// src/components/Card/Card.jsx
import styles from './Card.module.scss';

export function Card({ children }) {
    return <div className={styles.card}>{children}</div>;
}
```

**3. Import mixins when needed:**

```scss
// src/components/Container/Container.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.container {
    padding: var(--sp-6);
    
    @include breakpoint('md') {
        padding: var(--sp-4);
    }
    
    @include breakpoint('sm') {
        padding: var(--sp-2);
    }
}
```

**Path alias setup** (optional but recommended):

```js
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
});
```

</details>

<details>
<summary><b>Option B: Next.js</b></summary>

**1. Import base styles** (in `_app.jsx` or `layout.jsx`):

```jsx
// pages/_app.jsx (Pages Router)
import '@/styles/main.scss';

export default function App({ Component, pageProps }) {
    return <Component {...pageProps} />;
}
```

```jsx
// app/layout.jsx (App Router)
import '@/styles/main.scss';

export default function RootLayout({ children }) {
    return (
        <html lang="en">
            <body>{children}</body>
        </html>
    );
}
```

**2. Use in component modules:**

```scss
// components/Card/Card.module.scss
.card {
    padding: var(--sp-4);
    background: var(--clr-main-bg);
    color: var(--clr-main-text);
}
```

```jsx
import styles from './Card.module.scss';

export function Card() {
    return <div className={styles.card}>Content</div>;
}
```

**Path aliases** (already configured in Next.js):
- `@/styles/...` works out of the box
- Or use relative paths: `../../styles/...`

</details>

<details>
<summary><b>Option C: Standalone HTML/CSS</b></summary>

If you need to compile manually (for static sites, legacy projects):

```bash
# Install Sass CLI
npm install --save-dev sass

# Compile once
npx sass src/styles/main.scss dist/styles.css

# Watch mode
npx sass --watch src/styles/main.scss:dist/styles.css
```

**Add to package.json:**
```json
{
  "scripts": {
    "build:css": "sass src/styles/main.scss dist/styles.css",
    "watch:css": "sass --watch src/styles/main.scss:dist/styles.css"
  }
}
```

**Link in HTML:**
```html
<link rel="stylesheet" href="/dist/styles.css">
```

</details>

---

### Usage Examples

#### CSS Variables in Component Styles

```scss
// Button.module.scss
.button {
    /* Spacing */
    padding: var(--sp-2) var(--sp-4);
    
    /* Colors */
    background: var(--clr-primary-500);
    color: var(--clr-neutral-100);
    
    /* Borders */
    border: none;
    border-radius: var(--rd-md);
    
    /* Typography */
    font-size: var(--fs-default);
    font-weight: var(--fw-medium);
    
    /* Animation */
    transition: all var(--dur-fast) var(--tf-ease-out);
    
    &:hover {
        background: var(--clr-primary-600);
        transform: translateY(-1px);
        box-shadow: var(--shadow-md);
    }
}
```

#### SCSS Mixins

```scss
// Container.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.container {
    max-width: 1280px;
    margin: 0 auto;
    padding: var(--sp-6);
    
    @include breakpoint('lg') {
        padding: var(--sp-4);
    }
    
    @include breakpoint('md') {
        padding: var(--sp-3);
    }
    
    @include breakpoint('sm') {
        padding: var(--sp-2);
    }
}
```

#### Theme Variables

```scss
// Card.module.scss
.card {
    /* Use theme-aware variables */
    background: var(--clr-main-bg);
    color: var(--clr-main-text);
    
    /* Mix with base tokens */
    padding: var(--sp-4);
    border-radius: var(--rd-lg);
    box-shadow: var(--shadow-md);
    
    &:hover {
        background: var(--clr-main-bg-hover);
    }
}
```

Works automatically with light/dark themes!

---

### Available Variables

<details>
<summary><b>Colors</b> (OKLCH system)</summary>

```css
/* Brand colors (9 shades each) */
--clr-primary-100 ... --clr-primary-900
--clr-secondary-100 ... --clr-secondary-900
--clr-neutral-100 ... --clr-neutral-900

/* Semantic colors */
--clr-success-bg, --clr-success-text, --clr-success-solid
--clr-warning-bg, --clr-warning-text, --clr-warning-solid
--clr-danger-bg, --clr-danger-text, --clr-danger-solid
--clr-info-bg, --clr-info-text, --clr-info-solid

/* Theme variables (if using themes) */
--clr-main-bg, --clr-main-text
--clr-header-bg, --clr-header-text
```

See [Colors](../02-tokens/colors.md) for complete reference.
</details>

<details>
<summary><b>Spacing</b> (8px grid → rem)</summary>

```css
--sp-0: 0
--sp-1: 0.5rem    /* 8px */
--sp-2: 1rem      /* 16px */
--sp-3: 1.5rem    /* 24px */
--sp-4: 2rem      /* 32px */
--sp-5: 2.5rem    /* 40px */
--sp-6: 3rem      /* 48px */
--sp-7: 3.5rem    /* 56px */
--sp-8: 4rem      /* 64px */
```

See [Spacing](../02-tokens/spacing.md)
</details>

<details>
<summary><b>Typography</b></summary>

```css
/* Font families */
--ff-primary: 'JetBrains', system-ui, sans-serif
--ff-accent: 'Tektur', system-ui, sans-serif
--ff-system: system-ui, sans-serif

/* Font weights */
--fw-light: 300
--fw-regular: 400
--fw-medium: 500
--fw-bold: 700
--fw-extra-bold: 800

/* Font sizes (rem, scales with $base-font-size) */
--fs-default: 1rem      /* 16px */
--fs-h1: 1.875rem       /* 30px */
--fs-h2: 1.5rem         /* 24px */
--fs-h3: 1.25rem        /* 20px */
--fs-h4: 1.125rem       /* 18px */
--fs-h5: 1rem           /* 16px */
--fs-h6: 0.875rem       /* 14px */
```

See [Typography](../02-tokens/typography.md)
</details>

<details>
<summary><b>Borders & Shadows</b></summary>

```css
/* Border radius */
--rd-none: 0
--rd-xs: 0.25rem
--rd-sm: 0.375rem
--rd-md: 0.5rem
--rd-lg: 0.75rem
--rd-xl: 1rem
--rd-pill: 9999px
--rd-full: 50%

/* Stroke widths */
--stroke-thin: 1px
--stroke-normal: 2px
--stroke-thick: 4px

/* Shadows */
--shadow-xs, --shadow-sm, --shadow-md
--shadow-lg, --shadow-xl, --shadow-inset
```

See [Borders](../02-tokens/borders.md), [Shadows](../02-tokens/shadows.md)
</details>

<details>
<summary><b>Animations & Z-index</b></summary>

```css
/* Duration */
--dur-instant: 0.1s
--dur-fast: 0.15s
--dur-normal: 0.3s
--dur-slow: 0.5s
--dur-slower: 0.7s

/* Easing (timing functions) */
--tf-linear, --tf-ease-in, --tf-ease-out
--tf-ease-in-out, --tf-bounce

/* Z-index layers */
--z-base: 0
--z-content: 100
--z-header: 200
--z-dropdown: 300
--z-modal: 500
--z-tooltip: 600
```

See [Animations](../02-tokens/animations.md), [Z-index](../02-tokens/z-index.md)
</details>

---

### Quick Customization

Change your brand color in one line:

```scss
// src/styles/tokens/_colors.scss
$primary-hue: 200deg !default;  // Blue instead of purple
```

Save and refresh - all 9 shades become blue automatically! 🎉

**More customization:**
- **Spacing:** Change `$base-spacing: 4px` for tighter layout
- **Typography:** Change `$base-font-size: 14px` for smaller text
- **Borders:** Adjust radius scale in `_borders.scss`

See [Customizing](../06-usage/customizing.md) for complete guide.

---

### Verify Setup

**1. Check CSS variables are loaded:**

Open browser DevTools → Console:
```js
getComputedStyle(document.documentElement).getPropertyValue('--clr-primary-500')
// Should return: "oklch(60% 0.2 270deg)" or similar
```

**2. Test in a component:**

```jsx
// TestComponent.jsx
export function Test() {
    return (
        <div style={{
            padding: 'var(--sp-4)',
            background: 'var(--clr-primary-500)',
            color: 'white',
            borderRadius: 'var(--rd-md)'
        }}>
            If you see a purple box with padding, it works! ✅
        </div>
    );
}
```

---

### Troubleshooting

**Variables showing as literal strings?**
- ✅ Check `sass` is installed: `npm list sass`
- ✅ Verify `main.scss` is imported in your app entry point
- ✅ Restart dev server after installing sass

**Mixins not working?**
- ✅ Check import path: `@use '@/styles/core/mixins/breakpoint'`
- ✅ Verify path alias configured (Vite: `vite.config.js`)
- ✅ Use `.scss` extension for files using mixins

**Styles not updating?**
- ✅ Hard refresh browser: `Ctrl/Cmd + Shift + R`
- ✅ Restart dev server
- ✅ Clear Vite cache: `rm -rf node_modules/.vite`

**Build errors in production?**
- ✅ Ensure `sass` is in dependencies (not devDependencies) if deploying to platforms like Vercel
- ✅ Check all import paths are correct

---

### Need Help?

- 📚 Browse the [full documentation](../README.md)
- 🐛 Found a bug? Open an issue
- 💬 Have questions? Start a discussion