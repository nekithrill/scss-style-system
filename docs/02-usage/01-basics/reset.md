## ♻️ Basic styles reset

Modern CSS Reset based on modern best practices and browser defaults.

> Sources:
> [Josh Comeau's CSS Reset](https://www.joshwcomeau.com/css/custom-css-reset/),
> [Andy Bell's Modern Reset](https://gist.github.com/Asjas/4b0736108d56197fce0ec9068145b421),
> [Elad Shechter](https://github.com/elad2412/the-new-css-reset)

<br>

### Reset configuration
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

<br>

### Customization example
```scss
// Remove iOS default styling
button,
input,
textarea,
select {
	-webkit-appearance: none;
	appearance: none;
}

// Custom focus styles (replace default outline)
*:focus {
	outline: none; // Only if styling :focus-visible
}

*:focus-visible {
	outline: 2px solid var(--clr-primary-500);
	outline-offset: 2px;
}
```