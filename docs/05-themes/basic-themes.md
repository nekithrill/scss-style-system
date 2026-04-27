> 📂 **Location:** `styles/themes/*`
> 🎯 **Scope:** Basic themes configuration
> 🏷️ **Type:** Theme

# 🎨 Basic themes

Two ready-to-use themes — light and dark. Both ship as empty templates with commented-out semantic variables. Fill them in to activate theming.

## 🧠 How it works

Light theme is defined in `:root` and active by default. Dark theme is activated via `[data-theme='dark']` on the `<html>` element.

Themes map raw token values to semantic variables that components use:

```scss
// Instead of hardcoding in components:
.card { background: var(--clr-secondary-100); } // breaks in dark mode

// Components reference semantic variables:
.card { background: var(--clr-bg); } // adapts automatically
```

## ⚡️ Usage

```scss
body {
	background: var(--clr-bg);
	color: var(--clr-text);
}

.button {
	color: var(--clr-text-accent);
}
```

Switch themes via JavaScript:

```js
document.documentElement.setAttribute('data-theme', 'dark')
document.documentElement.removeAttribute('data-theme') // back to light
```

See [Theme management](themes-management.md) for complete switching logic.

## ⚙️ Configuration

**Light theme (`_light.scss`):**

```scss
:root {
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);

	--clr-bg: var(--clr-secondary-100);

	--clr-focus: var(--clr-primary-500);

	--clr-selection-bg: var(--clr-primary-300);
	--clr-selection-text: var(--clr-neutral-900);

	--clr-scrollbar-thumb: var(--clr-neutral-400);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track: var(--clr-neutral-100);
}
```

**Dark theme (`_dark.scss`):**

```scss
[data-theme='dark'] {
	--clr-text: var(--clr-neutral-100);
	--clr-text-accent: var(--clr-primary-300);

	--clr-bg: var(--clr-secondary-900);

	--clr-focus: var(--clr-primary-300);

	--clr-selection-bg: var(--clr-primary-700);
	--clr-selection-text: var(--clr-neutral-100);

	--clr-scrollbar-thumb: var(--clr-neutral-600);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track: var(--clr-neutral-900);
}
```