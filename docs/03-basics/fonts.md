> **📁 Location:** `styles/base/_fonts.scss`
> **📦 Type:** Basic

## 🔤 Font loading

Font face declarations for loading custom web fonts with optimal performance.

<br>

### 🧠 How it works

This file loads custom font files using `@font-face` declarations. The system supports:

**Multiple font weights:** Separate font files for regular (400), medium (500), and bold (700) weights ensure precise typography control.

**Variable fonts:** Optional variable font declaration (`font-weight: 300 700`) provides a range of weights from a single file, reducing HTTP requests.

**Font-display strategy:** Uses `font-display: swap` to show fallback fonts immediately while custom fonts load, preventing invisible text (FOIT) and improving perceived performance.

**Format fallbacks:** Includes both WOFF2 (modern, best compression) and WOFF (older browser support) formats for maximum compatibility.

**Important:** Update the file paths (`path/to/...`) to match your actual font file locations before using in production.

---

### 🚀 Usage

```scss
// Fonts are loaded automatically when imported in main.scss
// Use the font-family tokens in your styles:

.text {
	font-family: var(--ff-primary);  // JetBrains
	font-weight: var(--fw-regular);  // 400
}

.heading {
	font-family: var(--ff-accent);   // Tektur
	font-weight: var(--fw-bold);     // 700
}
```

---

### ⚙️ Configuration

```scss
// base/_fonts.scss

// Regular (400)
@font-face {
	font-family: JetBrains;
	font-weight: 400;
	font-style: normal;
	font-display: swap;
	src:
		url('path/to/JetBrains-Regular.woff2') format('woff2'),
		url('path/to/JetBrains-Regular.woff') format('woff');
}

// Medium (500)
@font-face {
	font-family: JetBrains;
	font-weight: 500;
	font-style: normal;
	font-display: swap;
	src:
		url('path/to/JetBrains-Medium.woff2') format('woff2'),
		url('path/to/JetBrains-Medium.woff') format('woff');
}

// Bold (700)
@font-face {
	font-family: JetBrains;
	font-weight: 700;
	font-style: normal;
	font-display: swap;
	src:
		url('path/to/JetBrains-Bold.woff2') format('woff2'),
		url('path/to/JetBrains-Bold.woff') format('woff');
}

// Variable font (weight range 300-700)
@font-face {
	font-family: JetBrains;
	font-weight: 300 700;
	font-style: normal;
	font-display: swap;
	src:
		url('path/to/JetBrains-Variable.woff2') format('woff2'),
		url('path/to/JetBrains-Variable.woff') format('woff');
}
```

---

### 🔧 Customization

**Load different fonts:**
```scss
// Replace with your font
@font-face {
	font-family: Inter;
	font-weight: 400;
	font-style: normal;
	font-display: swap;
	src:
		url('/fonts/Inter-Regular.woff2') format('woff2'),
		url('/fonts/Inter-Regular.woff') format('woff');
}

// Update typography tokens to match
// In tokens/_typography.scss:
$font-families: (
	primary: 'Inter',
	// ...
);
```

**Add italic variants:**
```scss
@font-face {
	font-family: JetBrains;
	font-weight: 400;
	font-style: italic;  // Italic variant
	font-display: swap;
	src:
		url('/fonts/JetBrains-Italic.woff2') format('woff2'),
		url('/fonts/JetBrains-Italic.woff') format('woff');
}
```

**Use only variable font:**
```scss
// Single file for all weights
@font-face {
	font-family: Inter;
	font-weight: 100 900;  // Full range
	font-style: normal;
	font-display: swap;
	src: url('/fonts/Inter-Variable.woff2') format('woff2');
}
```

**Preload critical fonts:**
```html
<!-- In your HTML <head> -->
<link rel="preload" href="/fonts/JetBrains-Regular.woff2" as="font" type="font/woff2" crossorigin>
```

---

### ✔️ Best practices

- ✅ **Do:** Use WOFF2 format (best compression)
- ✅ **Do:** Use `font-display: swap` to avoid invisible text
- ✅ **Do:** Load only weights you actually use
- ✅ **Do:** Update font paths before deployment
- ✅ **Do:** Consider variable fonts for multiple weights
- ❌ **Don't:** Load all font weights unnecessarily
- ❌ **Don't:** Use EOT or TTF formats (outdated)
- ❌ **Don't:** Forget to update typography tokens
- ❌ **Don't:** Use `font-display: block` (causes FOIT)

```scss
// ✅ Good: Load only needed weights
@font-face {
	font-family: Inter;
	font-weight: 400;  // Regular
	// ...
}

@font-face {
	font-family: Inter;
	font-weight: 700;  // Bold
	// ...
}

// ❌ Bad: Loading every weight
// Thin, Extra-light, Light, Regular, Medium, 
// Semi-bold, Bold, Extra-bold, Black...
// (unnecessary HTTP requests)
```

---

### ❌ Common mistakes

**Wrong paths:**
```scss
// ❌ Bad: Generic placeholder
src: url('path/to/font.woff2');

// ✅ Good: Actual file path
src: url('/fonts/JetBrains-Regular.woff2');
```

**Missing font-display:**
```scss
// ❌ Bad: No font-display (can cause FOIT)
@font-face {
	font-family: Inter;
	src: url('/fonts/Inter.woff2');
}

// ✅ Good: Always include font-display
@font-face {
	font-family: Inter;
	font-display: swap;
	src: url('/fonts/Inter.woff2');
}
```

**Mismatched weights:**
```scss
// ❌ Bad: Using weight not loaded
.text {
	font-family: var(--ff-primary);
	font-weight: 600;  // But we only loaded 400, 500, 700!
}

// ✅ Good: Use loaded weights
.text {
	font-family: var(--ff-primary);
	font-weight: var(--fw-medium);  // 500 - loaded ✓
}
```