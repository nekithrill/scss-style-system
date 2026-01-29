> **📁 Location:** Custom theme file
> **📦 Type:** Theme

# 🆕 Creating custom themes

Step-by-step guide to creating your own theme that follows the system's structure.

## 🧠 How it works

Creating a custom theme involves four steps:

1. **Create theme map:** Define color mappings following the required schema structure
2. **Validate theme:** Use `validate-theme` mixin to catch errors at compile time
3. **Generate CSS variables:** Use `generate-theme` mixin to output theme variables
4. **Apply theme:** Use `data-theme` attribute to activate your theme

**Key principle:** Themes map base color tokens (`--clr-primary-500`, `--clr-neutral-100`) to semantic theme variables (`--clr-text`, `--clr-header-bg`). This keeps components decoupled from specific color values.

## 🚀 Usage

**Step 1: Create theme file**

Create `styles/themes/_custom.scss`:

```scss
// Custom theme - Your brand colors
$custom: (
	text: (
		_: var(--clr-neutral-900),
		accent: var(--clr-primary-500)
	),
	selection: (
		bg: (_: var(--clr-primary-200)),
		text: (_: var(--clr-primary-900))
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-400),
			hover: var(--clr-neutral-500)
		),
		track: (_: var(--clr-neutral-100))
	),
	header: (
		bg: (_: var(--clr-primary-600)),      // Custom: Brand color header
		text: (_: var(--clr-neutral-100))
	),
	main: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (_: var(--clr-neutral-800))
	),
	footer: (
		bg: (_: var(--clr-neutral-800)),      // Custom: Dark footer
		text: (_: var(--clr-neutral-300))
	)
);
```

**Step 2: Apply theme**

Update `styles/themes/_apply.scss`:

```scss
@use 'light' as *;
@use 'dark' as *;
@use 'custom' as *;  // Import your theme
@use 'schema' as *;
@use '../core/mixins/generate-theme' as *;
@use '../core/mixins/validate-theme' as *;

// Validate all themes
@include validate-theme($light, $theme-schema);
@include validate-theme($dark, $theme-schema);
@include validate-theme($custom, $theme-schema); // Add validation of custom theme 

// Generate themes
:root {
	@include generate-theme($light);
}

[data-theme='dark'] {
	@include generate-theme($dark);
}

[data-theme='custom'] {  // Add your theme
	@include generate-theme($custom);
}
```

**Step 3: Activate theme**

```html
<html data-theme="custom">
  <!-- Your custom theme is now active -->
</html>
```

## ⚙️ Advanced examples

**High-contrast theme:**

```scss
$high-contrast: (
	text: (
		_: var(--clr-neutral-900),  // Pure black
		accent: var(--clr-primary-700)  // Darker accent
	),
	selection: (
		bg: (_: var(--clr-neutral-900)),
		text: (_: var(--clr-neutral-100))
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-900),
			hover: var(--clr-neutral-800)
		),
		track: (_: var(--clr-neutral-100))
	),
	header: (
		bg: (_: var(--clr-neutral-900)),
		text: (_: var(--clr-neutral-100))
	),
	main: (
		bg: (
			_: var(--clr-neutral-100),  // Pure white
			hover: var(--clr-neutral-200)
		),
		text: (_: var(--clr-neutral-900))
	),
	footer: (
		bg: (_: var(--clr-neutral-900)),
		text: (_: var(--clr-neutral-100))
	)
);
```

**Brand-focused theme:**

```scss
$brand: (
	text: (
		_: var(--clr-neutral-800),
		accent: var(--clr-primary-600)
	),
	selection: (
		bg: (_: var(--clr-primary-300)),
		text: (_: var(--clr-primary-900))
	),
	scrollbar: (
		thumb: (
			_: var(--clr-primary-400),  // Brand scrollbar
			hover: var(--clr-primary-500)
		),
		track: (_: var(--clr-primary-100))
	),
	header: (
		bg: (
			_: var(--clr-primary-500),  // Full brand header
			hover: var(--clr-primary-600)
		),
		text: (_: var(--clr-neutral-100))
	),
	main: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (_: var(--clr-neutral-800))
	),
	footer: (
		bg: (_: var(--clr-primary-700)),
		text: (_: var(--clr-neutral-100))
	)
);
```

**Adding custom sections:**

```scss
// First, update schema
$theme-schema: (
	// ... existing sections
	sidebar: (
		bg: (),
		text: ()
	),
	card: (
		bg: (),
		text: (),
		border: ()
	)
);

// Then use in theme
$extended: (
	// ... all required sections
	sidebar: (
		bg: (
			_: var(--clr-neutral-100),
			hover: var(--clr-neutral-200),
			active: var(--clr-primary-100)
		),
		text: (_: var(--clr-neutral-800))
	),
	card: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (_: var(--clr-neutral-800)),
		border: (
			_: var(--clr-neutral-300),
			hover: var(--clr-primary-400)
		)
	)
);
```

## 🔧 Customization workflow

**1. Start with existing theme:**

```scss
// Copy light.scss as starting point
$my-theme: (
	// Paste light theme structure
	// Modify colors to match your design
);
```

**2. Adjust colors systematically:**

```scss
// Header section
header: (
	bg: (_: var(--clr-YOUR-COLOR)),  // Replace
	text: (_: var(--clr-YOUR-COLOR))
),

// Main section
main: (
	bg: (
		_: var(--clr-YOUR-COLOR),
		hover: var(--clr-YOUR-COLOR-VARIANT)
	),
	text: (_: var(--clr-YOUR-COLOR))
),
```

**3. Test contrast:**

```scss
// Use browser DevTools or online tools to check:
// - Text on background: 4.5:1 minimum
// - UI components: 3:1 minimum
// Adjust colors if needed
```

**4. Validate and generate:**

```scss
@include validate-theme($my-theme, $theme-schema);

[data-theme='my-theme'] {
	@include generate-theme($my-theme);
}
```

## 🎨 Theme creation checklist

Before deploying your custom theme:

- [ ] All required sections present
- [ ] Validation passes without errors
- [ ] Contrast ratios meet WCAG AA (4.5:1 for text)
- [ ] Hover states visibly different from default
- [ ] Tested in all major components
- [ ] Tested with focus indicators
- [ ] Tested with form elements
- [ ] Scrollbar colors work
- [ ] Selection colors have good contrast
- [ ] Documentation updated

## 💡 Quick start template

```scss
// styles/themes/_my-theme.scss

$my-theme: (
	text: (
		_: var(--clr-neutral-900),
		accent: var(--clr-primary-500)
	),
	selection: (
		bg: (_: var(--clr-primary-200)),
		text: (_: var(--clr-primary-900))
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-400),
			hover: var(--clr-neutral-500)
		),
		track: (_: var(--clr-neutral-100))
	),
	header: (
		bg: (_: /* YOUR COLOR */),
		text: (_: /* YOUR COLOR */)
	),
	main: (
		bg: (
			_: /* YOUR COLOR */,
			hover: /* YOUR COLOR */
		),
		text: (_: /* YOUR COLOR */)
	),
	footer: (
		bg: (_: /* YOUR COLOR */),
		text: (_: /* YOUR COLOR */)
	)
);
```

## ✔️ Best practices

- ✅ **Do:** Start with light or dark theme as template
- ✅ **Do:** Validate theme before deployment
- ✅ **Do:** Test all components in your theme
- ✅ **Do:** Check contrast ratios for accessibility
- ✅ **Do:** Document your theme's purpose/use case
- ✅ **Do:** Add hover/active states for interactive elements
- ❌ **Don't:** Skip validation (catches errors early)
- ❌ **Don't:** Use absolute color values (use tokens)
- ❌ **Don't:** Forget to test edge cases
- ❌ **Don't:** Create too many themes (maintain 2-4 max)

```scss
// ✅ Good: Token-based, validated
@use 'schema' as *;
@use '../core/mixins/validate-theme' as *;

$my-theme: (
	text: (_: var(--clr-neutral-900)),
	// ... rest of theme
);

@include validate-theme($my-theme, $theme-schema);

// ❌ Bad: Absolute colors, no validation
$my-theme: (
	text: (_: #1a1a1a),  // Hardcoded
	// ... rest
);
// No validation - errors only at runtime
```

## ❌ Common mistakes

**Missing required sections:**

```scss
// ❌ Bad: Missing footer
$incomplete: (
	text: (...),
	selection: (...),
	scrollbar: (...),
	header: (...),
	main: (...)
	// Missing: footer
);
// Error: ⚠️ Theme map is missing required key `footer`!

// ✅ Good: All sections present
$complete: (
	text: (...),
	selection: (...),
	scrollbar: (...),
	header: (...),
	main: (...),
	footer: (...)  // ✓
);
```

**Using wrong structure:**

```scss
// ❌ Bad: Flat structure
$wrong: (
	text: var(--clr-neutral-900),  // Should be nested
	'header-bg': var(--clr-primary-500)
);

// ✅ Good: Nested structure
$correct: (
	text: (
		_: var(--clr-neutral-900)
	),
	header: (
		bg: (_: var(--clr-primary-500))
	)
);
```

**Forgetting base `_` value:**

```scss
// ❌ Bad: No base value
$missing-base: (
	header: (
		bg: (
			hover: var(--clr-primary-600)  // Where's the base?
		)
	)
);

// ✅ Good: Always include base
$with-base: (
	header: (
		bg: (
			_: var(--clr-primary-500),     // Base value
			hover: var(--clr-primary-600)
		)
	)
);
```