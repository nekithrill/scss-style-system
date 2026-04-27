> 📁 **Location:** `styles/base/_reset.scss`
> 🎯 **Scope:** Browser style normalization
> 🏷️ **Type:** Basic

# 🔄 CSS Reset

Removes browser inconsistencies and provides a predictable foundation. Intentionally minimal — only resets what causes real cross-browser issues.

## ⚙️ Configuration

```scss
// Box sizing
*,
*::before,
*::after {
	box-sizing: border-box;
}

// Margins and padding
* {
	margin: 0;
	padding: 0;
}

// Responsive media
img, picture, video, canvas, svg {
	display: block;
	max-width: 100%;
}

// Form elements — inherit typography
input, button, textarea, select {
	font: inherit;
	color: inherit;
	background: transparent;
	line-height: var(--lh-compact, 1);
}

textarea {
	line-height: var(--lh-normal, 1.5);
	resize: vertical;
	overflow: auto;
}

// Lists
ol, ul {
	list-style: none;
}

// Headings — sized via globals.scss
h1, h2, h3, h4, h5, h6 {
	font-size: inherit;
	font-weight: inherit;
}

// Links
a {
	text-decoration: none;
	color: inherit;
}

// Buttons
button {
	background: none;
	border: none;
	padding: 0;
	cursor: pointer;
	font: inherit;
	color: inherit;
}

// Tables
table {
	border-collapse: collapse;
	border-spacing: 0;
}

// Quotes
blockquote, q {
	quotes: none;
}

blockquote::before, blockquote::after,
q::before, q::after {
	content: '';
	content: none;
}

// Text overflow
p, h1, h2, h3, h4, h5, h6 {
	overflow-wrap: break-word;
}

// Root stacking context
#root, #__next {
	isolation: isolate;
}
```

List styles are removed by default. Add them back in content areas:

```scss
.prose ul {
	list-style: disc;
	padding-left: var(--sp-4);
}
```