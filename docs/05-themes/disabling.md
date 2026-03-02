> **📁 Location:** `styles/themes/*`
> **📦 Type:** Theme

# 🚫 Disabling themes

How to disable or limit theming in your project.

## Disable dark theme

Simply don't import `_dark.scss` in `main.scss`:

```scss
@use 'themes/light'; // Only light theme
// @use 'themes/dark'; // Commented out
```

## Use only dark theme as default

Replace `:root` in `_light.scss` with `[data-theme='light']` and move the dark theme to `:root`:

```scss
// _dark.scss — set as default
:root {
	--clr-text: var(--clr-neutral-100);
	// ...
}

// _light.scss — optional, on demand
[data-theme='light'] {
	--clr-text: var(--clr-neutral-900);
	// ...
}
```
