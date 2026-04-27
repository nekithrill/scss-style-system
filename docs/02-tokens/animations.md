> 📁 **Location:** `styles/tokens/_animations.scss`
> 🎯 **Scope:** Motion — duration, easing, delay
> 🏷️ **Type:** Token

# 🎞️ Animation tokens

Timing parameters for consistent motion. Three groups: `duration`, `easing`, `delay`.

## ⚡️ Usage

```scss
.button {
	transition:
		background-color var(--dur-fast) var(--tf-ease-out),
		transform var(--dur-fast) var(--tf-ease-out);
}

.modal {
	animation: slideIn var(--dur-normal) var(--tf-ease-out);
}

// Staggered list
.item:nth-child(2) { animation-delay: var(--delay-short); }
.item:nth-child(3) { animation-delay: var(--delay-medium); }
```

## ⚙️ Configuration

```scss
// Duration — prefix: --dur-
$duration: (
	faster: 100ms,
	fast:   200ms,
	normal: 300ms,
	slow:   500ms,
	slower: 700ms
) !default;

// Easing — prefix: --tf-
$easing: (
	linear:     linear,
	ease-in:    cubic-bezier(0.4, 0, 1, 1),
	ease-out:   cubic-bezier(0, 0, 0.2, 1),
	ease-in-out: cubic-bezier(0.4, 0, 0.2, 1),
	bounce:     cubic-bezier(0.68, -0.55, 0.265, 1.55)
) !default;

// Delay — prefix: --delay-
$delay: (
	short:  50ms,
	medium: 100ms,
	long:   200ms
) !default;
```

**Generated variables**

```css
:root {
	--dur-faster: 100ms;
	--dur-fast:   200ms;
	--dur-normal: 300ms;
	--dur-slow:   500ms;
	--dur-slower: 700ms;

	--tf-linear:      linear;
	--tf-ease-in:     cubic-bezier(0.4, 0, 1, 1);
	--tf-ease-out:    cubic-bezier(0, 0, 0.2, 1);
	--tf-ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
	--tf-bounce:      cubic-bezier(0.68, -0.55, 0.265, 1.55);

	--delay-short:  50ms;
	--delay-medium: 100ms;
	--delay-long:   200ms;
}
```

**Duration guide:**

| Token | Typical use |
|-------|-------------|
| `faster` | Immediate feedback — hover, focus |
| `fast` | Standard interactions — toggles, buttons |
| `normal` | Default — modals, dropdowns |
| `slow` | Complex transitions — page changes |
| `slower` | Elaborate effects — reveals, carousels |

**Easing guide:**

| Token | Typical use |
|-------|-------------|
| `ease-out` | Entrances |
| `ease-in` | Exits |
| `ease-in-out` | Continuous motion |
| `linear` | Loaders, infinite animations |
| `bounce` | Playful effects |

## 🔧 Customization

**Snappier feel:**

```scss
$duration: (
	faster: 50ms,
	fast:   150ms,
	normal: 200ms,
	slow:   350ms,
	slower: 500ms
) !default;
```

**Add custom easing:**

```scss
$easing: (
	// ...existing values
	spring: cubic-bezier(0.175, 0.885, 0.32, 1.275)
) !default;
```