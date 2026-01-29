> **📁 Location:** `styles/themes/_light.scss`, `styles/themes/_dark.scss`, `styles/themes/_apply.scss`
> **📦 Type:** Theme

# 🎨 Basic themes (Light & Dark)

Pre-configured light and dark themes with semantic color mappings.

## 🧠 How it works

The system provides two ready-to-use themes that demonstrate best practices:

- **Light theme** (`$light`): Uses light backgrounds (secondary-100/200) with dark text (neutral-800/900). Designed for daytime use and well-lit environments.

- **Dark theme** (`$dark`): Uses dark backgrounds (neutral-800/900) with light text (neutral-100/200). Designed for low-light environments and reduced eye strain.

**Theme application** (`_apply.scss`): Orchestrates the theme system by:

1. Importing both themes and the schema
2. Validating themes against schema (catches errors at compile time)
3. Generating CSS variables in `:root` (light theme as default)
4. Generating CSS variables in `[data-theme='dark']` selector

**Key concept:** Themes reference base color tokens (like `--clr-neutral-900`) and map them to semantic theme variables (like `--clr-text`). This indirection allows components to use semantic names while themes control actual colors.

**Generated output:**

```css
:root {
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);
	--clr-header-bg: var(--clr-secondary-100);
	/* ... etc */
}

[data-theme='dark'] {
	--clr-text: var(--clr-neutral-100);
	--clr-text-accent: var(--clr-primary-400);
	--clr-header-bg: var(--clr-neutral-900);
	/* ... etc */
}
```

## 🚀 Usage

```scss
// Themes are applied automatically
// Switch themes via HTML attribute:

<html data-theme="dark">
  <!-- Dark theme active -->
</html>

<html data-theme="light">
  <!-- Light theme active (or omit attribute) -->
</html>

// Components use semantic theme variables:
.header {
	background: var(--clr-header-bg);
	color: var(--clr-header-text);
}

.button {
	color: var(--clr-text);
	
	&:hover {
		background: var(--clr-main-bg-hover);
	}
}
```

## ⚙️ Configuration

**Light theme (_light.scss):**
```scss
$light: (
	text: (
		_: var(--clr-neutral-900),      // Dark text
		accent: var(--clr-primary-500)  // Brand color
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
		bg: (_: var(--clr-secondary-100)),
		text: (_: var(--clr-neutral-900))
	),
	main: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (_: var(--clr-neutral-800))
	),
	footer: (
		bg: (_: var(--clr-secondary-200)),
		text: (_: var(--clr-neutral-700))
	)
);
```

**Dark theme (_dark.scss):**

```scss
$dark: (
	text: (
		_: var(--clr-neutral-100),      // Light text
		accent: var(--clr-primary-400)  // Adjusted brand color
	),
	selection: (
		bg: (_: var(--clr-primary-700)),
		text: (_: var(--clr-neutral-100))
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-600),
			hover: var(--clr-neutral-500)
		),
		track: (_: var(--clr-neutral-900))
	),
	header: (
		bg: (_: var(--clr-neutral-900)),
		text: (_: var(--clr-neutral-100))
	),
	main: (
		bg: (
			_: var(--clr-neutral-800),
			hover: var(--clr-neutral-700)
		),
		text: (_: var(--clr-neutral-200))
	),
	footer: (
		bg: (_: var(--clr-neutral-900)),
		text: (_: var(--clr-neutral-400))
	)
);
```

**Theme application (_apply.scss):**

```scss
@use 'light' as *;
@use 'dark' as *;
@use 'schema' as *;
@use '../core/mixins/generate-theme' as *;
@use '../core/mixins/validate-theme' as *;

// Validate themes at compile time
@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);
@include validate-theme($dark, $theme-required-keys, $theme-leaf-keys);

// Generate default (light) theme
:root {
	@include generate-theme($light);
}

// Generate dark theme
[data-theme='dark'] {
	@include generate-theme($dark);
}
```

## 🔧 Customization

**Adjust light theme colors:**

```scss
$light: (
	text: (
		_: var(--clr-neutral-800),     // Slightly lighter
		accent: var(--clr-primary-600) // Darker accent
	),
	header: (
		bg: (_: var(--clr-secondary-200)),  // Darker header
		text: (_: var(--clr-neutral-900))
	),
	// ... rest of theme
);
```

**Add new sections:**

```scss
$light: (
	// ... existing sections
	card: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (_: var(--clr-neutral-800)),
		border: (_: var(--clr-neutral-300))
	)
);

// Don't forget to update schema!
```

**Change default theme:**

```scss
// Make dark theme default
:root {
	@include generate-theme($dark);  // Dark by default
}

[data-theme='light'] {
	@include generate-theme($light);  // Light on demand
}
```

## 🎨 Color mapping guide

**Light theme philosophy:**

- Backgrounds: Secondary palette (100-300) - very light
- Text: Neutral palette (700-900) - very dark
- Accents: Primary palette (500-600) - vibrant

**Dark theme philosophy:**

- Backgrounds: Neutral palette (800-900) - very dark
- Text: Neutral palette (100-300) - very light
- Accents: Primary palette (400-500) - slightly muted

**Contrast checklist:**
```
✓ Text on background: 4.5:1 minimum (WCAG AA)
✓ Large text on background: 3:1 minimum
✓ UI components: 3:1 minimum
✓ Hover states: Visibly different from default
```

## ✔️ Best practices

- ✅ **Do:** Use neutral colors for text (high contrast)
- ✅ **Do:** Adjust primary/accent colors for dark mode (lighter shades)
- ✅ **Do:** Test contrast ratios (WCAG AA: 4.5:1 for text)
- ✅ **Do:** Validate themes before deployment
- ✅ **Do:** Add state variants (hover, active) where needed
- ❌ **Don't:** Use same colors in both themes (defeats the purpose)
- ❌ **Don't:** Forget to test all components in both themes
- ❌ **Don't:** Use low-contrast colors (accessibility issue)

```scss
// ✅ Good: High contrast in both themes
$light: (
	text: (_: var(--clr-neutral-900)),  // Dark on light
	main: (bg: (_: var(--clr-secondary-100)))
);

$dark: (
	text: (_: var(--clr-neutral-100)),  // Light on dark
	main: (bg: (_: var(--clr-neutral-900)))
);

// ❌ Bad: Low contrast
$light: (
	text: (_: var(--clr-neutral-400)),  // Gray on light gray
	main: (bg: (_: var(--clr-secondary-200)))
);
```

## ❌ Common mistakes

**Forgetting validation:**

```scss
// ❌ Bad: No validation, errors only show at runtime
:root {
	@include generate-theme($light);
}

// ✅ Good: Validate first
@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);
:root {
	@include generate-theme($light);
}
```

**Using absolute colors:**

```scss
// ❌ Bad: Hardcoded colors
$light: (
	text: (_: #1a1a1a),  // Can't adjust with tokens
	main: (bg: (_: #ffffff))
);

// ✅ Good: Reference color tokens
$light: (
	text: (_: var(--clr-neutral-900)),
	main: (bg: (_: var(--clr-secondary-100)))
);
```

**Missing state variants:**

```scss
// ❌ Bad: No hover state
$light: (
	main: (
		bg: (_: var(--clr-secondary-100)),
		text: (_: var(--clr-neutral-800))
	)
);

// ✅ Good: Include interactive states
$light: (
	main: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)  // Better UX
		),
		text: (_: var(--clr-neutral-800))
	)
);
```