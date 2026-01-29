> **📁 Location:** `styles/themes/_schema.scss`
> **📦 Type:** Theme

# 📋 Theme schema

Defines the required structure and allowed variant keys for theme validation.

## 🧠 How it works

The theme schema serves as a contract that all themes must follow, ensuring consistency across light, dark, and custom themes:

**Theme leaf keys** (`$theme-leaf-keys`): Defines allowed state variant suffixes like `hover`, `active`, `focus`, `disabled`. These can be used at any leaf level in the theme structure. The special `_` key represents the base/default value.

**Required keys** (`$theme-required-keys`): Defines the minimum structure every theme must provide. This includes semantic sections like `text`, `selection`, `scrollbar`, `header`, `main`, and `footer`, each with their required properties.

**Validation process:** When a theme is validated (using `validate-theme` mixin), it checks:
1. All required keys are present (throws error if missing)
2. No unexpected keys are used (warns if found)
3. Leaf keys match the allowed list

**Why this matters:** Schema validation catches typos, missing sections, and structural errors at compile time, preventing runtime theme issues.

## 🚀 Usage

```scss
// Schema is used automatically during theme validation
// You don't import it directly - it's used by _apply.scss

// When creating custom themes, follow this structure:
$custom: (
	text: (
		_: ...,
		accent: ...
	),
	selection: (
		bg: (...),
		text: (...)
	),
	// ... all other required sections
);
```

## ⚙️ Configuration

```scss
// themes/_schema.scss

// Allowed leaf keys (state variants)
$theme-leaf-keys: (
	'_',          // Base value (required)
	'hover',      // Hover state
	'active',     // Active/pressed state
	'focus',      // Focus state
	'disabled',   // Disabled state
	'muted',      // Muted/subtle variant
	'selected',   // Selected state
	'hidden',     // Hidden state
	'error',      // Error state
	'success',    // Success state
	'warning',    // Warning state
	'info'        // Info state
);

// Required theme structure
$theme-required-keys: (
	text: (
		_: (),
		accent: ()
	),
	selection: (
		bg: (),
		text: ()
	),
	scrollbar: (
		track: (),
		thumb: ()
	),
	header: (
		bg: (),
		text: ()
	),
	main: (
		bg: (),
		text: ()
	),
	footer: (
		bg: (),
		text: ()
	)
);
```

**What each section means:**

- `text`: Base text colors (default + accent variant)
- `selection`: Text selection highlight colors
- `scrollbar`: Custom scrollbar styling
- `header`, `main`, `footer`: Layout section colors

## 🔧 Customization

**Add new required section:**

```scss
$theme-required-keys: (
	// ... existing sections
	sidebar: (
		bg: (),
		text: ()
	),
	card: (
		bg: (),
		text: (),
		border: ()
	)
);
```

**Add new state variants:**

```scss
$theme-leaf-keys: (
	'_',
	'hover',
	'active',
	// ... existing states
	'loading',    // New: loading state
	'invalid',    // New: invalid state
	'checked'     // New: checkbox checked state
);
```

**Remove optional sections:**

```scss
// If you don't need footer theming
$theme-required-keys: (
	text: (...),
	selection: (...),
	scrollbar: (...),
	header: (...),
	main: (...)
	// Removed: footer
);
```

## 🔍 Validation examples

**Valid theme (passes validation):**

```scss
$custom: (
	text: (_: ..., accent: ...),             // ✓ Required
	selection: (bg: (...), text: (...)),     // ✓ Required
	scrollbar: (track: (...), thumb: (...)), // ✓ Required
	header: (bg: (...), text: (...)),        // ✓ Required
	main: (bg: (...), text: (...)),          // ✓ Required
	footer: (bg: (...), text: (...))         // ✓ Required
);
// ✅ Validation passes
```

**Invalid theme (validation error):**

```scss
$custom: (
	text: (_: ..., accent: ...),
	selection: (bg: (...), text: (...)),
	scrollbar: (track: (...), thumb: (...)),
	header: (bg: (...), text: (...)),
	main: (bg: (...), text: (...))
	// Missing: footer
);
// ❌ Error: Theme map is missing required key `footer`!
```

**Theme with warning:**

```scss
$custom: (
	text: (_: ..., accent: ...),
	// ... all required sections ...
	footer: (
		bg: (
			_: ...,
			hovered: ...  // Wrong key name
		),
		text: (...)
	)
);
// ⚠️ Warning: Theme map contains unexpected key `footer.bg.hovered`
//            that is not in the schema or leaf keys whitelist!
```

## ✔️ Best practices

- ✅ **Do:** Keep required keys minimal (only truly required sections)
- ✅ **Do:** Add custom sections for your specific needs
- ✅ **Do:** Use semantic names (`header`, `card`, not `div1`, `section2`)
- ✅ **Do:** Document custom sections for other developers
- ❌ **Don't:** Remove core sections (text, selection) - they're used by base styles
- ❌ **Don't:** Add too many required sections (makes themes harder to create)
- ❌ **Don't:** Use technical names in schema (keep it semantic)

```scss
// ✅ Good: Semantic structure
$theme-required-keys: (
	button: (
		primary: (...),
		secondary: (...)
	)
);

// ❌ Bad: Technical names
$theme-required-keys: (
	component1: (...),
	element-a: (...)
);
```

## ❌ Common mistakes

**Forgetting to update schema when adding theme sections:**

```scss
// ❌ Bad: Theme has sidebar, but schema doesn't require it
$light: (
	// ... required sections
	sidebar: (...)  // Works but not validated!
);

// ✅ Good: Add to schema first
$theme-required-keys: (
	// ... existing
	sidebar: (
		bg: (),
		text: ()
	)
);
```

**Using wrong leaf key names:**

```scss
// ❌ Bad: 'hovered' not in allowed list
$light: (
	header: (
		bg: (
			_: ...,
			hovered: ...  // Should be 'hover'
		)
	)
);

// ✅ Good: Use correct leaf key
$light: (
	header: (
		bg: (
			_: ...,
			hover: ...  // Correct
		)
	)
);
```

**Making everything required:**

```scss
// ❌ Bad: Too strict, hard to create themes
$theme-required-keys: (
	header: (
		bg: (_: (), hover: (), active: ()),
		text: (_: (), hover: (), active: ()),
		border: (_: (), hover: (), active: ())
	)
);

// ✅ Good: Only require base values
$theme-required-keys: (
	header: (
		bg: (),   // Only base required
		text: ()  // States are optional
	)
);
```