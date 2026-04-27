# 🚀 Getting started

## 📋 Prerequisites

- Node.js and npm
- A project with a SCSS-compatible bundler (Vite, webpack, Next.js, etc.)

## 📥 Installation

### Step 1: Install Sass

```bash
npm install --save-dev sass
```

### Step 2: Copy the `styles/` folder to your project

```
your-project/
└── src/
    └── styles/
        ├── base/
        ├── config/
        ├── core/
        ├── themes/
        ├── tokens/
        └── main.scss
```

### Step 3: Import in your app entry point

```jsx
// main.jsx or app.jsx
import './styles/main.scss'
```

CSS custom properties are now available globally.

## ⚡️ Usage

### Component styles

```scss
.button {
	padding: var(--sp-2) var(--sp-4);
	background: var(--clr-primary-500);
	border-radius: var(--br-md);
	font-weight: var(--fw-medium);
	transition: background var(--dur-fast) var(--tf-ease-out);

	&:hover {
		background: var(--clr-primary-700);
	}
}
```

### Responsive styles

```scss
.container {
	padding: var(--sp-4);

	@include breakpoint('md') { padding: var(--sp-6); }
	@include breakpoint('lg') { padding: var(--sp-8); }
}
```

Available breakpoints: `xs` (360px), `sm` (576px), `md` (768px), `lg` (1024px), `xl` (1280px), `2xl` (1536px).

### Theming

Toggle themes by setting `data-theme` on `<html>`:

```js
document.documentElement.setAttribute('data-theme', 'dark')
document.documentElement.removeAttribute('data-theme') // back to light
```

Define semantic variables in theme files:

```scss
// themes/_light.scss
:root {
	--clr-bg:   var(--clr-secondary-100);
	--clr-text: var(--clr-neutral-900);
}

// themes/_dark.scss
[data-theme='dark'] {
	--clr-bg:   var(--clr-secondary-900);
	--clr-text: var(--clr-neutral-100);
}
```

## 🔧 Customization

```scss
// Change brand color — all 5 shades update automatically
$primary-hue: 200deg !default;

// Change base font size — all heading sizes scale proportionally
$base-font-size: 14px !default;

// Change spacing grid — all 10 steps update automatically
$base-spacing: 4px !default;
```

For a complete reference see the [token docs](../02-tokens/).

## 🔨 Manual compilation

For static sites or projects without a bundler:

```bash
npx sass src/styles/main.scss dist/styles.css
npx sass --watch src/styles/main.scss dist/styles.css
```

```html
<link rel="stylesheet" href="/dist/styles.css" />
```

## 🪲 Troubleshooting
 
**CSS variables showing as literal strings**
- Verify `sass` is installed: `npm list sass`
- Check that `main.scss` is imported in the app entry point
- Restart the dev server

**Mixin import not resolving**
 
With Vite, you can auto-import mixins globally via `additionalData` — no manual `@use` needed in every file:
 
```ts
// vite.config.ts
import path from 'path'
 
export default {
	css: {
		preprocessorOptions: {
			scss: {
				loadPaths: [path.resolve(__dirname, './src')],
				additionalData: `
					@use "styles/core/functions" as *;
					@use "styles/core/mixins" as *;
				`
			}
		}
	}
}
```
 
Without a bundler, import mixins manually at the top of each file that uses them:
 
```scss
@use '../core/mixins/breakpoint' as *;
```
 
**Styles not updating after changes**
- Hard refresh: `Ctrl + Shift + R` / `Cmd + Shift + R`
- Clear Vite cache: `rm -rf node_modules/.vite`