## 🖱️ Selection styles

Customize text selection highlight using the `::selection` pseudo-element. Control background color, text color, and other properties when users highlight text across the application.

<br>

### Basic selection configuration
```scss
// base/_selection.scss

::selection {
	background-color: var(--clr-selection-bg);
	color: var(--clr-selection-text);

	// Optional: text shadow for better readability
	text-shadow: none;
}
```

<br>

### Customization examples
```scss
// Vibrant selection highlight
::selection {
	background-color: gold; // Gold background
	color: black;           // Black text
	text-shadow: none;
}

// Semi-transparent selection
::selection {
	background-color: rgba(59, 130, 246, 0.3); // Blue with opacity
	color: inherit;                             // Keep original text color
}

// Custom selection for specific elements
code::selection,
pre::selection {
	background-color: var(--clr-code-selection);
	color: var(--clr-code-text);
}

// Different selection for links
a::selection {
	background-color: var(--clr-link-selection);
	text-decoration-color: currentColor; // Maintain underline color
}

// No selection for certain elements
.no-select {
	user-select: none; // Prevent text selection entirely
}
```

<br>

### Available properties

**Supported properties for `::selection`:**

- `background-color` / `background` - highlight background
- `color` - text color
- `text-shadow` - text shadow (usually set to `none`)
- `text-decoration-color` - underline/strikethrough color
- `cursor` - cursor type (limited support)

> 💡 Not all CSS properties work with `::selection`. Properties like `padding`, `margin`, `border` are not supported.