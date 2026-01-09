## 🌓 Basic themes handling

The system includes `light` and `dark` themes by default.

> 💡 To customize theme elements you need to edit [theme schema](theme-schema.md)

<br>

### How themes work

Themes override base CSS variables to change the appearance of your site:
```scss
// Base tokens (always available)
--clr-neutral-900: oklch(20% 0.01 220deg);

// Theme variables (change based on [data-theme])
--clr-text: var(--clr-neutral-900);  // Light theme
--clr-text: var(--clr-neutral-100);  // Dark theme
```

**Theme structure:**
- Base tokens (`--clr-primary-500`) → never change
- Theme tokens (`--clr-text`, `--clr-main-bg`) → change with theme
- Your components use theme tokens for automatic color switching

<br>

### Switching themes

Add `data-theme` attribute to `<html>` or `<body>`:
```html
<!-- Light theme (default) -->
<html>

<!-- Dark theme -->
<html data-theme="dark">
```

**JavaScript example:**
```js
// Toggle theme
const html = document.documentElement;
const currentTheme = html.getAttribute('data-theme');
const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
html.setAttribute('data-theme', newTheme);

// Save preference
localStorage.setItem('theme', newTheme);

// Load saved theme on page load
const savedTheme = localStorage.getItem('theme');
if (savedTheme) {
  html.setAttribute('data-theme', savedTheme);
}
```

**Respect system preference:**
```js
// Check user's OS preference
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

// Apply if no saved preference
if (!localStorage.getItem('theme')) {
  html.setAttribute('data-theme', prefersDark ? 'dark' : 'light');
}

// Listen for OS preference changes
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
  if (!localStorage.getItem('theme')) {
    html.setAttribute('data-theme', e.matches ? 'dark' : 'light');
  }
});
```

<br>

### Generated CSS variables

Both themes generate the same variable names with different values:
```css
/* Light theme (default) */
:root {
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);
	--clr-main-bg: var(--clr-secondary-100);
	--clr-header-bg: var(--clr-secondary-100);
	/* ... */
}

/* Dark theme */
[data-theme='dark'] {
	--clr-text: var(--clr-neutral-100);
	--clr-text-accent: var(--clr-primary-400);
	--clr-main-bg: var(--clr-neutral-800);
	--clr-header-bg: var(--clr-neutral-900);
	/* ... */
}
```

<br>

### Using theme variables in components

Always use theme variables (not base tokens) for colors that should change with theme:
```scss
// ✅ Good - uses theme variables
.card {
	background: var(--clr-main-bg);
	color: var(--clr-text);
	
	&:hover {
		background: var(--clr-main-bg-hover);
	}
}

// ❌ Bad - uses base tokens (won't change with theme)
.card {
	background: var(--clr-secondary-100);
	color: var(--clr-neutral-900);
}

// ✅ Good - accent colors can use base tokens (they don't change)
.button-primary {
	background: var(--clr-primary-500);
	color: white;
}
```

<br>

### 🌞 Light Theme (_light.scss)

Default theme using lighter backgrounds and darker text.
```scss
// themes/_light.scss

$light: (
	text: (
		_: var(--clr-neutral-900),
		accent: var(--clr-primary-500)
	),
	selection: (
		bg: (
			_: var(--clr-primary-200)
		),
		text: (
			_: var(--clr-primary-900)
		)
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-400),
			hover: var(--clr-neutral-500)
		),
		track: (
			_: var(--clr-neutral-100)
		)
	),
	header: (
		bg: (
			_: var(--clr-secondary-100)
		),
		text: (
			_: var(--clr-neutral-900)
		)
	),
	main: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (
			_: var(--clr-neutral-800)
		)
	),
	footer: (
		bg: (
			_: var(--clr-secondary-200)
		),
		text: (
			_: var(--clr-neutral-700)
		)
	)
);
```

<br>

### 🌑 Dark Theme (_dark.scss)

Dark mode using darker backgrounds and lighter text.
```scss
// themes/_dark.scss

$dark: (
	text: (
		_: var(--clr-neutral-100),
		accent: var(--clr-primary-400)
	),
	selection: (
		bg: (
			_: var(--clr-primary-700)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-600),
			hover: var(--clr-neutral-500)
		),
		track: (
			_: var(--clr-neutral-900)
		)
	),
	header: (
		bg: (
			_: var(--clr-neutral-900)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	),
	main: (
		bg: (
			_: var(--clr-neutral-800),
			hover: var(--clr-neutral-700)
		),
		text: (
			_: var(--clr-neutral-200)
		)
	),
	footer: (
		bg: (
			_: var(--clr-neutral-900)
		),
		text: (
			_: var(--clr-neutral-400)
		)
	)
);
```

<br>

### Customizing themes

To modify existing themes, edit the color references:
```scss
// themes/_light.scss

$light: (
	// Use different neutral shades
	main: (
		bg: (
			_: var(--clr-neutral-50),  // Lighter background
		),
		text: (
			_: var(--clr-neutral-950)  // Darker text
		)
	),
	
	// Use primary color for header
	header: (
		bg: (
			_: var(--clr-primary-500)
		),
		text: (
			_: white
		)
	)
);
```

For more details on creating custom themes, see [Custom theme creation](custom-theme.md).

<br>

### Disabling themes

If you don't need theming:

1. Remove theme imports from `styles/main.scss`:
```scss
   // @use './themes/apply' as *;  ← Comment out or delete
```

2. Use base tokens directly in your components:
```scss
   .card {
   	background: var(--clr-secondary-100);
   	color: var(--clr-neutral-900);
   }
```

This reduces CSS output size if theming isn't needed.