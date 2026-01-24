## 🌐 Global styles

Foundation styles for html, body, and heading elements with design token integration.

<br>

### 🧠 How it works

Global styles establish baseline typography and colors that apply throughout the application:

**:root declarations:** Sets default text colors (`--clr-text`, `--clr-text-accent`) that themes can override, plus `accent-color` for form controls.

**html element:** Sets base font size from tokens and enables smooth scrolling for anchor links.

**body element:** Establishes minimum height, font family hierarchy, weight, and text color using tokens.

**Headings (h1-h6):** Assigns bold weight and accent font family, with sizes defined individually using typography tokens.

These styles serve as sensible defaults that can be overridden by themes or component-specific styles.

---

### 🚀 Usage

```scss
// Global styles apply automatically
// No imports needed in components

// They provide defaults that you can override:
.custom-heading {
	font-family: var(--ff-primary);  // Override accent font
	font-weight: var(--fw-regular);  // Override bold
}

.custom-text {
	color: var(--clr-primary-500);   // Override default text color
}
```

---

### ⚙️ Configuration

```scss
// base/_globals.scss

:root {
	// Default text colors (overridden by themes)
	--clr-text: var(--clr-neutral-900);
	--clr-text-accent: var(--clr-primary-500);
	accent-color: var(--clr-text-accent);
}

html {
	height: 100%;
	font-size: var(--fs-default);
	scroll-behavior: smooth;
}

body {
	min-height: 100%;
	font-family: var(--ff-primary), var(--ff-system);
	font-weight: var(--fw-regular);
	color: var(--clr-text);
}

h1, h2, h3, h4, h5, h6 {
	font-weight: var(--fw-bold);
	font-family: var(--ff-accent), var(--ff-primary), var(--ff-system);
}

h1 { font-size: var(--fs-h1); }
h2 { font-size: var(--fs-h2); }
h3 { font-size: var(--fs-h3); }
h4 { font-size: var(--fs-h4); }
h5 { font-size: var(--fs-h5); }
h6 { font-size: var(--fs-h6); }
```

---

### 🔧 Customization

```scss
// Add line-height to body
body {
	min-height: 100%;
	line-height: 1.6;
	font-family: var(--ff-primary), var(--ff-system);
	font-weight: var(--fw-regular);
	color: var(--clr-text);
}

// Add custom heading styles
h1, h2, h3 {
	font-weight: var(--fw-extra-bold);
	line-height: 1.2;
	margin-bottom: var(--sp-3);
}

// Disable smooth scrolling if user prefers reduced motion
@media (prefers-reduced-motion: reduce) {
	html {
		scroll-behavior: auto;
	}
}

// Custom accent color per theme
[data-theme='dark'] {
	accent-color: var(--clr-primary-400);
}
```

---

### ✔️ Best practices

- ✅ **Do:** Use design tokens for all values
- ✅ **Do:** Let themes override default colors
- ✅ **Do:** Provide fallback fonts
- ✅ **Do:** Test smooth scrolling UX
- ❌ **Don't:** Hardcode font sizes or colors
- ❌ **Don't:** Set line-height here (better in reset or components)
- ❌ **Don't:** Override too much (keep it minimal)

```scss
// ✅ Good: Token-based
body {
	font-family: var(--ff-primary), var(--ff-system);
	color: var(--clr-text);
}

// ❌ Bad: Hardcoded
body {
	font-family: 'Arial', sans-serif;
	color: #333;
}
```

---

### ❌ Common mistakes

**Forgetting fallbacks:**
```scss
// ❌ Bad: No fallback
body {
	font-family: var(--ff-primary);
}

// ✅ Good: System font fallback
body {
	font-family: var(--ff-primary), var(--ff-system);
}
```

**Conflicting with reset:**
```scss
// ❌ Bad: Conflicts with reset.scss
h1 {
	font-size: var(--fs-h1);
	margin-bottom: 1rem;  // Reset removes this anyway
}

// ✅ Good: Let reset handle margins
h1 {
	font-size: var(--fs-h1);
}
```