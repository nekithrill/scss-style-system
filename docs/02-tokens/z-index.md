> **📁 Location:** `styles/tokens/_z-index.scss`
> **📦 Type:** Token

## 🏔️ Z-index tokens

Define stacking order values for consistent layering and depth control across your interface.

<br>

### 🧠 How it works

Z-index tokens establish a **stacking hierarchy** that prevents z-index conflicts and creates predictable layering. Instead of using arbitrary values like `999` or `9999`, the system provides semantic names for common stacking contexts.

**The scale (`--z-*`)** uses a 100-based increment system:
- `base` **(0)**: Default layer (most content)
- `content` **(100)**: Elevated content (active cards)
- `header/sidebar/footer` **(200)**: Fixed UI chrome
- `dropdown` **(300)**: Contextual overlays
- `sticky` **(400)**: Sticky positioned elements
- `modal` **(500)**: Modal dialogs
- `tooltip` **(600)**: Tooltips and popovers
- `notification` **(700)**: Toast notifications

**Why 100 increments?** Large gaps between levels allow inserting intermediate layers when needed without restructuring the entire system. For example, you could use `z-index: 250` for an element that needs to be above header but below dropdowns.

**Key concept:** Z-index only works on positioned elements (`position: relative`, `absolute`, `fixed`, or `sticky`). Non-positioned elements ignore z-index.

---

### 🚀 Usage

```scss
// Header navigation
.header {
	position: fixed;
	top: 0;
	z-index: var(--z-header);  // 200
}

// Dropdown menu
.dropdown {
	position: absolute;
	z-index: var(--z-dropdown);  // 300 - Above header
}

// Modal overlay and content
.modal-overlay {
	position: fixed;
	inset: 0;
	z-index: var(--z-modal);  // 500
	background: rgba(0, 0, 0, 0.5);
}

.modal-content {
	position: fixed;
	z-index: calc(var(--z-modal) + 1);  // 501 - Above overlay
}

// Tooltip
.tooltip {
	position: absolute;
	z-index: var(--z-tooltip);  // 600 - Above modals
}

// Toast notification
.notification {
	position: fixed;
	top: 20px;
	right: 20px;
	z-index: var(--z-notification);  // 700 - Highest priority
}

// Sticky sidebar
.sidebar {
	position: sticky;
	top: 0;
	z-index: var(--z-sticky);  // 400
}

// Elevated card
.card {
	position: relative;
	z-index: var(--z-base);  // 0 - Default
	
	&:hover {
		z-index: var(--z-content);  // 100 - Elevated on hover
	}
}
```

---

### ⚙️ Basic configuration

```scss
// tokens/_z-index.scss

$z-index: (
	base: 0,           // Default layer - most content
	content: 100,      // Elevated content - active elements
	header: 200,       // Fixed header
	sidebar: 200,      // Fixed sidebar (same level as header)
	footer: 200,       // Fixed footer
	dropdown: 300,     // Dropdown menus, select options
	sticky: 400,       // Sticky elements
	modal: 500,        // Modal dialogs and overlays
	tooltip: 600,      // Tooltips, popovers
	notification: 700  // Toast notifications, alerts
) !default;
```

**Generated CSS variables:**
```css
:root {
	--z-base: 0;
	--z-content: 100;
	--z-header: 200;
	--z-sidebar: 200;
	--z-footer: 200;
	--z-dropdown: 300;
	--z-sticky: 400;
	--z-modal: 500;
	--z-tooltip: 600;
	--z-notification: 700;
}
```

---

### 🔧 Customization

**Add custom layers:**
```scss
$z-index: (
	base: 0,
	content: 100,
	header: 200,
	sidebar: 200,
	footer: 200,
	dropdown: 300,
	sticky: 400,
	modal: 500,
	tooltip: 600,
	notification: 700,
	// Custom additions
	backdrop: 450,       // Between sticky and modal
	debug: 9999          // Development overlays
) !default;
```

**Adjust hierarchy:**
```scss
// Move tooltips above notifications
$z-index: (
	base: 0,
	content: 100,
	header: 200,
	dropdown: 300,
	sticky: 400,
	modal: 500,
	notification: 600,   // Swapped
	tooltip: 700         // Swapped
) !default;
```

**Use smaller increments:**
```scss
// For fine-grained control
$z-index: (
	base: 0,
	content: 10,
	header: 20,
	sidebar: 20,
	footer: 20,
	dropdown: 30,
	sticky: 40,
	modal: 50,
	tooltip: 60,
	notification: 70
) !default;
```

**Semantic naming:**
```scss
$z-index: (
	'layer-default': 0,
	'layer-elevated': 100,
	'layer-navigation': 200,
	'layer-overlay': 300,
	'layer-dialog': 500,
	'layer-alert': 700
) !default;
```

---

### ✔️ Best practices

**Z-index hierarchy:**
- `base` (0): Default for most content, cards, images
- `content` (100): Active/hover states that need slight elevation
- `header/sidebar/footer` (200): Fixed navigation elements
- `dropdown` (300): Contextual menus that appear on interaction
- `sticky` (400): Sticky positioned elements
- `modal` (500): Full-page overlays and dialogs
- `tooltip` (600): Always-visible hints and popovers
- `notification` (700): Critical alerts that must be seen

**Common patterns:**
```scss
// Modal with overlay
.modal {
	&__overlay {
		position: fixed;
		inset: 0;
		z-index: var(--z-modal);
		background: rgba(0, 0, 0, 0.5);
	}
	
	&__content {
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: calc(var(--z-modal) + 1);  // Above overlay
	}
	
	&__close-button {
		position: absolute;
		top: var(--sp-2);
		right: var(--sp-2);
		z-index: calc(var(--z-modal) + 2);  // Above content
	}
}

// Dropdown menu
.dropdown {
	position: relative;
	
	&__trigger {
		position: relative;
		z-index: var(--z-base);
	}
	
	&__menu {
		position: absolute;
		top: 100%;
		left: 0;
		z-index: var(--z-dropdown);
		box-shadow: var(--shadow-lg);
	}
}

// Sticky header
.page-header {
	position: sticky;
	top: 0;
	z-index: var(--z-header);
	background: var(--clr-secondary-100);
	box-shadow: var(--shadow-sm);
}
```

**Stacking context awareness:**
```scss
// ✅ Good: Positioned element with z-index
.elevated-card {
	position: relative;  // Creates stacking context
	z-index: var(--z-content);
}

// ❌ Bad: Z-index on non-positioned element (ignored)
.card {
	z-index: var(--z-content);  // Won't work without position
}

// ✅ Good: Use transform to create stacking context
.card {
	transform: translateZ(0);  // Creates stacking context
	z-index: var(--z-content);
}
```

**Nested stacking contexts:**
```scss
// Parent creates stacking context
.parent {
	position: relative;
	z-index: var(--z-content);  // 100
	
	.child {
		position: absolute;
		z-index: var(--z-modal);  // 500, but contained within parent's context
		// This child can't appear above elements with z-index > 100 outside parent
	}
}
```

---

### ❌ Common mistakes

**Don't use arbitrary z-index values:**
```scss
// ❌ Bad: Random high numbers
.modal {
	z-index: 999999;
}

.tooltip {
	z-index: 9999999;  // "Mine is higher!"
}

// ✅ Good: Use token system
.modal {
	z-index: var(--z-modal);
}

.tooltip {
	z-index: var(--z-tooltip);
}
```

**Don't forget position property:**
```scss
// ❌ Bad: Z-index without position
.element {
	z-index: var(--z-dropdown);  // Won't work!
}

// ✅ Good: Include position
.element {
	position: relative;
	z-index: var(--z-dropdown);
}
```

**Don't use negative z-index carelessly:**
```scss
// ❌ Bad: Negative z-index can hide elements
.background {
	z-index: -1;  // Might go behind page background
}

// ✅ Good: Use base (0) or low positive value
.background {
	z-index: var(--z-base);
	order: -1;  // Use flexbox/grid order instead
}
```

**Don't create too many stacking contexts:**
```scss
// ❌ Bad: Every element creates context
.card {
	position: relative;
	z-index: 1;
	
	.card-header {
		position: relative;
		z-index: 2;
		
		.card-title {
			position: relative;
			z-index: 3;  // Unnecessary complexity
		}
	}
}

// ✅ Good: Minimal stacking contexts
.card {
	position: relative;
	// No z-index needed if not overlapping
	
	.card-header {
		// No position/z-index needed
	}
}
```

**Don't mix z-index with transforms carelessly:**
```scss
// ⚠️ Warning: Transform creates new stacking context
.parent {
	z-index: var(--z-header);  // 200
	
	.child {
		transform: scale(1.1);  // Creates new context
		z-index: var(--z-modal);  // Trapped in parent's context
	}
}

// ✅ Good: Be aware of stacking context creation
.parent {
	position: relative;
	z-index: var(--z-header);
}

.child {
	// Use will-change instead if possible
	will-change: transform;
	z-index: var(--z-content);
}
```

**Don't hardcode intermediate values:**
```scss
// ❌ Bad: Hardcoded in-between values
.element {
	z-index: 250;  // Between header and dropdown
}

// ✅ Good: Use calc or add to tokens
.element {
	z-index: calc(var(--z-header) + 50);
}

// Or add to tokens:
$z-index: (
	// ...
	header: 200,
	'between-header-dropdown': 250,
	dropdown: 300,
	// ...
);
```