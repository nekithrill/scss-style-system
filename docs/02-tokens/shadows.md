> 📁 **Location:** `styles/tokens/_shadows.scss`
> 🎯 **Scope:** Elevation and depth
> 🏷️ **Type:** Token

# 🌫️ Shadow tokens

Progressive elevation scale from subtle depth to dramatic overlay. Change `$base-shadow` to adjust color and intensity globally.

## ⚡️ Usage

```scss
.card {
	box-shadow: var(--shadow-md);

	&:hover {
		box-shadow: var(--shadow-lg);
	}
}

.button:active {
	box-shadow: var(--shadow-inset);
}

.modal {
	box-shadow: var(--shadow-xl);
}
```

## ⚙️ Configuration

```scss
$base-shadow: rgb(0 0 0 / 10%) !default;

$shadows: (
	xs:    0 1px 3px $base-shadow,
	sm:    0 2px 6px $base-shadow,
	md:    0 4px 12px $base-shadow,
	lg:    0 8px 24px $base-shadow,
	xl:    0 16px 48px $base-shadow,
	inset: inset 0 2px 4px $base-shadow
) !default;
```

**Generated variables**

Prefix: `--shadow-`

```css
:root {
	--shadow-xs:    0 1px 3px rgb(0 0 0 / 10%);
	--shadow-sm:    0 2px 6px rgb(0 0 0 / 10%);
	--shadow-md:    0 4px 12px rgb(0 0 0 / 10%);
	--shadow-lg:    0 8px 24px rgb(0 0 0 / 10%);
	--shadow-xl:    0 16px 48px rgb(0 0 0 / 10%);
	--shadow-inset: inset 0 2px 4px rgb(0 0 0 / 10%);
}
```

**Elevation guide:**

| Token | Typical use |
|-------|-------------|
| `xs` | Subtle separation — table rows, list items |
| `sm` | Interactive elements — buttons, inputs |
| `md` | Elevated surfaces — cards, panels |
| `lg` | Floating elements — dropdowns, tooltips |
| `xl` | Major overlays — modals, dialogs |
| `inset` | Pressed states |

## 🔧 Customization

**Adjust intensity:**

```scss
$base-shadow: rgb(0 0 0 / 15%) !default; // Darker
$base-shadow: rgb(0 0 0 / 5%) !default;  // Lighter
```

**Colored shadows:**

```scss
$base-shadow: rgb(99 102 241 / 20%) !default; // Brand-tinted
```

**Stronger scale:**

```scss
$shadows: (
	xs:    0 1px 3px $base-shadow,
	sm:    0 2px 6px $base-shadow,
	md:    0 6px 16px $base-shadow,
	lg:    0 12px 32px $base-shadow,
	xl:    0 24px 64px $base-shadow,
	inset: inset 0 2px 4px $base-shadow
) !default;
```