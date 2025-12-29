## 🌫️ Shadow tokens

Shadow tokens define elevation levels for consistent depth across your interface.

**Location:** `tokens/_shadows.scss`

---

### Default shadows
```scss
// tokens/_shadows.scss

/// Base shadow color (10% black)
$base-shadow: rgb(0 0 0 / 10%);

$shadows: (
	xs: 0 1px 2px $base-shadow,      // Subtle depth
	sm: 0 1px 3px $base-shadow,      // Buttons, inputs
	md: 0 2px 6px $base-shadow,      // Cards
	lg: 0 4px 12px $base-shadow,     // Modals, dropdowns
	xl: 0 8px 24px $base-shadow,     // Major elevations
	inset: inset 0 2px 4px $base-shadow  // Pressed states
);
```

**Generated CSS variables:**
```css
:root {
	--shd-xs: 0 0.0625rem 0.125rem rgba(0, 0, 0, 0.1);
	--shd-sm: 0 0.0625rem 0.1875rem rgba(0, 0, 0, 0.1);
	--shd-md: 0 0.125rem 0.375rem rgba(0, 0, 0, 0.1);
	--shd-lg: 0 0.25rem 0.75rem rgba(0, 0, 0, 0.1);
	--shd-xl: 0 0.5rem 1.5rem rgba(0, 0, 0, 0.1);
	--shd-inset: inset 0 0.125rem 0.25rem rgba(0, 0, 0, 0.1);
}
```

---

### Usage
```scss
.card {
	box-shadow: var(--shd-md);
	
	&:hover {
		box-shadow: var(--shd-lg);
	}
}

.button {
	box-shadow: var(--shd-sm);
	
	&:active {
		box-shadow: var(--shd-inset);
	}
}

.modal {
	box-shadow: var(--shd-xl);
}
```

---

### Customization

#### Adjust shadow intensity
```scss
// Darker shadows
$base-shadow: rgb(0 0 0 / 15%);

// Lighter shadows
$base-shadow: rgb(0 0 0 / 5%);
```

#### Use colored shadows
```scss
// Indigo tint
$base-shadow: rgb(99 102 241 / 20%);

// Brand color shadow
$base-shadow: rgb(139 92 246 / 15%);
```

#### Add new shadow levels
```scss
$shadows: (
	xs: 0 1px 2px $base-shadow,
	sm: 0 1px 3px $base-shadow,
	md: 0 2px 6px $base-shadow,
	lg: 0 4px 12px $base-shadow,
	xl: 0 8px 24px $base-shadow,
	2xl: 0 16px 48px $base-shadow,  // ← New: dramatic elevation
	inset: inset 0 2px 4px $base-shadow
);
```

#### Adjust specific shadow values
```scss
$shadows: (
	xs: 0 1px 2px $base-shadow,
	sm: 0 2px 4px $base-shadow,      // ← Stronger
	md: 0 4px 8px $base-shadow,      // ← Stronger
	lg: 0 8px 16px $base-shadow,     // ← Stronger
	xl: 0 16px 32px $base-shadow,    // ← Stronger
	inset: inset 0 2px 4px $base-shadow
);
```

---

### Best practices

**Shadow hierarchy:**
- Use `xs` for subtle separation (table rows, dividers)
- Use `sm` for interactive elements (buttons, inputs)
- Use `md` for elevated surfaces (cards, panels)
- Use `lg` for floating elements (dropdowns, tooltips)
- Use `xl` for major overlays (modals, dialogs)
- Use `inset` for pressed/active states

**Performance:**
- Shadows can impact performance on low-end devices
- Avoid animating shadows directly; animate `opacity` or `transform` instead
- Consider using `will-change: box-shadow` for hover transitions

**Accessibility:**
- Don't rely solely on shadows to convey information
- Ensure sufficient contrast remains with shadow overlays
- Test shadows in both light and dark themes

**Theme compatibility:**
- Use `rgba()` or `rgb()` with alpha for proper theme support
- Colored shadows may need adjustment in dark themes
- Consider separate `$base-shadow` values per theme if needed

---

### Common patterns

**Layered cards:**
```scss
.card-container {
	.card {
		box-shadow: var(--shd-sm);
		
		&:hover {
			box-shadow: var(--shd-md);
			transform: translateY(-2px);
			transition: all 0.2s ease;
		}
	}
}
```

**Floating action button:**
```scss
.fab {
	box-shadow: var(--shd-lg);
	
	&:hover {
		box-shadow: var(--shd-xl);
	}
	
	&:active {
		box-shadow: var(--shd-md);
	}
}
```

**Pressed button:**
```scss
.button {
	box-shadow: var(--shd-sm);
	
	&:active {
		box-shadow: var(--shd-inset);
		transform: scale(0.98);
	}
}
```

**Multi-layer shadow (for depth):**
```scss
.elevated-card {
	box-shadow: 
		var(--shd-sm),
		var(--shd-lg);
}
```