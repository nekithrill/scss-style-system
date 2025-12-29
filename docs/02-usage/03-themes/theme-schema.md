## 📐 Theme schema

The schema defines the **required structure** for all themes.

---

### Default schema

```scss
// themes/_schema.scss

/// Allowed leaf keys (state variants)
$theme-leaf-keys: (
	'_',        // Base value (required)
	'hover',    // Hover state
	'active',   // Active/pressed state
	'focus',    // Focused state
	'disabled', // Disabled state
	'muted',    // Muted variant
	'selected', // Selected state
	'error',    // Error state
	'success',  // Success state
	'warning',  // Warning state
	'info'      // Info state
);

/// Required keys (all themes must include these)
$theme-required-keys: (
	text: (
		_: (),      // Default text 
		accent: ()  // Accent text
	),
	selection: (
		bg: (),   // Text selection background
		text: ()  // Text selection color
	),
	scrollbar: (
		track: (),  // Scrollbar track
		thumb: ()   // Scrollbar thumb
	),
	header: (
		bg: (),   // Header background
		text: ()  // Header text
	),
	main: (
		bg: (),   // Main content background
		text: ()  // Main content text
	),
	footer: (
		bg: (),   // Footer background
		text: ()  // Footer text
	)
);
```

---

### Customizing Schema

#### Adding New Components

```scss
// themes/_schema.scss

$theme-required-keys: (
	// ... existing keys
	/// Add button component
	button: (
			primary: (),
			secondary: (),
			danger: ()
		),

	/// Add card component
	card: (
			bg: (),
			border: (),
			text: ()
		),

	/// Add input component
	input: (
			bg: (),
			border: (),
			text: (),
			placeholder: ()
		)
);
```

#### Adding Custom Leaf Keys

```scss
$theme-leaf-keys: (
	'_',
	'hover',
	'active',
	'focus',
	'disabled',
	'highlighted',  // ← New
	'dimmed',       // ← New
	'loading',      // ← New
	'pressed'       // ← New
);
```
