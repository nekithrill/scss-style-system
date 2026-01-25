> **📁 Location:** `styles/core/functions/*.scss`
> **🧭 Scope:** Low-level utilities and value transformations
> **📦 Type:** Core

## ⚙️ Functions

Utility functions for value transformations and calculations.

<br>

### px-to-rem

**Purpose:** Converts pixel values to rem units based on a configurable base font size.

**Location:** `styles/core/functions/_px-to-rem.scss`

#### ✍️ Signature

```scss
@function px-to-rem($value, $base: 16)
```

#### 🧩 Parameters

- `$value` (Number | List) - Value in px, list of px values, or unitless zero
- `$base` (Number, optional) - Base font-size in pixels. Default: `16`

#### 🔁 Returns

(Number | List) - Corresponding rem value(s), or original value if not in pixels

#### 🧠 How it works

The function processes values through these steps:

1. **Type checking:** Detects if input is a number or list
2. **Zero handling:** Returns `0` immediately for zero values (no unit)
3. **Unit validation:** Checks if value has `px` unit
4. **Large value protection:** Values ≥5000px stay in pixels (e.g., `9999px` for pill radius)
5. **Conversion:** Divides px value by base, multiplies by 1rem
6. **List processing:** Recursively converts each item in lists

**Formula:** `(value / (base * 1px)) * 1rem`

**Example:** `24px / (16 * 1px) * 1rem = 1.5rem`

**Edge cases:**
- Large values (≥5000px) remain in pixels for special cases like `border-radius: 9999px`
- Zero values lose their unit: `0px` → `0`
- Non-pixel values pass through unchanged: `50%`, `300ms`, `auto`
- Lists are processed recursively, maintaining order
- Colors and other non-numeric values in lists are preserved


#### 🚀 Usage

```scss
@use '@/styles/core/functions/px-to-rem' as *;

// Single value
.element {
	padding: px-to-rem(24px);  // → 1.5rem
	margin: px-to-rem(16px);   // → 1rem
}

// List of values
.box {
	padding: px-to-rem(16px 24px);  // → 1rem 1.5rem
	margin: px-to-rem(8px 16px 24px 32px);  // → 0.5rem 1rem 1.5rem 2rem
}

// Zero values
.flush {
	margin: px-to-rem(0);  // → 0 (no unit)
}
```
#### ✔️ Best practices

- ✅ **Do:** Use for spacing, sizing, and layout values that should scale with user preferences
- ✅ **Do:** Set `$base` to match your root font-size if different from 16px
- ✅ **Do:** Use in token generation with `transform: 'rem'` option
- ❌ **Don't:** Convert colors, weights, or unitless values
- ❌ **Don't:** Convert values that should stay in pixels (borders, shadows)
- ❌ **Don't:** Forget that large values (≥5000px) won't be converted

**Example patterns:**
```scss
// ✅ Good: Convert layout spacing
.container {
	padding: px-to-rem(24px);
	gap: px-to-rem(16px);
}

// ✅ Good: Used in token system
spacing: (
	map: $spacing,
	prefix: 'sp',
	transform: 'rem'  // Uses px-to-rem internally
),

// ❌ Bad: Converting colors
.button {
	background: px-to-rem(#6366f1);  // Makes no sense
}

// ❌ Bad: Converting borders (should stay in px)
.card {
	border: px-to-rem(1px) solid;  // 0.0625rem might render inconsistently
}
```