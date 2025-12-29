## 📐 Theme schema

The schema defines the **required structure** and **allowed variations** for all themes in the system.

---

## Understanding Leaf Keys

**Leaf keys** are the final level in the theme hierarchy — they represent the actual color values and their variants (states).

### Structure Hierarchy
```
Component → Property → Leaf Key → Value
   ↓           ↓          ↓         ↓
 header   →    bg    →    _     →  var(--clr-neutral-900)
                     →  hover   →  var(--clr-neutral-800)
```

**Example:**
```scss
$theme: (
	header: (              // Component
		bg: (              // Property
			_: #fff,       // Leaf key: base value
			hover: #eee    // Leaf key: hover state
		)
	)
);
```

### Allowed Leaf Keys

The `$theme-leaf-keys` list defines which keys are valid at the deepest level. This prevents typos and ensures consistency.

**Valid:**
```scss
button: (
	bg: (
		_: #fff,      // ✅ '_' is in leaf keys
		hover: #eee   // ✅ 'hover' is in leaf keys
	)
)
```

**Invalid:**
```scss
button: (
	bg: (
		_: #fff,
		hovered: #eee  // ❌ 'hovered' is NOT in leaf keys (typo!)
	)
)
```

The validation system will catch this error during theme generation.

---

## Default schema
```scss
// themes/_schema.scss

/// Allowed leaf keys (state variants)
/// These are the only keys allowed at the deepest nesting level
$theme-leaf-keys: (
	'_',        // Base value (common but not required)
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
/// Structure: component → property → () (leaf keys go here)
$theme-required-keys: (
	text: (
		_: (),      // Default text color
		accent: ()  // Accent text color
	),
	selection: (
		bg: (),     // Text selection background
		text: ()    // Text selection text color
	),
	scrollbar: (
		track: (),  // Scrollbar track background
		thumb: ()   // Scrollbar thumb color
	),
	header: (
		bg: (),     // Header background
		text: ()    // Header text
	),
	main: (
		bg: (),     // Main content background
		text: ()    // Main content text
	),
	footer: (
		bg: (),     // Footer background
		text: ()    // Footer text
	)
);
```

---

## Customizing Schema

### Adding New Components

Add components that your project needs:
```scss
// themes/_schema.scss

$theme-required-keys: (
	// ... existing keys (text, selection, scrollbar, header, main, footer)
	
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

Then use in your themes:
```scss
// themes/_light.scss
$light: (
	// ... existing components
	button: (
		primary: (
			_: var(--clr-primary-500),
			hover: var(--clr-primary-600)
		),
		secondary: (
			_: var(--clr-neutral-300),
			hover: var(--clr-neutral-400)
		)
	)
);
```

---

### Adding Custom Leaf Keys

Add project-specific state variants:
```scss
$theme-leaf-keys: (
	'_',
	'hover',
	'active',
	'focus',
	'disabled',
	'highlighted',  // ← New: for highlighted items
	'dimmed',       // ← New: for dimmed/inactive items
	'loading',      // ← New: for loading states
	'pressed'       // ← New: for pressed/clicked state
);
```

**Usage example:**
```scss
$light: (
	button: (
		primary: (
			_: var(--clr-primary-500),
			hover: var(--clr-primary-600),
			pressed: var(--clr-primary-700),    // ← Custom leaf key
			loading: var(--clr-primary-400)     // ← Custom leaf key
		)
	)
);
```

---

## How Validation Works

The validation system performs two checks:

### Required Keys Check

Ensures all keys from `$theme-required-keys` exist in your theme.
```scss
// ❌ Error: Missing required key
$light: (
	text: (...),
	header: (...)
	// footer: (...) ← MISSING 'footer'!
);
```

**Error:** `⚠️ Theme map is missing required key 'footer'!`

---

### Leaf Keys Check

Warns if theme contains keys not in schema or `$theme-leaf-keys`.
```scss
// ⚠️ Warning: Unexpected key
$light: (
	header: (
		bg: (
			_: var(--clr-neutral-100),
			hovered: var(--clr-neutral-200)  // ← TYPO: should be 'hover'
		)
	)
);
```

**Warning:** `⚠️ Theme map contains unexpected key 'header.bg.hovered'...`

This catches typos in leaf keys like `hovered` instead of `hover`.

---

### What's NOT Validated

**Base value (`_`) presence:**  
Not enforced. Include `_` when you need a default value, omit when only states/variants are needed:
```scss
// ✅ With base (most common)
bg: (
	_: var(--clr-neutral-100),
	hover: var(--clr-neutral-200)
)

// ✅ Without base (only states)
border: (
	error: var(--clr-danger-border),
	success: var(--clr-success-border)
	// No '_' - default border not theme-controlled
)

// ✅ Only base (no variants)
text: (
	_: var(--clr-neutral-500)
	// No hover/active - just a color modifier
)
```

**When to include `_`:**

- Properties that need a default value (most cases)
- Interactive elements that start with a base state

**When `_` is optional:**

- Properties that only define states (hover, error, etc.)
- Modifiers applied conditionally
- Values that inherit or default from elsewhere

**Value types:**  
The validator doesn't check if values are valid CSS (e.g., `var(--clr-invalid)`).

---

## Best Practices

**Component naming:**

- Use semantic names: `button`, `card`, `input` (not `btn`, `box`, `field`)
- Group related components: `nav` for navigation, `form` for forms

**Property naming:**

- Use consistent names: `bg`, `text`, `border` (across all components)
- Be specific: `placeholder` not `hint`, `icon` not `symbol`

**Leaf key usage:**

- Include `_` (base value) when element needs a default state
- Use `hover`, `active`, `focus` for interactive states
- Use `error`, `success`, `warning` for semantic variants
- Add custom leaf keys only when needed across multiple components

**Keep it simple:**

- Don't add components you don't use
- Start minimal, expand as needed
- Remove unused keys from schema for clarity

---

## Example: Complete Custom Schema
```scss
// Minimal e-commerce theme schema
$theme-required-keys: (
	// Base
	body: (
		bg: (),
		text: ()
	),
	
	// Navigation
	nav: (
		bg: (),
		text: (),
		link: ()
	),
	
	// Products
	product: (
		card: (
			bg: (),
			border: ()
		),
		price: (),
		badge: ()
	),
	
	// Actions
	button: (
		primary: (),
		secondary: (),
		disabled: ()
	),
	
	// Forms
	input: (
		bg: (),
		border: (),
		text: ()
	)
);

$theme-leaf-keys: (
	'_',
	'hover',
	'focus',
	'disabled',
	'error'      // Only needed states
);
```