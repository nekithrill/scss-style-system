> **📁 Location:** Custom theme file
> **📦 Type:** Theme

# 🆕 Creating custom themes

Step-by-step guide to creating your own theme.

## 🧠 How it works

Creating a custom theme involves two steps:

1. **Create theme file:** Define CSS custom properties under a `[data-theme='name']` selector
2. **Import in main.scss:** Add the import so the file gets included in the build

**Key principle:** Themes map base color tokens (`--clr-primary-500`, `--clr-neutral-100`) to semantic theme variables (`--clr-text`, `--clr-header-bg`). This keeps components decoupled from specific color values.

## 🚀 Usage

**Step 1: Create theme file**

Create `styles/themes/_custom.scss`:

```scss
[data-theme='custom'] {
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

	--clr-header-bg: var(--clr-primary-600); // Custom: Brand color header
	--clr-header-text: var(--clr-neutral-100);

	--clr-main-bg: var(--clr-secondary-100);
	--clr-main-text: var(--clr-neutral-800);

	--clr-footer-bg: var(--clr-neutral-800); // Custom: Dark footer
	--clr-footer-text: var(--clr-neutral-300);
}
```

**Step 2: Import in main.scss**

```scss
@use 'themes/light';
@use 'themes/dark';
@use 'themes/custom'; // Add your theme
```

**Step 3: Activate theme**

```html
<html data-theme="custom">
  <!-- Your custom theme is now active -->
</html>
```

## ✔️ Best practices

- ✅ **Do:** Start with light or dark theme as template
- ✅ **Do:** Reference color tokens, not hardcoded values
- ✅ **Do:** Test all components in your theme
- ✅ **Do:** Check contrast ratios for accessibility (WCAG AA: 4.5:1)
- ✅ **Do:** Add hover/active states for interactive elements
- ❌ **Don't:** Use absolute color values (use tokens)
- ❌ **Don't:** Forget to test edge cases
- ❌ **Don't:** Create too many themes (maintain 2-4 max)

```scss
// ✅ Good: Token-based
[data-theme='custom'] {
	--clr-text: var(--clr-neutral-900);
}

// ❌ Bad: Hardcoded color
[data-theme='custom'] {
	--clr-text: #1a1a1a;
}
```
