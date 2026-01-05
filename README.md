# 🎨 SCSS Style System

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

A modular design token system for generating CSS variables with optional theming support. Built to work seamlessly with component-scoped styling (SCSS modules, CSS-in-JS).

## ✨ Key Features

- 🎯 **Token-first architecture** - centralized design values
- 🎨 **Optional theming** - light/dark/custom modes with validation
- 🔧 **Utility mixins** - breakpoints, token generation, helpers
- 📐 **Auto conversion** - px to rem with design tokens
- 🎨 **OKLCH colors** - perceptually uniform color system
- 🧩 **Fully modular** - remove unused features easily


<br>

## 🚀 Quick Start

```bash
npm install --save-dev sass
```

### Installation

**1. Copy the `/styles` folder to your project**

**2. Choose your integration method:**

**Option A: Standalone (main stylesheet)**
```bash
sass styles/main.scss dist/styles.css
```
```html
<link rel="stylesheet" href="/dist/styles.css" />
```

**Option B: Component-scoped (recommended)**
```scss
// Component.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.card {
	padding: var(--sp-4);
	background: var(--theme-main-bg);
	
	@include breakpoint('md') {
		padding: var(--sp-2);
	}
}
```

**Option C: Existing SCSS workflow**
```scss
// your-styles.scss
@use 'styles/main';

.your-component {
	color: var(--clr-primary-500);
}
```

> 💡 **Recommended:** Use component-scoped approach (Option B) for maximum flexibility. The base system compiles separately: `sass styles/main.scss dist/base.css`

<br>

## 🎯 What's Included

- **Design Tokens** - Colors, spacing, typography, radius, shadows (core)
- **CSS Variables** - Auto-generated with px → rem conversion (core)
- **Themes** - Light/dark/custom modes (optional)
- **Mixins** - Breakpoints, utilities, helpers (optional)
- **Base Styles** - Reset, globals, scrollbar (optional)

<br>

## 💡 Best Used For

- ✅ Projects with SCSS modules or CSS-in-JS
- ✅ Design systems with centralized tokens
- ✅ Multi-theme applications (light/dark mode)
- ✅ Projects needing modular, removable features

**Not a good fit?** Consider [Tailwind CSS](https://tailwindcss.com/) for utility-first, or vanilla CSS variables for zero build step.

<br>

## 🛠️ Example Usage
```scss
// Component.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.card {
	// System tokens
	padding: var(--sp-4);
	border-radius: var(--rd-md);
	background: var(--clr-main-bg);
	color: var(--clr-main-text);
	
	// System mixin
	@include breakpoint('md') {
		padding: var(--sp-6);
	}
	
	&:hover {
		background: var(--clr-main-bg-hover);
	}
}
```

<br>

## 📖 Documentation

**[📚 View full documentation](docs/README.md)**

Learn about architecture, customization, theme setup, and advanced usage.