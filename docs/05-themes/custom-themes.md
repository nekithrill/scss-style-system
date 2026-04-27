> 📂 **Location:** `styles/themes/*`
> 🎯 **Scope:** Custom themes creation
> 🏷️ **Type:** Theme

# 🆕 Creating custom themes

Add an extra theme or replace the default ones entirely.

## 🧠 How it works

A theme is a plain SCSS file that maps token values to semantic variables under a `[data-theme='name']` selector. Any number of themes can coexist — only the active one applies.

## 👣 Steps

**1. Create theme file** — `styles/themes/_custom.scss`:

```scss
[data-theme='custom'] {
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

**2. Import in `main.scss`:**

```scss
@use './themes/light';
@use './themes/dark';
@use './themes/custom';
```

**3. Activate:**

```html
<html data-theme="custom">
```

Or via JavaScript:

```js
document.documentElement.setAttribute('data-theme', 'custom')
```

## 🔧 Customization

Prefer referencing token variables over hardcoded values — if token changes later, the theme will update automatically:
 
```scss
// Preferred — updates automatically when token changes
[data-theme='custom'] {
	--clr-bg: var(--clr-primary-100);
}
 
// Works, but won't reflect token changes
[data-theme='custom'] {
	--clr-bg: #ede9fe;
}
```
 
Use light or dark theme as a starting template — copy it and adjust individual variables as needed.