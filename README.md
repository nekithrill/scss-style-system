# 🎨 SCSS Style System

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

A modular design token system for generating CSS variables with optional theming support. Built to work seamlessly with component-scoped styling (SCSS modules, CSS-in-JS).

---

## ✨ Key Features

- 🎯 **Token-first architecture** - centralized design values
- 🎨 **Optional theming** - light/dark/custom modes with validation
- 🔧 **Utility mixins** - breakpoints, token generation, helpers
- 📐 **Auto conversion** - px to rem with design tokens
- 🎨 **OKLCH colors** - perceptually uniform color system
- 🧩 **Fully modular** - remove unused features easily

---

## 🔍 What This System Provides

| Layer             | Purpose                                        | Optional    |
| ----------------- | ---------------------------------------------- | ----------- |
| **Design Tokens** | Raw values (colors, spacing, typography, etc.) | ❌ Core     |
| **CSS Variables** | Generated from tokens with auto px → rem       | ❌ Core     |
| **Themes**        | Light/dark/custom modes with semantic mappings | ✅ Optional |
| **Mixins**        | Breakpoints, utilities, helpers                | ✅ Optional |
| **Base Styles**   | Reset, globals, scrollbar, selection           | ✅ Optional |

---

## 💡 Recommended Usage

This system is designed as a **foundation layer** that works with component-scoped styling:

```
┌─────────────────────────────────────────┐
│ SCSS Style System (this)                │
│ • Design tokens                         │
│ • CSS variables                         │
│ • Optional themes                       │
│ • Utility mixins                        │
└─────────────────┬───────────────────────┘
                  │
                  ↓
┌─────────────────────────────────────────┐
│ Your Components                         │
│ • SCSS Modules                          │
│ • CSS-in-JS                             │
│ • Component-scoped styles               │
└─────────────────────────────────────────┘
```

**Example:**

```scss
// Component.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.card {
	padding: var(--sp-4); // System token
	background: var(--theme-main-bg); // System theme (optional)

	@include breakpoint('md') {
		// System mixin
		padding: var(--sp-2);
	}
}
```

---

## 🚀 Quick Start

### Prerequisites

```bash
npm install --save-dev sass
# or install globally
npm install -g sass
```

### Option 1: Standalone Usage

Use as your main styling solution.

**1. Copy files to your project:**

```
your-project/
└── styles/          ← Copy this folder
    ├── tokens/
    ├── themes/
    ├── base/
    └── main.scss
```

**2. Compile:**

```bash
sass styles/main.scss dist/styles.css
```

**3. Link in HTML:**

```html
<link rel="stylesheet" href="/dist/styles.css" />
```

---

### Option 2: Integration with Existing System

Import into your existing SCSS workflow.

**1. Copy `/styles` folder to your project**

**2. Import in your main SCSS file:**

```scss
// your-styles.scss
@use 'styles/main';

// Your custom styles here
.your-component {
	color: var(--clr-primary-500); // Use system tokens
}
```

**3. Compile:**

```bash
sass your-styles.scss dist/styles.css
```

---

### Option 3: Component-Scoped (Recommended)

Use with SCSS modules or CSS-in-JS.

**1. Copy `/styles` folder**

**2. Import only what you need:**

```scss
// Component.module.scss
@use '@/styles/core/mixins/breakpoint' as *;

.component {
	padding: var(--sp-4); // Use tokens

	@include breakpoint('md') {
		// Use mixins
		padding: var(--sp-2);
	}
}
```

**3. Base system compiles separately:**

```bash
sass styles/main.scss dist/base.css
```

---

## 🎯 When to Use This System

### ✅ Good fit for:

- Projects using SCSS modules or CSS-in-JS
- Design systems needing centralized tokens
- Multi-theme applications (light/dark mode)
- Consistent spacing, typography and others
- Projects that need modular, removable features

### ⚠️ Consider alternatives if:

- You need utility-first CSS (use Tailwind CSS)
- You want zero build step (use vanilla CSS + variables)
- You need class-based components (use Bootstrap/Bulma)
- Project is pure HTML/CSS without SCSS

---

## 📖 Documentation

Comprehensive guides for architecture, customization, and usage.

**[📚 View full documentation →](docs/README.md)**
