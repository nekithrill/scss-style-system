> 📂 **Location:** `styles/core/functions/`
> 🎯 **Scope:** Value transformations
> 🏷️ **Type:** Core

# ⚙️ Functions

## px-to-rem

Convert pixel values to rem units.

**Location:** `styles/core/functions/_px-to-rem.scss`

### Signature

```scss
@function px-to-rem($value, $base: $base-font-size)
```

### Parameters

- `$value` — px value, list of px values, or zero
- `$base` — base font size in px (default: `$base-font-size` from typography tokens)

### Returns

Rem value, list of rem values, or the original value unchanged.

### Behavior

| Input | Output | Reason |
|-------|--------|--------|
| `24px` | `1.5rem` | Standard conversion |
| `0` | `0` | Zero has no unit |
| `16px 24px` | `1rem 1.5rem` | List support |
| `50%` | `50%` | Non-px values pass through |
| `9999px` | `9999px` | Values ≥ 5000px stay in px |

Values ≥ 5000px are left in px to preserve `pill: 9999px` border radius.

### Usage

```scss
@use '@/styles/core/functions/px-to-rem' as *;

.element {
	padding: px-to-rem(24px);        // → 1.5rem
	margin: px-to-rem(16px 24px);    // → 1rem 1.5rem
}
```

In practice, `px-to-rem` is called automatically by `generate-tokens` when `transform: 'rem'` is set — you rarely need to call it directly.