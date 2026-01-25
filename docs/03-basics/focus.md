> **📁 Location:** `styles/base/_focus.scss`
> **🧭 Scope:** Focus visibility and accessibility states
> **📦 Type:** Basic

## ⌨️ Focus styles

Custom focus indicators for accessibility that show only during keyboard navigation.

<br>

### 🧠 How it works

This system uses the `:focus-visible` pseudo-class to intelligently show focus indicators only when needed:

**Keyboard navigation:** When users navigate with Tab, arrow keys, or other keyboard input, the browser adds the `:focus-visible` state and focus rings appear.

**Mouse/touch navigation:** When users click or tap, the browser only adds `:focus`, not `:focus-visible`, so focus rings are hidden. This prevents distracting outlines when clicking buttons or links.

**Why this matters:** Traditional `:focus` styles show outlines for both keyboard and mouse users. The `:focus-visible` approach improves UX by only showing outlines when they're actually helpful (keyboard navigation) while maintaining full accessibility.

The focus ring uses theme variables (`--clr-text-accent`) so it automatically adapts to light/dark themes, and uses `--stroke-normal` for consistent width with other UI elements.

---

### 🚀 Usage

```scss
// Focus styles are applied automatically to interactive elements
// No additional code needed in your components

.button {
	// Button styles...
	// Focus ring appears automatically on keyboard navigation
}

.link {
	// Link styles...
	// Focus ring appears automatically on keyboard navigation
}
```

**What gets focus rings:**
- Form elements: `input`, `textarea`, `select`
- Interactive elements: `button`, `a` (links)
- ARIA elements: `[role='button']`
- Custom interactive elements: `[tabindex]`

---

### ⚙️ Configuration

```scss
// base/_focus.scss

// Show outline ONLY for keyboard navigation
input:focus-visible,
textarea:focus-visible,
select:focus-visible,
button:focus-visible,
a:focus-visible,
[role='button']:focus-visible,
[tabindex]:focus-visible {
	outline: var(--stroke-normal) solid var(--clr-text-accent);
	outline-offset: 2px;
}

// Hide outline for mouse/touch users
input:focus:not(:focus-visible),
textarea:focus:not(:focus-visible),
select:focus:not(:focus-visible),
button:focus:not(:focus-visible),
a:focus:not(:focus-visible),
[role='button']:focus:not(:focus-visible),
[tabindex]:focus:not(:focus-visible) {
	outline: none;
}
```

---

### 🔧 Customization

```scss
// Different color
input:focus-visible,
button:focus-visible {
	outline: var(--stroke-normal) solid var(--clr-primary-500);
	outline-offset: 2px;
}

// Box-shadow instead of outline
button:focus-visible {
	outline: none;
	box-shadow: 0 0 0 var(--stroke-normal) var(--clr-text-accent);
}

// Per-element customization
input:focus-visible {
	outline: var(--stroke-normal) solid var(--clr-primary-500);
}

button:focus-visible {
	outline: var(--stroke-thick) solid var(--clr-primary-600);
	outline-offset: 4px;
}
```

---

### ✔️ Best practices

- ✅ **Do:** Keep focus indicators visible for keyboard users
- ✅ **Do:** Use theme colors so focus adapts to light/dark mode
- ✅ **Do:** Ensure sufficient contrast (WCAG AA: 3:1 minimum)
- ✅ **Do:** Test with keyboard navigation (Tab key)
- ❌ **Don't:** Remove focus indicators entirely
- ❌ **Don't:** Use low-contrast colors
- ❌ **Don't:** Use `:focus` alone without `:focus-visible`

```scss
// ✅ Good: Handled automatically
.button {
	background: var(--clr-primary-500);
	padding: var(--sp-2) var(--sp-4);
	// Focus handled by global styles
}

// ❌ Bad: Removes all focus
* {
	outline: none !important;
}
```

---

### ❌ Common mistakes

**Don't kill all focus styles:**
```scss
// ❌ Bad
* { outline: none !important; }

// ✅ Good: Use :focus-visible
```

**Don't forget outline-offset:**
```scss
// ❌ Bad: No breathing room
input:focus-visible {
	outline: 2px solid var(--clr-text-accent);
}

// ✅ Good: Space between element and outline
input:focus-visible {
	outline: var(--stroke-normal) solid var(--clr-text-accent);
	outline-offset: 2px;
}
```