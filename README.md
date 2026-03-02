# 🎨 SCSS Style System

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

A modular design token system for generating CSS variables with built-in theming support. Built to work seamlessly with component-scoped styling (SCSS modules, CSS-in-JS).

<br>

## ✨ Key Features

- 🎯 **Token-first architecture** - centralized design values
- 🎨 **Optional theming** - light/dark/custom modes
- 🔧 **Utility mixins** - breakpoints, token generation, helpers
- 📐 **Auto conversion** - px to rem with design tokens
- 🎨 **OKLCH colors** - perceptually uniform color system
- 🧩 **Fully modular** - remove unused features easily

<br>

## 🚀 Quick Start

### Step 1: Install Sass
```bash
npm install --save-dev sass
```

### Step 2: Copy `styles/` folder to your project
```
your-project/
├── src/
│   └── styles/         ← Copy here
```

### Step 3: Import in your app
```jsx
// main.jsx or _app.jsx
import './styles/main.scss';
```

### Step 4: Use variables in your styles
```scss
// Component.module.scss
.card {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    border-radius: var(--rd-md);
}
```

**Full guide:** [Getting Started](docs/01-introduction/getting-started.md)

<br>

## 🎨 Quick Customization

Change your brand color with one line:

```scss
// styles/tokens/_colors.scss
$primary-hue: 200deg !default; // Blue instead of purple
```

All 9 shades (100-900) update automatically! 🎉

**More:** [Customization guide](docs/06-usage/customizing.md)

<br>

## 🛠️ Example Usage

```scss
// Component.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.card {
    // Design tokens
    padding: var(--sp-4);
    border-radius: var(--rd-md);
    background: var(--clr-main-bg);
    color: var(--clr-main-text);

    // Responsive
    @include breakpoint('md') {
        padding: var(--sp-6);
    }

    // Theme-aware
    &:hover {
        background: var(--clr-main-bg-hover);
    }
}
```

<br>

## 🎯 What's Included

- **Design Tokens** - Colors, spacing, typography, borders, shadows, animations
- **CSS Variables** - Auto-generated with px → rem conversion
- **Themes** (optional) - Light/dark mode
- **Mixins** (optional) - Breakpoints, utilities, helpers
- **Base Styles** (optional) - Reset, globals, scrollbar

<br>

## 💡 Best Used For

- ✅ Component-based projects (React, Vue, Svelte)
- ✅ Design systems with centralized tokens
- ✅ Multi-theme applications (light/dark mode)
- ✅ Projects needing modular, removable features

**Not a good fit?** Consider [Tailwind CSS](https://tailwindcss.com/) for utility-first, or vanilla CSS variables for zero build step.

<br>

## 🌐 Browser Support

- ✅ Chrome 49+ (2016)
- ✅ Firefox 31+ (2014)
- ✅ Safari 9.1+ (2016)
- ✅ Edge 15+ (2017)
- ❌ IE11 not supported (requires CSS custom properties)

<br>

## 📖 Documentation

**[📚 View full documentation](docs/README.md)**
