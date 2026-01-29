> **📁 Location:** `styles/base/_reset.scss`
> **🧭 Scope:** Browser style normalization
> **📦 Type:** Basic

# 🔄 CSS Reset

Minimal CSS reset that removes browser inconsistencies and provides a clean foundation.

## 🧠 How it works

This reset removes default browser styles that cause cross-browser inconsistencies:

- **Box-sizing:** Sets `border-box` on all elements so padding/border are included in width calculations.
- **Margins/padding:** Removes all default spacing for a predictable starting point.
- **Body:** Improves text rendering and sets comfortable line-height (1.5).
- **Media:** Makes images/videos responsive by default, preventing overflow.
- **Form elements:** Inherit typography from parent for consistency.
- **Lists:** Removes bullets/numbers (add back in content areas if needed).
- **Headings:** Reset to inherit size/weight (defined in globals.scss instead).
- **Links:** Removes underline and inherits color (style per component).
- **Buttons:** Removes all default styles for custom button designs.
- **Text overflow:** Prevents long words from breaking layouts.
- **Root isolation:** Creates stacking context for React/Next.js roots.

## 🚀 Usage

```scss
// Reset applies automatically - provides clean foundation
// Build your components on top:

.button {
	// No default button styles to override
	padding: var(--sp-2) var(--sp-4);
	background: var(--clr-primary-500);
	border-radius: var(--rd-md);
}
```

## ⚙️ Configuration

Key features: box-sizing, margin/padding reset, responsive media, form inheritance, list reset, button reset, text overflow prevention.

```scss
// Box sizing - use border-box for predictable sizing
*,
*::before,
*::after {
	box-sizing: border-box;
}

// Remove default margins/padding for consistent starting point
* {
	margin: 0;
	padding: 0;
}

// Body - better readability and text rendering
body {
	line-height: 1.5;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}

// Media - responsive by default, maintain aspect ratio
img,
picture,
video,
canvas,
svg {
	display: block;
	max-width: 100%;
	height: auto;
}

// Form elements - inherit typography for consistency
input,
button,
textarea,
select {
	font: inherit;
	color: inherit;
	background: transparent;
}

// Lists - remove default styles (add back in content areas if needed)
ol,
ul {
	list-style: none;
}

// Headings - reset to use design tokens instead
h1,
h2,
h3,
h4,
h5,
h6 {
	font-size: inherit;
	font-weight: inherit;
}

// Links - remove underline, inherit color
a {
	text-decoration: none;
	color: inherit;
}

// Buttons - clean slate for custom styling
button {
	background: none;
	border: none;
	padding: 0;
	cursor: pointer;
	font: inherit;
	color: inherit;
}

// Tables - consistent rendering across browsers
table {
	border-collapse: collapse;
	border-spacing: 0;
}

// Quotes - remove default quotation marks
blockquote,
q {
	quotes: none;
}

blockquote::before,
blockquote::after,
q::before,
q::after {
	content: '';
	content: none;
}

// Text overflow - prevent long words from breaking layout
p,
h1,
h2,
h3,
h4,
h5,
h6 {
	overflow-wrap: break-word;
}

// Root stacking context - prevents z-index issues
#root,
#__next {
	isolation: isolate;
}
```

## ✔️ Best practices

- ✅ **Do:** Apply reset before other styles
- ✅ **Do:** Add back list styles in content areas
- ✅ **Do:** Style form elements explicitly
- ❌ **Don't:** Modify the reset (it's intentionally minimal)
- ❌ **Don't:** Rely on default browser styles


## ❌ Common mistakes

**Expecting default list styles:**

```scss
// ❌ Lists have no bullets after reset
<ul>
  <li>Item</li>
</ul>

// ✅ Add them back in content
.content ul {
	list-style: disc;
	padding-left: var(--sp-4);
}
```