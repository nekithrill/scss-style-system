## 🛠️ **Code quality & formatting**

All SCSS files in this system are linted and formatted locally before pushing. Also some tests were carried out.

---

### Prettier

This system follows the following Prettier configuration to maintain consistent formatting.

> 💡 Project is missing a `.prettierrc.cjs` file - these settings are provided in case you want to use the settings for the same formatting.

```js
module.exports = {
	trailingComma: 'none',
	arrowParens: 'avoid',
	jsxSingleQuote: true,
	bracketSpacing: true,
	singleQuote: true,
	useTabs: true,
	semi: false,
	tabWidth: 2
}
```

---

### Stylelint

This system follows the following Stylelint configuration to enforce consistent SCSS/CSS best practices.

> 💡 Project does not include a `.stylelintrc.cjs` file – these settings are provided for reference to show how the system was formatted.

> 💡 To use stylelint in your project, you need to install following dependencies:
> `stylelint`
> `stylelint-scss`.
> `stylelint-config-standard-scss`

```js
module.exports = {
	extends: ['stylelint-config-standard-scss'],
	plugins: ['stylelint-scss'],
	rules: {
		// Overrides
		'at-rule-no-unknown': null,

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

---

### Testing

...

<!-- This system was tested on different types of projects and no problems were found. -->
