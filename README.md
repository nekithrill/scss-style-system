# 🎨 **SCSS styles system**

[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css&logoColor=ffffff)](https://www.w3.org/TR/CSS/)
[![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=ffffff)](https://sass-lang.com/)

This SCSS Styles System is modular, scalable, and flexible, allowing you to:

- Centralize tokens (colors, spacing, typography, shadows, radius, breakpoints, animations)
- Easily create and switch themes (light, dark, custom themes)
- Use mixins and functions to generate CSS variables and reusable patterns
- Scale projects by adding new tokens, themes, and styles without breaking existing structure

<br>

## 📖 **How to use**

1. Copy the `styles/` folder into your project. No additional packages are required if SCSS compilation is already configured.

2. Use existing main.scss (from this system) or import system to your main SCSS entry point (e.g., main.scss):

   ```scss
   @use './styles/main' as *;
   ```

   This automatically includes:
   - **Tokens** (colors, spacing, typography, radius, shadows, breakpoints, animations)
   - **Themes** (theme-schema, light, dark, etc.)
   - **Core utilities** (mixins, functions, variables)
   - **Base styles** (reset, globals, typography)

3. Customize tokens and themes

   General variables are generated in `_variables.scss`.

   Theme variables are generated in theme's module, such as `_dark.scss` or `_light.scss` and applied using a data-theme attribute:

   ```html
   <body data-theme="light">
   	...
   </body>
   <body data-theme="dark">
   	...
   </body>
   ```

4. Responsive Utilities

   Use the included breakpoint mixin for desktop-first or mobile-first queries (true = mobile-first):

   ```scss
   @include breakpoint('md') {
   	// max-width: md
   }

   @include breakpoint('md', true) {
   	// min-width: md
   }
   ```

<br>

## 🧩 **Configuration**

<details>
<summary><strong>Variables</strong></summary>

<br>

To configure variables you need to edit `/tokens/*`, for example `/tokens/_typography.scss`:

```scss
/// Typography Tokens
///
/// Core typography settings:
/// - Font families: primary, accent (optional)
/// - Font weights: light, regular, medium, bold, black
/// - Font sizes: default + h1–h6, automatically converted to rems (in /core/variables)

$font-families: (
	primary: 'JetBrains, sans-serif',
	accent: 'Tektur, sans-serif'
);

$font-weights: (
	light: 300,
	regular: 400,
	medium: 500,
	bold: 700,
	black: 900
);

$font-sizes: (
	default: 16px,
	h1: 30px,
	h2: 24px,
	h3: 20px,
	h4: 18px,
	h5: 16px,
	h6: 14px
);
```

Then to edit `/core/_variables.scss` for generation CSS variables:

```scss
$tokens: (
	colors: (
		map: $colors,
		prefix: 'clr'
	),
	font-families: (
		map: $font-families,
		prefix: 'ff'
	),
	font-weights: (
		map: $font-weights,
		prefix: 'fw'
	),
	font-sizes: (
		map: $font-sizes,
		prefix: 'fs',
		transform: 'rem'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	),
	radius: (
		map: $radius,
		prefix: 'rd',
		transform: 'rem'
	),
	shadows: (
		map: $shadows,
		prefix: 'shd',
		transform: 'rem'
	)
);

:root {
	@include generate-tokens($tokens);
}
```

> 💡 if you want another prefixes, change prefix value in group

> 💡 to generate variables, generate-tokens mixin exists in `/core/mixins`

<br>
</details>

<details>
<summary><strong>Fonts</strong></summary>

<br>

To configure fonts you need to edit `/base/_fonts.scss` file in which fonts are connected.

```scss
/// Font Loading Guidelines
///
/// 1️ Use `.woff2` fonts for optimal loading and modern browser support.
/// 2️⃣ Include `.woff` as a fallback for older browsers.
/// 3️⃣ Include multiple weights/styles in separate `@font-face` declarations.
/// 4️⃣ For variable fonts, define a range of weights in one declaration.
///
/// - Always use `font-display: swap` to improve UX and avoid invisible text.
/// - Keep file paths relative to your CSS/SCSS file location.
/// - Include all font weights used in your project.
/// - Consider hosting fonts locally for faster loading and offline support.
/// - Variable fonts can be animated or have dynamic weight changes with CSS.

@font-face {
	font-family: 'CustomFont';
	font-weight: 400;
	font-style: normal;
	font-display: swap;
	src:
		url('path/to/CustomFont.woff2') format('woff2'),
		url('path/to/CustomFont.woff') format('woff');
}
```

<br>
</details>

<details>
<summary><strong>Themes</strong></summary>

<br>

To configure themes, first you need to edit colors `/tokens/_colors.scss`:

```scss
@use 'sass:color';

/// Color Tokens
///
/// Defines the core color palette for the project:
/// - $brand-color: base brand color
/// - $colors: derived colors for consistent theming
///
/// Notes:
/// - Colors are defined using HSL for easier manipulation with `color.adjust()`
/// - Derived colors help maintain visual hierarchy and consistency

$brand-color: hsl(40deg 100% 50%);
$colors: (
	accent: $brand-color,
	primary: color.adjust($brand-color, $saturation: -60%, $lightness: +30%),
	secondary: color.adjust($brand-color, $saturation: -80%, $lightness: -20%),
	neutral: color.adjust($brand-color, $saturation: -100%, $lightness: -30%)
);
```

> 💡 HSL is comfortable to setup shades with color.adjust().

then to setup your layout schema in `/themes/_theme-schema.scss`:

```scss
/// Theme Schema
///
/// Defines the required structure for theme maps in the project.
///
/// $theme-required-keys:
/// - Specifies which keys and nested keys must exist in a theme
/// - Used to validate themes before generating CSS variables
/// - Ensures consistency and completeness across different themes
///
/// $theme-allowed-states:
/// - Lists all valid "state" keys that can exist at the lowest level of a theme map
/// - Examples of states: '_', 'hover', 'active', 'focus', 'disabled', 'muted', etc.
/// - Used during theme validation to allow these keys without triggering warnings
/// - Ensures that developers cannot accidentally add arbitrary keys at the state level

$theme-allowed-states: (
	'_',
	'hover',
	'active',
	'focus',
	'disabled',
	'muted',
	'selected',
	'hidden',
	'error',
	'success',
	'warning'
);

$theme-required-keys: (
	header: (
		bg: (),
		text: ()
	),
	main: (
		bg: (),
		text: ()
	),
	footer: (
		bg: (),
		text: ()
	)
);
```

and configure your theme in module `/themes/_dark.scss` or `/themes/_light.scss`:

```scss
@use 'sass:map';
@use '../tokens/colors' as *;
@use '../core/mixins' as *;
@use './theme-schema' as *;

/// Theme map for dark mode
///
/// Defines color values for different UI elements following the structure
/// specified in `$theme-required-keys`.
///
/// - Can include colors for headers, footers, buttons, text, etc.
/// - Used with `validate-theme()` to ensure all required keys are present.
/// - Allows generating CSS variables for theming (light, dark, or custom themes).
///
/// Notes:
/// - Theme maps can be extended or modified for different projects.
/// - Helps maintain consistent styling across all components.

$dark: (
	header: (
		bg: (
			_: map.get($colors, neutral) // default appearance
			hover: map.get($colors, primary) // hover state
			active: map.get($colors, secondary) // active state
		),
		text: (
			_: map.get($colors, primary)
		)
	),
	main: (
		bg: (
			_: map.get($colors, secondary),
			hover: map.get($colors, neutral)
		),
		text: (
			_: map.get($colors, primary)
		)
	),
	footer: (
		bg: (
			_: map.get($colors, neutral)
		),
		text: (
			_: map.get($colors, primary)
		)
	)
);

@include validate-theme($dark, $theme-required-keys, $theme-allowed-states);

[data-theme='dark'] {
	@include generate-theme($dark, 'clr');
}
```

> 💡 `_` is the default state. It corresponds to the element's normal appearance without any special states such as hover, active, or disabled.

> 💡 to generate themes, generate-theme mixin exists in `/core/mixins`

> 💡 to validate themes, validate-theme mixin exists in `/core/mixins` and it uses `/themes/_theme-schema.scss` to keep structure

also you can create or custom theme, for example `/themes/_neon.scss` and just import it to `/themes/_index.scss`.

</details>

<br>

## 🛠️ **Code quality & formatting**

All SCSS files in this system are linted and formatted locally before pushing to the repository:

<details>
<summary><strong>Prettier</strong></summary>
For consistent code formatting.

```json .prettierrc
{
	"trailingComma": "none",
	"arrowParens": "avoid",
	"jsxSingleQuote": true,
	"bracketSpacing": true,
	"singleQuote": true,
	"useTabs": true,
	"semi": false,
	"tabWidth": 2
}
```

</details>

<details>
<summary><strong>Stylelint</strong></summary>
For enforcing SCSS/CSS best practices.

```js .stylelintrc.cjs
module.exports = {
	extends: ['stylelint-config-standard-scss'],
	plugins: ['stylelint-scss'],
	rules: {
		// Overrides
		'at-rule-no-unknown': null,
		'custom-property-empty-line-before': null,
		'declaration-empty-line-before': null,

		// Colors & alpha
		'color-hex-length': 'long',
		'color-function-notation': 'modern',
		'alpha-value-notation': 'percentage',

		// Fonts & Strings
		'font-family-name-quotes': 'always-where-recommended',
		'length-zero-no-unit': true,

		// Declarations
		'declaration-block-no-duplicate-properties': true,
		'declaration-block-no-redundant-longhand-properties': true,
		'declaration-block-no-shorthand-property-overrides': true,

		// Selectors
		'no-duplicate-selectors': true,
		'no-descending-specificity': true,
		'selector-no-qualifying-type': true,
		'selector-max-id': 0,
		'selector-max-class': 4,
		'max-nesting-depth': 4,

		// Vendor Prefixes
		'property-no-vendor-prefix': true,
		'value-no-vendor-prefix': true,

		// SCSS
		'scss/at-rule-no-unknown': true,
		'scss/at-mixin-pattern': '^[-a-z]+$',
		'scss/at-function-pattern': '^[-a-z]+$',
		'scss/dollar-variable-pattern': '^[-a-z]+$',
		'scss/dollar-variable-empty-line-before': null,
		'scss/no-duplicate-dollar-variables': true,
		'scss/no-global-function-names': true,
		'scss/selector-no-redundant-nesting-selector': true
	}
}
```

</details>

<br>

## 📂 **Folder structure**

- **base/** — base styles and global rules (reset, fonts, basic elements)
- **core/** — mixins, functions and variable generation
- **themes/** — theme maps (theme-schema, light, dark, etc.)
- **tokens/** — core values: colors, spacing, radius, shadows, breakpoints, animations, typography

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
 │    ├── 📄 _mixins.scss
 │    ├── 📄 _variables.scss
 │    └── 📄 _index.scss
 │
 ├── 📁 themes
 │    ├── 📄 _dark.scss
 │    ├── 📄 _light.scss
 │    ├── 📄 _theme-schema.scss
 │    └── 📄 _index.scss
 │
 ├── 📁 tokens
 │    ├── 📄 _animations.scss
 │    ├── 📄 _breakpoints.scss
 │    ├── 📄 _typography.scss
 │    ├── 📄 _colors.scss
 │    ├── 📄 _radius.scss
 │    ├── 📄 _shadow.scss
 │    ├── 📄 _spacing.scss
 │    └── 📄 _index.scss
 │
 └── 📄 main.scss
</pre>
