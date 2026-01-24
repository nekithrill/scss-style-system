> **📁 Location:** `styles/tokens/_shadows.scss`
> **📦 Type:** Token

## 🌫️ Shadow tokens

Shadow tokens define elevation levels for consistent depth across your interface.

<br>

### 🧠 How it works

Shadow tokens create visual hierarchy by simulating depth and layering. The system provides 6 pre-defined elevation levels:

**Shadow scale (`--shadow-*`)** ranges from `xs` (subtle depth) to `xl` (dramatic elevation), plus a special `inset` value for pressed/depressed states. Each shadow uses the same base color but varies in blur radius and spread.

**Base shadow color** (`$base-shadow`) is defined once and used across all shadows, making it easy to adjust the overall shadow intensity or color globally. The default is 10% black (`rgb(0 0 0 / 10%)`).

Shadows are generated as CSS custom properties and can be used directly in `box-shadow` declarations. The values stay in their original units (px for offsets, rgb/rgba for colors) rather than converting to rem.

**Key concept:** Higher shadow values = larger blur + more offset = appears further from surface.

---

### 🚀 Usage

```scss
.card {
	box-shadow: var(--shadow-md);
	
	&:hover {
		box-shadow: var(--shadow-lg);
	}
}

.button {
	box-shadow: var(--shadow-sm);
	
	&:active {
		box-shadow: var(--shadow-inset);
	}
}

.modal {
	box-shadow: var(--shadow-xl);
}

// Subtle separator
.list-item {
	border-bottom: 1px solid var(--clr-neutral-200);
	
	&.elevated {
		border: none;
		box-shadow: var(--shadow-xs);
	}
}
```

---

### ⚙️ Basic configuration

```scss
// tokens/_shadows.scss

// Base shadow color (10% black)
$base-shadow: rgb(0 0 0 / 10%) !default;

$shadows: (
	xs: 0 1px 2px $base-shadow,          // Subtle depth
	sm: 0 1px 3px $base-shadow,          // Buttons, inputs
	md: 0 2px 6px $base-shadow,          // Cards
	lg: 0 4px 12px $base-shadow,         // Modals, dropdowns
	xl: 0 8px 24px $base-shadow,         // Major elevations
	inset: inset 0 2px 4px $base-shadow  // Pressed states
) !default;
```

**Generated CSS variables:**
```css
:root {
	--shadow-xs: 0 1px 2px rgb(0 0 0 / 10%);
	--shadow-sm: 0 1px 3px rgb(0 0 0 / 10%);
	--shadow-md: 0 2px 6px rgb(0 0 0 / 10%);
	--shadow-lg: 0 4px 12px rgb(0 0 0 / 10%);
	--shadow-xl: 0 8px 24px rgb(0 0 0 / 10%);
	--shadow-inset: inset 0 2px 4px rgb(0 0 0 / 10%);
}
```

---

### 🔧 Customization

**Adjust shadow intensity:**
```scss
// Darker shadows
$base-shadow: rgb(0 0 0 / 15%);

// Lighter shadows
$base-shadow: rgb(0 0 0 / 5%);
```

**Use colored shadows:**
```scss
// Indigo tint for brand consistency
$base-shadow: rgb(99 102 241 / 20%);

// Brand color shadow
$base-shadow: rgb(139 92 246 / 15%);
```

**Add new shadow levels:**
```scss
$shadows: (
	xs: 0 1px 2px $base-shadow,
	sm: 0 1px 3px $base-shadow,
	md: 0 2px 6px $base-shadow,
	lg: 0 4px 12px $base-shadow,
	xl: 0 8px 24px $base-shadow,
	'2xl': 0 16px 48px $base-shadow,  // New: dramatic elevation
	inset: inset 0 2px 4px $base-shadow
);
```

**Adjust specific shadow values:**
```scss
$shadows: (
	xs: 0 1px 2px $base-shadow,
	sm: 0 2px 4px $base-shadow,      // Stronger
	md: 0 4px 8px $base-shadow,      // Stronger
	lg: 0 8px 16px $base-shadow,     // Stronger
	xl: 0 16px 32px $base-shadow,    // Stronger
	inset: inset 0 2px 4px $base-shadow
);
```

---

### ✔️ Best practices

**Shadow hierarchy:**
- Use `xs` for subtle separation (table rows, dividers)
- Use `sm` for interactive elements (buttons, inputs)
- Use `md` for elevated surfaces (cards, panels)
- Use `lg` for floating elements (dropdowns, tooltips)
- Use `xl` for major overlays (modals, dialogs)
- Use `inset` for pressed/active states

**Performance considerations:**
```scss
// ✅ Good: Animate transform or opacity
.card {
	box-shadow: var(--shadow-sm);
	transition: transform 0.3s ease, box-shadow 0.3s ease;
	
	&:hover {
		transform: translateY(-2px);
		box-shadow: var(--shadow-md);
	}
}

// ❌ Avoid: Animating shadow alone on low-end devices
.card {
	transition: box-shadow 0.3s ease; // Can be janky
}

// ⚡ Better: Use will-change for hover transitions
.card {
	box-shadow: var(--shadow-sm);
	
	&:hover {
		will-change: box-shadow;
		box-shadow: var(--shadow-md);
	}
}
```

**Accessibility:**
- Don't rely solely on shadows to convey information
- Ensure sufficient contrast remains with shadow overlays
- Test shadows in both light and dark themes
- Consider users with reduced transparency preferences

**Layering examples:**
```scss
// Layered cards with progressive elevation
.card-container {
	.card {
		box-shadow: var(--shadow-sm);
		
		&:hover {
			box-shadow: var(--shadow-md);
			transform: translateY(-2px);
			transition: all 0.2s ease;
		}
	}
}

// Floating action button
.fab {
	box-shadow: var(--shadow-lg);
	
	&:hover {
		box-shadow: var(--shadow-xl);
	}
	
	&:active {
		box-shadow: var(--shadow-md);
	}
}

// Pressed button state
.button {
	box-shadow: var(--shadow-sm);
	
	&:active {
		box-shadow: var(--shadow-inset);
		transform: scale(0.98);
	}
}

// Multi-layer shadow for depth
.elevated-card {
	box-shadow: 
		var(--shadow-sm),
		var(--shadow-lg);
}
```

---

### ❌ Common mistakes

**Don't mix shadow scales randomly:**
```scss
// ❌ Bad: inconsistent elevation
.card {
	box-shadow: var(--shadow-xs);
	
	&:hover {
		box-shadow: var(--shadow-xl); // Too dramatic jump
	}
}

// ✅ Good: gradual elevation
.card {
	box-shadow: var(--shadow-sm);
	
	&:hover {
		box-shadow: var(--shadow-md); // One level up
	}
}
```

**Don't hardcode shadow values:**
```scss
// ❌ Bad: hardcoded shadow
.card {
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

// ✅ Good: use token
.card {
	box-shadow: var(--shadow-md);
}
```

**Don't forget theme compatibility:**
```scss
// ❌ Bad: black shadow in dark theme looks wrong
$base-shadow: rgb(0 0 0 / 10%);

// ✅ Better: adjust per theme or use transparent black
// In dark theme, consider lighter/more subtle shadows:
[data-theme='dark'] {
	// Override shadows if needed
	--shadow-sm: 0 1px 3px rgb(0 0 0 / 30%);
	--shadow-md: 0 2px 6px rgb(0 0 0 / 40%);
}
```