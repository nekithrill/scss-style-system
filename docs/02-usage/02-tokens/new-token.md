## ✨ Creating custom tokens

Follow these steps to add new design tokens to your project.

---

### Create token file

Define your token values in a new SCSS file inside the `tokens/` directory:

```scss
// tokens/_borders.scss

/// Border width tokens
/// Consistent border thicknesses across the project
$borders: (
	thin: 1px,    // Subtle dividers
	normal: 2px,  // Standard borders
	thick: 4px,   // Emphasized borders
	bold: 6px     // Heavy separators
);
```

---

### Import and configure

Add your new token to the generation configuration (see [Variables generation](../01-basics/variables-generation.md)):

```scss
// tokens/_index.scss

@use '../tokens/borders' as *; // ← Import new token file

$base-tokens: (
	// ... existing tokens (colors, spacing, typography, etc.)
	borders: (
			map: $borders,
			prefix: 'border',
			transform: 'rem' // Optional: convert px to rem
		)
);

:root {
	@include generate-tokens($base-tokens);
}
```

---

### Generated output

CSS variables are automatically created with your specified prefix:

```css
:root {
	/* Generated from $borders */
	--border-thin: 0.0625rem;  /* 1px */
	--border-normal: 0.125rem; /* 2px */
	--border-thick: 0.25rem;   /* 4px */
	--border-bold: 0.375rem;   /* 6px */
}
```

---

### Usage in component

Use the generated CSS variables throughout your project:

```scss
.card {
	border: var(--border-normal) solid var(--clr-neutral-300);

	&:hover {
		border-width: var(--border-thick);
	}
}

.divider {
	border-bottom: var(--border-thin) solid var(--clr-neutral-200);
}

.emphasis-box {
	border: var(--border-bold) solid var(--clr-primary-500);
}
```

---

### Additional examples

**Nested token structure (like colors):**

```scss
// tokens/_elevations.scss

$elevations: (
	'low': (
		shadow: 0 1px 3px rgba(0, 0, 0, 0.12),
		blur: 4px
	),
	'medium': (
		shadow: 0 4px 6px rgba(0, 0, 0, 0.1),
		blur: 8px
	),
	'high': (
		shadow: 0 10px 20px rgba(0, 0, 0, 0.15),
		blur: 16px
	)
);

// Configuration
$base-tokens: (
	elevations: (
		map: $elevations,
		prefix: 'elevation'
	)
);

// Generated:
// --elevation-low-shadow: 0 1px 3px rgba(0, 0, 0, 0.12);
// --elevation-low-blur: 4px;
// --elevation-medium-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
// --elevation-medium-blur: 8px;
```

**Flat token structure without transformation:**

```scss
// tokens/_icons.scss

$icon-sizes: (
	sm: 16px,
	md: 24px,
	lg: 32px,
	xl: 48px
);

// Configuration (no transform)
$base-tokens: (
	icon-sizes: (
		map: $icon-sizes,
		prefix: 'icon' // No transform - keep px units
	)
);

// Generated:
// --icon-sm: 16px;
// --icon-md: 24px;
// --icon-lg: 32px;
// --icon-xl: 48px;
```

---

### Best practices

**Token organization:**

- One token file per category (borders, elevations, icons, etc.)
- Use descriptive file names prefixed with underscore (`_borders.scss`)
- Keep token values simple and semantic

**Naming conventions:**

- Use lowercase keys for consistency
- Choose prefixes that won't conflict (`border`, `icon`, `elev`)
- Use scale names like `sm/md/lg` or numbered scales `100-900`

**When to use transform: 'rem':**

- ✅ Use for spacing, sizing, borders (anything layout-related)
- ❌ Don't use for colors, shadows, z-index, timing values
- ❌ Don't use if you need exact pixel values (icons, images)
