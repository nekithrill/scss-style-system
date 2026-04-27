# 🎨 SCSS Style System

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

A modular SCSS design token system that generates CSS custom properties with built-in theming support. Designed for component-based projects using CSS Modules or scoped styles.

## ✨ Key features

- **Token-first architecture** — centralized design values, single source of truth
- **OKLCH color system** — perceptually uniform palettes, hue-based generation
- **Automatic rem conversion** — define in px, output in rem
- **Light / dark theming** — plain CSS custom properties, no mixins or schema required
- **Responsive mixins** — mobile-first breakpoints out of the box
- **Fully modular** — every file is optional, use only what you need

## 🚀 Quick start

**1. Install Sass**

```bash
npm install --save-dev sass
```

**2. Copy `styles/` to your project**

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

**3. Import once in your app entry**

```jsx
// main.jsx or app.jsx
import './styles/main.scss'
```

**4. Use in components**

```scss
.card {
	padding: var(--sp-4);
	background: var(--clr-primary-500);
	border-radius: var(--br-md);
	box-shadow: var(--shadow-md);
}
```

Full setup guide: [Getting started](docs/01-introduction/getting-started.md)

## 🎨 Customization

Change brand color — all five shades update automatically:

```scss
// tokens/_colors.scss
$primary-hue: 200deg !default; // Blue instead of purple
```

Change base font size — all headings scale proportionally:

```scss
// tokens/_typography.scss
$base-font-size: 14px !default;
```

Change spacing grid — all ten steps update:

```scss
// tokens/_spacing.scss
$base-spacing: 4px !default;
```

## 📦 What's included

| Group | Description |
|-------|-------------|
| **Tokens** | Colors, typography, spacing, borders, shadows, animations, z-index, breakpoints |
| **Core** | `px-to-rem` function, `breakpoint` mixin, `generate-tokens` mixin |
| **Base** | Reset, globals, fonts, focus, scrollbar, selection |
| **Themes** | Light and dark mode templates |

## 🌐 Browser support

Requires CSS custom properties support — all modern browsers. IE11 is not supported.

## 📖 Documentation

**[View full documentation](docs/README.md)**