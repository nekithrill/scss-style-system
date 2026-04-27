> 📁 **Location:** `styles/tokens/_borders.scss`
> 🎯 **Scope:** Border radius and width
> 🏷️ **Type:** Token

# 🔲 Border tokens

Radius scale for consistent rounding and width scale for borders and outlines.

> `pill` (9999px) — pill-shaped buttons and tags
> `full` (50%) — circular avatars and icons (square elements only)

## ⚡️ Usage

```scss
.button {
	border-radius: var(--br-md);
	border: var(--bw-normal) solid var(--clr-primary-500);
}

.badge {
	border-radius: var(--br-pill);
}

.avatar {
	width: 40px;
	height: 40px;
	border-radius: var(--br-full);
}

.modal {
	border-radius: var(--br-xl);
}
```

## ⚙️ Configuration

```scss
// Border radius — prefix: --br-
$border-radius: (
	xs:   2px,
	sm:   4px,
	md:   6px,
	lg:   10px,
	xl:   14px,
	pill: 9999px,
	full: 50%
) !default;

// Border width — prefix: --bw-
$border-width: (
	thin:   1px,
	normal: 2px,
	thick:  4px
) !default;
```

**Generated variables**

```css
:root {
	--br-xs:   0.125rem;    /* 2px  */
	--br-sm:   0.25rem;     /* 4px  */
	--br-md:   0.375rem;    /* 6px  */
	--br-lg:   0.625rem;    /* 10px */
	--br-xl:   0.875rem;    /* 14px */
	--br-pill: 9999px;
	--br-full: 50%;

	--bw-thin:   1px;
	--bw-normal: 2px;
	--bw-thick:  4px;
}
```

## 🔧 Customization

**Rounder UI:**

```scss
$border-radius: (
	xs:   2px,
	sm:   6px,
	md:   10px,
	lg:   16px,  // Increased
	xl:   24px,  // Increased 
	pill: 9999px,
	full: 50%
) !default;
```

**Add extra sizes:**

```scss
$border-radius: (
	xs:   2px,
	sm:   4px,
	md:   6px,
	lg:   10px,
	xl:   14px,
	'2xl': 20px,  // New token
	pill: 9999px,
	full: 50%
) !default;
```