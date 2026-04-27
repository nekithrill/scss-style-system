> 📁 **Location:** `styles/base/_globals.scss`
> 🎯 **Scope:** Global element defaults
> 🏷️ **Type:** Basic

# 🌐 Global styles

Base defaults for `html`, `body`, and headings. Sets typography tokens and text colors that themes can override.

## ⚙️ Configuration

```scss
// styles/base/_globals.scss

:root {
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);
	accent-color: var(--clr-text-accent);
	font-synthesis: none;
	text-rendering: optimizeLegibility;
	color-scheme: light dark;
}

html {
	height: 100%;
	font-size: var(--fs-default);
	line-height: var(--lh-normal, 1.5);
	scroll-behavior: smooth;
}

body {
	min-height: 100%;
	font-family: var(--ff-primary), var(--ff-system);
	font-weight: var(--fw-regular);
	color: var(--clr-text);
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}

h1, h2, h3, h4, h5, h6 {
	font-weight: var(--fw-bold);
	font-family: var(--ff-accent), var(--ff-primary), var(--ff-system);
}

h1 { font-size: var(--fs-h1); }
h2 { font-size: var(--fs-h2); }
h3 { font-size: var(--fs-h3); }
h4 { font-size: var(--fs-h4); }
h5 { font-size: var(--fs-h5); }
h6 { font-size: var(--fs-h6); }
```

`--clr-text` and `--clr-text-accent` are set here as defaults and overridden by themes when present.

## 🔧 Customization

**Add background color** (define in theme, reference here):

```scss
body {
	background-color: var(--clr-bg, white);
}
```

**Reduce motion:**

```scss
@media (prefers-reduced-motion: reduce) {
	html {
		scroll-behavior: auto;
	}
}
```

**Remove accent font from headings** if you only use one typeface:

```scss
h1, h2, h3, h4, h5, h6 {
	font-family: var(--ff-primary), var(--ff-system);
}
```