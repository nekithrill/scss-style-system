> 📁 **Location:** `styles/tokens/_spacing.scss`
> 🎯 **Scope:** Layout spacing — padding, margin, gap
> 🏷️ **Type:** Token

# 📏 Spacing tokens

8px grid system. Change `$base-spacing` — all ten steps scale proportionally. Values are converted to rem.

## ⚡️ Usage

```scss
.card {
	padding: var(--sp-4);
	margin-bottom: var(--sp-6);
}

.button {
	padding: var(--sp-2) var(--sp-4);
}

.grid {
	display: grid;
	gap: var(--sp-3);
}
```

## ⚙️ Configuration

```scss
$base-spacing: 8px !default;

$spacing: (
	1: $base-spacing * 1,  // 8px
	2: $base-spacing * 2,  // 16px
	3: $base-spacing * 3,  // 24px
	4: $base-spacing * 4,  // 32px
	5: $base-spacing * 5,  // 40px
	6: $base-spacing * 6,  // 48px
	7: $base-spacing * 7,  // 56px
	8: $base-spacing * 8,  // 64px
	9: $base-spacing * 9,  // 72px
	10: $base-spacing * 10 // 80px
) !default;
```

**Generated variables**

Prefix: `--sp-`

```css
:root {
	--sp-1: 0.5rem; /* 8px  */
	--sp-2: 1rem;   /* 16px */
	--sp-3: 1.5rem; /* 24px */
	--sp-4: 2rem;   /* 32px */
	--sp-5: 2.5rem; /* 40px */
	--sp-6: 3rem;   /* 48px */
	--sp-7: 3.5rem; /* 56px */
	--sp-8: 4rem;   /* 64px */
	--sp-9: 4.5rem; /* 72px */
	--sp-10: 5rem;  /* 80px */
}
```

## 🔧 Customization

**Tighter layout:**

```scss
$base-spacing: 4px !default;
```

**Add extra-large steps:**

```scss
$spacing: (
	1: $base-spacing * 1,
	// ...
	10: $base-spacing * 10,
	12: $base-spacing * 12,  // 96px
	16: $base-spacing * 16   // 128px
) !default;
```
