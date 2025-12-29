## 📜 Scrollbar styles

Configure scrollbar appearance across all browsers. Firefox uses standard CSS properties (`scrollbar-width`, `scrollbar-color`), while Webkit browsers (Chrome, Safari, Edge) rely on pseudo-elements like `::-webkit-scrollbar`.

---

### Basic scrollbar configuration

```scss
// base/_scrollbar.scss

html {
	/// Firefox scrollbar (thin style)
	@supports (scrollbar-width: thin) and (not selector(::-webkit-scrollbar)) {
		scrollbar-width: thin;
		scrollbar-color: var(--clr-scrollbar-thumb) var(--clr-scrollbar-track);
	}

	/// Webkit scrollbar (Chrome, Safari, Edge)
	&::-webkit-scrollbar {
		width: 0.5rem;

		&-thumb {
			background-color: var(--clr-scrollbar-thumb);

			&:hover {
				background-color: var(--clr-scrollbar-thumb-hover);
			}
		}

		&-track {
			background-color: var(--clr-scrollbar-track);
		}
	}
}
```

---

### Customization examples

```scss
/// Different scrollbar width
html::-webkit-scrollbar {
	width: 0.75rem;  s// Thicker scrollbar
	height: 0.75rem; // For horizontal scroll
}

/// Rounded scrollbar thumb
html::-webkit-scrollbar-thumb {
	border-radius: var(--rd-full);  // Fully rounded
	border: 2px solid transparent;  // Gap around thumb
	background-clip: padding-box;   // Clip to padding
}

/// Hide scrollbar but keep functionality
.no-scrollbar {
	scrollbar-width: none; // Firefox

	&::-webkit-scrollbar {
		display: none; // Webkit
	}
}

/// Colored scrollbar for specific element
.custom-scroll {
	scrollbar-color: #ff6b6b #f8f9fa; // Firefox

	&::-webkit-scrollbar-thumb {
		background: linear-gradient(180deg, #ff6b6b, #ee5a52); // Gradient
	}
}
```

---

### Available options

**Firefox:**

- `scrollbar-width`: `auto` (default), `thin`, `none`
- `scrollbar-color`: `<thumb-color> <track-color>`

**Webkit:**

- `::-webkit-scrollbar` - scrollbar container
- `::-webkit-scrollbar-thumb` - draggable element
- `::-webkit-scrollbar-track` - background track
- `::-webkit-scrollbar-button` - arrow buttons (optional)
