# 🎨 **SCSS Style System**

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

A flexible and extensible SCSS Style System with theme support, automatic CSS variable generation, and validation.

---

## 🔍 **Overview**

### **Token-First Architecture**

- **Tokens** define raw design values (colors, spacing, typography, shadows, radii, animations)
- **Themes** map tokens to semantic meanings with light/dark mode support
- **Core utilities** generate CSS variables with automatic px → rem conversion
- **Base styles** apply global styling and resets

### **Key Features**

✅ Centralized design tokens  
✅ Easy theme switching (light, dark, custom)  
✅ OKLCH colors for perceptual uniformity  
✅ Automatic px → rem conversion  
✅ Theme validation and schema enforcement  
✅ Responsive breakpoints and mixins  
✅ Modular architecture — import only what you need

---

## 📖 **How to use**

Ensure Sass is installed:

```bash
npm install -g sass
# or
npm install --save-dev sass
```

### **Option A: Standalone Usage**

Use this system as your main styling solution.

**1. Copy files**

Copy `/styles` folder to your project root.

**2. Compile** _(skip if you have a build tool)_

```bash
sass styles/main.scss dist/styles.css
```

### **Option B: Integration with Existing System**

Import into your existing SCSS project.

**1. Copy files**

Copy `/styles` folder to your project.

**2. Import**

```scss
// your-main.scss
@use 'styles/main';
```

**3. Compile** _(skip if you have a build tool)_

```bash
sass your-main.scss dist/styles.css
```

---

## 📚 Documentation

Complete guides for architecture, tokens, themes, and customization.

- [📖 Open docs](docs/README.md)
