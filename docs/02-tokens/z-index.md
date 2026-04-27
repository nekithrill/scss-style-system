> 📁 **Location:** `styles/tokens/_z-index.scss`
> 🎯 **Scope:** Stacking context and layer ordering
> 🏷️ **Type:** Token

# 🏔️ Z-index tokens

Semantic stacking hierarchy. Prevents z-index conflicts by naming common layers instead of using arbitrary numbers.

## ⚡️ Usage

```scss
.header {
	position: sticky;
	top: 0;
	z-index: var(--z-header);
}

.modal-overlay {
	position: fixed;
	inset: 0;
	z-index: var(--z-overlay);
}

.modal-content {
	position: fixed;
	z-index: var(--z-modal);
}

.tooltip {
	position: absolute;
	z-index: var(--z-tooltip);
}
```

## ⚙️ Configuration

```scss
$z-index: (
	min:          -1,
	base:          0,
	content:      50,
	header:       100,
	footer:       150,
	overlay:      200,
	sidebar:      250,
	dropdown:     300,
	sticky:       350,
	modal:        400,
	tooltip:      450,
	notification: 500,
	max:          9999
) !default;
```

**Generated variables**

Prefix: `--z-`

```css
:root {
	--z-min:          -1;
	--z-base:          0;
	--z-content:      50;
	--z-header:       100;
	--z-footer:       150;
	--z-sidebar:      200;
	--z-dropdown:     250;
	--z-sticky:       300;
	--z-overlay:      350;
	--z-modal:        400;
	--z-tooltip:      450;
	--z-notification: 500;
	--z-max:          9999;
}
```

> Z-index only works on positioned elements (`position: relative`, `absolute`, `fixed`, `sticky`).

## 🔧 Customization
 
**Change existing values** — adjust the scale to fit your project:
 
```scss
$z-index: (
	min:          -1,
	base:          0,
	content:      100,
	header:       200,
	footer:       200,
	overlay:      300,
	sidebar:      400,
	dropdown:     500,
	sticky:       600,
	modal:        700,
	tooltip:      800,
	notification: 900,
	max:          9999
) !default;
```
 
**Remove unused layers** — if your project has no modals or tooltips:
 
```scss
$z-index: (
	min:      -1,
	base:      0,
	content:  50,
	header:   100,
	dropdown: 200,
	max:      9999
) !default;
```
 
**Add custom layers:**
 
```scss
$z-index: (
	// ...existing values
	backdrop: 380,  // Between overlay and modal
	debug:    9998  // Below max
) !default;
```