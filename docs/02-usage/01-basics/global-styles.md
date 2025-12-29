## 🌐 Global styles configuration

This section configures basic styles for the entire application: fonts, colors, scroll behavior, and other fundamental settings that are applied to all elements by default.

---

### Basic configuration

```scss
// base/_globals.scss

:root {
	/// System font stack (fallback)
	font-family:
		system-ui,
		-apple-system,
		'Segoe UI',
		Roboto,
		sans-serif;

	/// Font features (ligatures and kerning)
	font-feature-settings:
		'liga' 1,
		'kern' 1;

	/// Body defaults (overridden by themes if present)
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);

	/// Accent color for native form controls (checkboxes, radio, progress)
	accent-color: var(--body-accent);
}

html {
	/// Smooth scrolling for anchor links
	scroll-behavior: smooth;

	/// Base font size for rem calculations (default: 16px)
	/// All rem values are calculated relative to this
	font-size: var(--fs-default);
}

body {
	/// Typography from tokens
	font-family: var(--ff-primary);
	font-weight: var(--fw-regular);

	/// Color and background
	/// Alias for general text color that can be overridden by theme
	color: var(--clr-text);
}

input,
button,
textarea,
select {
	background: none;
	border: none;
	outline: none;
}

h1,
h2,
h3,
h4,
h5,
h6 {
	font-weight: var(--fw-bold);
	font-family: var(--ff-accent, var(--ff-primary));
}

h1 {
	font-size: var(--fs-h1);
}

h2 {
	font-size: var(--fs-h2);
}

h3 {
	font-size: var(--fs-h3);
}

h4 {
	font-size: var(--fs-h4);
}

h5 {
	font-size: var(--fs-h5);
}

h6 {
	font-size: var(--fs-h6);
}

p {
	font-size: var(--fs-text);
	font-weight: var(--fw-regular);
	margin-bottom: 1rem;
}
```

> 💡 **Note:** The `--clr-body-*` aliases provide defaults that work without themes. When themes are enabled, they automatically override these values for light/dark mode support.

---

### Customization example

#### Customize headings

```scss
h1,
h2,
h3 {
	text-transform: uppercase;
	letter-spacing: 0.05em;
	font-family: var(--ff-accent); // Use accent font
}
```

#### Customize links

```scss
a {
	color: var(--clr-primary-500);
	text-decoration-thickness: 2px;
	text-underline-offset: 0.2em;
	transition: color var(--duration-fast);

	&:hover {
		color: var(--clr-primary-700);
	}
}
```

#### Smooth scroll with offset (for fixed headers)

```scss
html {
	scroll-behavior: smooth;
	scroll-padding-top: 80px; // Offset for fixed header height
}
```

#### Custom cursor

```scss
:root {
	cursor: url('/cursors/custom.cur'), auto;
}
```

#### Custom focus styles

```scss
:focus-visible {
	outline: 2px solid var(--clr-primary-500);
	outline-offset: 2px;
	border-radius: var(--rd-xs);
}
```

---

### How themes override globals

When themes are enabled, they automatically override the `--body-*` aliases:

```scss
// Without themes: uses globals defaults
:root {
	--clr-body-bg: var(--clr-neutral-100);   // Light gray
	--clr-body-text: var(--clr-neutral-900); // Dark text
}

// With themes: light theme (same values but from theme)
:root {
	--clr-body-bg: var(--clr-neutral-100);   // Overridden by theme
	--clr-body-text: var(--clr-neutral-900); // Overridden by theme
}

// With themes: dark theme (different values)
[data-theme='dark'] {
	--clr-body-bg: var(--clr-neutral-900);   // Dark background
	--clr-body-text: var(--clr-neutral-100); // Light text
}
```

This design allows the system to work both with and without themes, maintaining modularity.
