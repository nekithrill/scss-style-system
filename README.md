# 🎨 **SCSS styles system**

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

This SCSS Styles System is a modular, scalable, flexible and allows you to:

- Centralize tokens (colors, spacing, typography, shadows, radius, breakpoints, animations)
- Easily create and switch themes (light, dark, etc.)
- Use mixins and functions to generate CSS variables and reusable components
- Build layouts and UI modules based on tokens and themes
- Scale projects by adding new components, themes, and variables without breaking existing structure

## 📖 **How to use**

1. Copy the `styles/` folder into your project. No additional packages are required if SCSS compilation is already configured.

2. Use existing main.scss (from this system) or import system to your main SCSS entry point (e.g., main.scss):

   ```scss
   @use './styles/main' as *;
   ```

   This automatically includes:

   - **Tokens** (colors, spacing, typography, radius, shadows, breakpoints, animations)
   - **Themes** (light, dark, etc.)
   - **Core utilities** (mixins, functions)
   - **Base styles** (reset, globals, typography)
   - **Layout** (grid, containers)
   - **Modules** (buttons, cards, tooltips, modals)

3. Using CSS Variables

   All tokens and theme values are generated as CSS variables:

   ```scss
   .button {
   	background-color: var(--clr-primary);
   	color: var(--clr-accent);
   	padding: var(--sp-md);
   	border-radius: var(--rd-sm);
   }
   ```

4. Applying Themes

   Themes are applied using a data-theme attribute:

   ```html
   <body data-theme="light">
   	...
   </body>

   <body data-theme="dark">
   	...
   </body>
   ```

5. Responsive Utilities

   Use the included breakpoint mixin for desktop-first or mobile-first queries (true = mobile-first):

   ```scss
   @include breakpoint('md') {
   	// max-width: md
   }

   @include breakpoint('md', true) {
   	// min-width: md
   }
   ```

6. Extending and Customizing

   - Add new tokens: Create SCSS maps in `tokens/` and include them in `_variables.scss`.
   - Add new modules: Add component SCSS files in `modules/` and include them in `modules/index.scss`.
   - Override themes: Extend existing theme maps in `themes/` or create new ones.

7. Example: Button Module

   ```scss
   .button {
   	background-color: var(--clr-button-bg);
   	color: var(--clr-button-text);
   	padding: var(--sp-md) var(--sp-lg);
   	border-radius: var(--rd-sm);
   	font-family: var(--ff-primary);
   	font-weight: var(--fw-bold);
   	box-shadow: var(--shd-sm);
   	transition: all 0.2s ease;

   	&:hover {
   		background-color: var(--clr-button-bg-hover);
   	}
   }
   ```

   ```html
   <button class="button">Click me</button>
   ```

   This button automatically adapts to tokens and current theme.

## 📂 **Folder structure**

- **base/** — base styles and global rules (reset, fonts, base elements)
- **core/** — mixins, functions and variable generation
- **layout/** — grids, containers, and page structure elements
- **modules/** — reusable UI components (buttons, cards, tooltips, modals)
- **themes/** — theme maps (light, dark, etc.)
- **tokens/** — core values: colors, spacing, radius, shadows, breakpoints, animations, typography

<!-- <br> -->

<pre lang="md">
📁 styles
 ├── 📁 base
 │    ├── 📄 _fonts.scss
 │    ├── 📄 _globals.scss
 │    ├── 📄 _reset.scss
 │    └── 📄 _index.scss
 │ 
 ├── 📁 core
 │    ├── 📄 _functions.scss
 │    └── 📄 _index.scss
 │
 ├── 📁 modules
 │    ├── 📄 _module.scss
 │    └── 📄 _index.scss
 │
 ├── 📁 themes
 │    ├── 📄 _dark.scss
 │    ├── 📄 _light.scss
 │    └── 📄 _index.scss
 │
 ├── 📁 tokens
 │    ├── 📄 _animations.scss
 │    ├── 📄 _breakpoints.scss
 │    ├── 📄 _colors.scss
 │    ├── 📄 _radius.scss
 │    ├── 📄 _shadow.scss
 │    ├── 📄 _spacing.scss
 │    └── 📄 _index.scss
 │
 └── 📄 main.scss
</pre>

<br>
</details>
