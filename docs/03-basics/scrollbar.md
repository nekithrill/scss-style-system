> 📂 **Location:** `styles/base/_scrollbar.scss`
> 🎯 **Scope:** Custom scrollbar appearance
> 🏷️ **Type:** Basic

# 📜 Custom scrollbar

Themed scrollbars for Firefox and Webkit. Uses semantic variables that themes define.

## ⚙️ Configuration

```scss
// styles/base/_scrollbar.scss

* {
	// Firefox
	@supports (scrollbar-width: thin) and (not selector(::-webkit-scrollbar)) {
		scrollbar-width: thin;
		scrollbar-color: var(--clr-scrollbar-thumb, red) var(--clr-scrollbar-track, maroon);
	}

	// Webkit (Chrome, Safari, Edge)
	&::-webkit-scrollbar {
		width: 0.5rem;

		&-thumb {
			background-color: var(--clr-scrollbar-thumb, red);

			&:hover {
				background-color: var(--clr-scrollbar-thumb-hover, tomato);
			}
		}

		&-track {
			background-color: var(--clr-scrollbar-track, maroon);
		}
	}
}
```

Fallback colors (`red`, `maroon`, `tomato`) are intentionally obvious — replace them in your theme.

## 🔧 Customization

**Define colors in theme:**

```scss
:root {
	--clr-scrollbar-thumb:       var(--clr-neutral-400);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track:       var(--clr-neutral-100);
}

[data-theme='dark'] {
	--clr-scrollbar-thumb:       var(--clr-neutral-600);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track:       var(--clr-neutral-900);
}
```

**Wider scrollbar:**

```scss
&::-webkit-scrollbar {
	width: 0.75rem;
}
```

**Scoped to specific container:**

```scss
.sidebar {
	&::-webkit-scrollbar-thumb {
		background-color: var(--clr-primary-500);
	}
}
```