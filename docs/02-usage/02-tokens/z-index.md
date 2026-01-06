## ⬆️⬇️ Z-index tokens

Define stacking order for layered UI elements. Values are aligned with the **theme schema** to ensure consistent layering across components like header, footer, and modals.
```scss
// tokens/_z-index.scss

// Z-index layering system
// Values correspond to theme components for semantic consistency
// Lower values = behind, higher values = in front
$z-index: (
	base: 0,           // Default layer
	content: 100,      // Content sections
	header: 200,       // Header component
	sidebar: 200,      // Sidebar navigation
	footer: 200,       // Footer component
	dropdown: 300,     // Dropdowns, menus
	sticky: 400,       // Sticky elements
	modal: 500,        // Modal dialogs
	tooltip: 600,      // Tooltips
	notification: 700  // Notifications
);
```

<br>

### Generated CSS variables
```css
:root {
	--z-base: 0;
	--z-content: 100;
	--z-header: 200;
	--z-sidebar: 200;
	--z-footer: 200;
	--z-dropdown: 300;
	--z-sticky: 400;
	--z-modal: 500;
	--z-tooltip: 600;
	--z-notification: 700;
}
```

<br>

### Usage examples
```scss
// Theme components (aligned with schema)
.header {
	position: sticky;
	top: 0;
	z-index: var(--z-header); // 200
	background: var(--theme-header-bg);
}

.footer {
	position: relative;
	z-index: var(--z-footer); // 200
	background: var(--theme-footer-bg);
}

// Overlay components
.dropdown {
	position: absolute;
	z-index: var(--z-dropdown); // 300
}

.modal {
	position: fixed;
	z-index: var(--z-modal); // 500
}

.tooltip {
	position: absolute;
	z-index: var(--z-tooltip); // 600
}

.notification {
	position: fixed;
	top: 1rem;
	right: 1rem;
	z-index: var(--z-notification); // 700 (always on top)
}
```

<br>

### Relationship with theme schema

Z-index tokens should align with your theme schema components:
```scss
// Theme schema defines these components:
$theme-required-keys: (
	header: (...),  // z-index: 200
	main: (...),    // z-index: 0 (base)
	footer: (...)   // z-index: 200
);

// Z-index tokens provide matching values:
$z-index: (
	base: 0,      // for main content
	header: 200,  // for header component
	footer: 200   // for footer component
);
```

<br>

### Customization examples

**Adjust layering hierarchy:**
```scss
$z-index: (
	base: 0,
	content: 100,
	header: 200,
	sidebar: 200,
	footer: 200,
	dropdown: 300,
	sticky: 400,       // New
	modal: 500,        // Moved up
	tooltip: 600,      // Moved up
	notification: 700  // New (highest)
);
```

**Add component-specific layers:**
```scss
$z-index: (
	// ... existing values
	'drawer': 450,    // Side drawer (between sticky and modal)
	'popover': 550,   // Popover (between modal and tooltip)
	'loading': 800    // Loading overlay (above everything)
);
```

**Semantic grouping (alternative approach):**
```scss
$z-index: (
	// Base layers (0-99)
	base: 0,
	content: 10,

	// Layout layers (100-199)
	header: 100,
	sidebar: 100,
	footer: 100,

	// Overlay layers (200-299)
	dropdown: 200,
	tooltip: 250,

	// Modal layers (300-399)
	modal: 300,
	drawer: 350,

	// Alert layers (400+)
	notification: 400,
	emergency: 500
);
```

<br>

### Best practices

**Alignment with theme:**

- Match z-index token names to theme schema components
- Use same values for components at the same visual level
- Keep header/footer at same z-index unless there's specific need

**Hierarchy guidelines:**

- **0-99:** Base content and static elements
- **100-299:** Navigation and layout (header, footer, sidebar)
- **300-499:** Overlays (dropdowns, tooltips)
- **500-699:** Modals and dialogs
- **700+:** Critical notifications and alerts

**Spacing between values:**

- Use increments of 100 for major layers
- Leaves room for additions (e.g., 250 between 200 and 300)
- Avoid arbitrary numbers like 9999

**Common mistakes to avoid:**

- ❌ Using z-index: 9999 (makes debugging hard)
- ❌ Inconsistent increments (1, 5, 100, 200, 9999)
- ❌ Not documenting why certain values are higher
- ✅ Use semantic names and consistent scale