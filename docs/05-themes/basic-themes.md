> **📁 Location:** `styles/themes/*`
> **📦 Type:** Theme

# 🎨 Basic themes (Light & Dark)

Pre-configured light and dark themes with semantic color mappings.

## 🧠 How it works

The system provides two ready-to-use themes:

- **Light theme** (`_light.scss`): Defined in `:root`. Uses light backgrounds with dark text. Designed for daytime use and well-lit environments.
- **Dark theme** (`_dark.scss`): Defined in `[data-theme='dark']`. Uses dark backgrounds with light text. Designed for low-light environments.

Themes directly declare CSS custom properties — no generation mixins or schema validation required. This keeps the system simple and easy to debug.

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
// Switch themes via HTML attribute:

<html data-theme="dark">
  <!-- Dark theme active -->
</html>

<html>
  <!-- Light theme active (default via :root) -->
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
:root {
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);
	--clr-text-active: var(--clr-primary-600);
	--clr-text-hover: var(--clr-primary-400);

	--clr-bg: var(--clr-secondary-100);
	--clr-bg-hover: var(--clr-secondary-200);
	--clr-bg-active: var(--clr-secondary-300);

	--clr-selection-bg: var(--clr-primary-200);
	--clr-selection-text: var(--clr-primary-900);

	--clr-scrollbar-thumb: var(--clr-neutral-400);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track: var(--clr-neutral-100);
	--clr-scrollbar-track-hover: var(--clr-neutral-200);

	--clr-header-bg: var(--clr-secondary-100);
	--clr-header-text: var(--clr-neutral-900);

	--clr-main-bg: var(--clr-secondary-100);
	--clr-main-text: var(--clr-neutral-800);

	--clr-footer-bg: var(--clr-secondary-200);
	--clr-footer-text: var(--clr-neutral-700);
}
```

**Dark theme (_dark.scss):**

```scss
[data-theme='dark'] {
	--clr-text: var(--clr-neutral-100);
	--clr-text-accent: var(--clr-primary-400);
	--clr-text-active: var(--clr-primary-300);
	--clr-text-hover: var(--clr-primary-500);

	--clr-bg: var(--clr-neutral-900);
	--clr-bg-hover: var(--clr-neutral-800);
	--clr-bg-active: var(--clr-neutral-700);

	--clr-selection-bg: var(--clr-primary-700);
	--clr-selection-text: var(--clr-neutral-100);

	--clr-scrollbar-thumb: var(--clr-neutral-600);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track: var(--clr-neutral-900);
	--clr-scrollbar-track-hover: var(--clr-neutral-800);

	--clr-header-bg: var(--clr-neutral-900);
	--clr-header-text: var(--clr-neutral-100);

	--clr-main-bg: var(--clr-neutral-800);
	--clr-main-text: var(--clr-neutral-200);

	--clr-footer-bg: var(--clr-neutral-900);
	--clr-footer-text: var(--clr-neutral-400);
}
```

## ✔️ Best practices

- ✅ **Do:** Use neutral colors for text (high contrast)
- ✅ **Do:** Adjust primary/accent colors for dark mode (lighter shades)
- ✅ **Do:** Test contrast ratios (WCAG AA: 4.5:1 for text)
- ✅ **Do:** Add state variants (hover, active) where needed
- ❌ **Don't:** Use same colors in both themes (defeats the purpose)
- ❌ **Don't:** Forget to test all components in both themes
- ❌ **Don't:** Use low-contrast colors (accessibility issue)
