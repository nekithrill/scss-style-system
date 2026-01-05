## 🛠️ **Code quality & formatting**

All SCSS files in this system are linted and formatted before pushing. Some tests were also carried out.

### Prettier

This system follows the Prettier configuration below to maintain consistent formatting.

> 💡 **Note:** Configuration files (`.prettierrc.cjs`) are available on the `sandbox` branch. These settings are provided for reference if you want to apply the same formatting rules.

> 💡 **Dependencies required:** To use Prettier in your project, install:
> - `prettier` 

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

This system follows the Stylelint configuration below to enforce consistent SCSS/CSS best practices.

> 💡 **Note:** Configuration files (`.stylelintrc.cjs`) are available on the `sandbox` branch. These settings are provided for reference to show how the system was formatted.

> 💡 **Dependencies required:** To use Stylelint in your project, install:
> - `stylelint`
> - `stylelint-scss`
> - `stylelint-config-standard-scss`
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