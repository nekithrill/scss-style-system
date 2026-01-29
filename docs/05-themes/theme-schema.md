> **📁 Location:** `styles/themes/_schema.scss`
> **📦 Type:** Theme

# 📋 Theme schema

Defines the required structure for theme validation. Only enforces structural requirements - does NOT restrict state names or variant names.

## 🧠 How it works

The theme schema serves as a structural contract that all themes must follow:

- ✅ Ensures all themes have required sections
- ✅ Catches missing keys at compile time
- ✅ Maintains consistency across themes
- ❌ Does NOT restrict state names (use any names you want)
- ❌ Does NOT restrict variant names (use any names you want)

**Schema structure** (`$theme-schema`): Defines minimum structure using empty parentheses `()` to indicate "any value or nested structure allowed here".

**Validation:** Only checks that required keys are present. State names (hover, active, etc.) and variant names (primary, danger, etc.) are NOT validated.

**Flexibility:** This approach gives you:
- Freedom to use custom state names (`spinning`, `pulsing`, `emphasized`)
- Freedom to use custom variant names (`luxury`, `minimal`, `brand`)
- Only structural requirements enforced
- No need to update schema when adding new states/variants

**Why this matters:** Schema validation catches missing sections and structural errors at compile time, while giving you complete flexibility in naming.

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

$theme-schema: (
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

**What empty `()` means:** "This key must exist, but can contain any structure"

**Examples:**

```scss
// Schema says:
button: (
	bg: (),
	text: ()
)

// Theme can have ANY states:
button: (
	bg: (
		_: ...,
		hover: ...,
		active: ...,
		custom_state: ...    // ✅ OK - any state name allowed
	),
	text: (_: ...),
	
	// And ANY variants:
	variants: (
		primary: (...),
		custom_variant: (...)  // ✅ OK - any variant name allowed
	)
)
```

**What each section means:**

- `text`: Base text colors (default + accent variant)
- `selection`: Text selection highlight colors
- `scrollbar`: Custom scrollbar styling
- `header`, `main`, `footer`: Layout section colors

## 🔧 Customization

**Add new required section:**

```scss
$theme-schema: (
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

**Add nested requirements:**

```scss
$theme-schema: (
	card: (
		bg: (),
		text: (),
		header: (
			bg: (),
			text: ()
		),
		footer: (
			bg: ()
		)
	)
);
```

**Remove sections:**

```scss
$theme-schema: (
	text: (...),
	button: (...),
	card: (...)
	// Removed: sidebar, footer, etc. (if you don't need them)
);
```

## 🔍 Validation examples

**Valid theme (passes validation):**

```scss
$custom: (
	text: (_: ..., accent: ...),
	selection: (bg: (...), text: (...)),
	scrollbar: (track: (...), thumb: (...)),
	header: (bg: (...), text: (...)),
	main: (bg: (...), text: (...)),
	footer: (bg: (...), text: (...))
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
// ❌ Error: Missing required key: footer
```

**Theme with custom states:**

```scss
$custom: (
	// ... all required sections ...
	button: (
		bg: (
			_: ...,
			hovr: ...,           // ✅ Custom state name - OK!
			pressed: ...,        // ✅ Custom state name - OK!
			spinning: ...        // ✅ Custom state name - OK!
		),
		text: (_: ...)
	)
);
// ✅ Passes - all custom state names accepted
```

**Theme with custom variants:**

```scss
$custom: (
	// ... all required sections ...
	button: (
		bg: (_: ...),
		text: (_: ...),
		variants: (
			mega: (              // ✅ Custom variant
				bg: (_: ...),
				text: (_: ...)
			),
			luxury: (            // ✅ Custom variant
				bg: (_: ...),
				text: (_: ...)
			)
		)
	)
);
// ✅ Passes - all custom variant names accepted
```

## 🎯 Complete example

```scss
// Schema - defines WHAT must exist
$theme-schema: (
	button: (
		bg: (),
		text: ()
	),
	card: ()
);

// Theme - defines HOW it looks
$custom: (
	button: (
		bg: (
			_: gray,
			hover: lightgray,
			pressed: darkgray,     // Custom state ✅
			spinning: blue         // Custom state ✅
		),
		text: (_: black),
		variants: (
			primary: (...),
			luxury: (...),         // Custom variant ✅
			mega: (...)            // Custom variant ✅
		)
	),
	card: (
		bg: (_: white),
		awesome_state: (...)       // Custom state ✅
	)
);

@include validate-theme($custom, $theme-schema);
// ✅ Passes - all required keys present
// ✅ All custom state/variant names accepted
```

## ✔️ Best practices

- ✅ **Do:** Keep schema minimal (only truly required sections)
- ✅ **Do:** Use semantic names (`button`, `card`, not `component1`)
- ✅ **Do:** Use empty `()` for flexible structures
- ✅ **Do:** Document what each section is for
- ✅ **Do:** Use any state/variant names that fit your design system
- ❌ **Don't:** Remove core UI sections if used in your app
- ❌ **Don't:** Make schema too strict (hurts flexibility)
- ❌ **Don't:** Try to validate state/variant names in schema

```scss
// ✅ Good: Minimal, flexible schema
$theme-schema: (
	button: (
		bg: (),      // Any structure allowed inside
		text: ()
	),
	card: ()         // Completely flexible
);

// ❌ Bad: Too strict, too detailed
$theme-schema: (
	button: (
		bg: (
			_: (),
			hover: (),      // Don't require specific states
			active: ()
		)
	)
);
```

## ❌ Common mistakes

**Forgetting to update schema:**

```scss
// ❌ Bad: Theme has new section, schema doesn't
$light: (
	button: (...),
	sidebar: (...)  // Not in schema!
);

// ✅ Good: Update schema first
$theme-schema: (
	button: (...),
	sidebar: (...)  // Now required
);
```

**Over-specifying structure:**

```scss
// ❌ Bad: Too many requirements
$theme-schema: (
	button: (
		bg: (
			_: (),
			hover: (),
			active: (),
			disabled: ()
		)
	)
);

// ✅ Good: Minimal requirements
$theme-schema: (
	button: (
		bg: (),    // Let themes decide what states to include
		text: ()
	)
);
```

**Expecting validation of states:**

```scss
// ❌ Wrong expectation:
// "Schema will catch typos in state names"

$theme: (
	button: (
		bg: (
			_: ...,
			hovr: ...  // Typo - but NOT caught by validation!
		)
	)
);

// ✅ Correct understanding:
// Only structure is validated, not state/variant names
// You have complete freedom in naming
```