> 📁 **Location:** `styles/themes/*`
> 🎯 **Scope:** Managing existing themes
> 🏷️ **Type:** Theme

# 🔄 Theme management

Switching between themes at runtime and controlling which themes are available.

## 🔘 Switching themes

Themes are activated by setting `data-theme` on the `<html>` element. The light theme (`:root`) is active by default — no attribute needed.

```html
<html>              <!-- light theme -->
<html data-theme="dark">   <!-- dark theme -->
```

**Basic toggle:**

```js
const html = document.documentElement;

function toggleTheme() {
	const isDark = html.getAttribute('data-theme') === 'dark';
	html.setAttribute('data-theme', isDark ? 'light' : 'dark');
	localStorage.setItem('theme', isDark ? 'light' : 'dark');
}

// Restore on load
const saved = localStorage.getItem('theme') || 'light';
html.setAttribute('data-theme', saved);
```

**Prevent flash of wrong theme** — run before page renders:

```html
<head>
	<script>
		(function() {
			const theme = localStorage.getItem('theme') || 'light';
			document.documentElement.setAttribute('data-theme', theme);
		})();
	</script>
</head>
```

**Respect system preference:**

```js
function getInitialTheme() {
	const stored = localStorage.getItem('theme');
	if (stored) return stored;

	return window.matchMedia('(prefers-color-scheme: dark)').matches
		? 'dark'
		: 'light';
}

document.documentElement.setAttribute('data-theme', getInitialTheme());
```

## 🔌 Disabling themes

**Remove dark theme** — simply don't import it:

```scss
// main.scss
@use './themes/light' as *;
// @use './themes/dark' as *; ← comment out or delete
```

**Use dark as default:**

```scss
// themes/_dark.scss — move to :root
:root {
	--clr-text: var(--clr-neutral-100);
	// ...
}

// themes/_light.scss — optional, on demand
[data-theme='light'] {
	--clr-text: var(--clr-neutral-900);
	// ...
}
```