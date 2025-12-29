## 🔤 Connecting font

Connect custom fonts using `@font-face` declarations.

1. Specify `font-family` name
2. Specify path to font files
3. Specify font weights (individual or variable font range)

> 💡 **Two approaches:** Load individual weights (Regular, Bold) or use a variable font with weight range (300-700).

```scss
// base/_fonts.scss

/// Approach 1: Individual weights
@font-face {
	font-family: YourFont;
	font-weight: 400;
	font-style: normal;
	font-display: swap;
	src:
		url('/fonts/YourFont-Regular.woff2') format('woff2'),
		url('/fonts/YourFont-Regular.woff') format('woff');
}

@font-face {
	font-family: YourFont;
	font-weight: 700;
	font-style: normal;
	font-display: swap;
	src:
		url('/fonts/YourFont-Bold.woff2') format('woff2'),
		url('/fonts/YourFont-Bold.woff') format('woff');
}

/// Approach 2: Variable font (weight range 300-700)
@font-face {
	font-family: YourFont;
	font-weight: 300 700;
	font-style: normal;
	font-display: swap;
	src:
		url('/fonts/YourFont-Variable.woff2') format('woff2'),
		url('/fonts/YourFont-Variable.woff') format('woff');
}
```

**Best practices:**

- Use `.woff2` (best compression) + `.woff` (fallback)
- Set `font-display: swap` to prevent invisible text during loading
- Variable fonts reduce file size when you need multiple weights
