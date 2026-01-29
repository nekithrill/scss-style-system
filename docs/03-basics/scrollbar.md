> **📁 Location:** `styles/base/_scrollbar.scss`
> **🧭 Scope:** Custom scrollbar appearance
> **📦 Type:** Basic

# 📜 Custom scrollbar

Styled scrollbars for Firefox and Webkit browsers using theme colors.

## 🧠 How it works

Custom scrollbar styles that adapt to your theme:

- **Firefox:** Uses `scrollbar-width` and `scrollbar-color` (modern CSS scrollbar styling).
- **Webkit:** Uses `::-webkit-scrollbar` pseudo-elements for Chrome/Safari/Edge.

**Theme integration:** Uses semantic color variables (`--clr-scrollbar-thumb`, `--clr-scrollbar-track`) that themes define, ensuring scrollbars match light/dark mode.

**Feature detection:** Uses `@supports` to apply Firefox styles only where supported, preventing conflicts.

## 🚀 Usage

```scss
// Scrollbars are styled automatically
// No additional code needed

// Theme must provide these variables:
[data-theme='dark'] {
	--clr-scrollbar-thumb: var(--clr-neutral-400);
	--clr-scrollbar-thumb-hover: var(--clr-neutral-500);
	--clr-scrollbar-track: var(--clr-neutral-100);
}
```

## ⚙️ Configuration

```scss
// base/_scrollbar.scss

* {
	// Firefox
	@supports (scrollbar-width: thin) and (not selector(::-webkit-scrollbar)) {
		scrollbar-width: thin;
		scrollbar-color: var(--clr-scrollbar-thumb) var(--clr-scrollbar-track);
	}

	// Webkit (Chrome, Safari, Edge)
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

## 🔧 Customization

```scss
// Wider scrollbar
html::-webkit-scrollbar {
	width: 1rem;
}

// Rounded scrollbar thumb
html::-webkit-scrollbar-thumb {
	background-color: var(--clr-scrollbar-thumb);
	border-radius: var(--rd-pill);
}

// Custom scrollbar for specific element
.scrollable-container {
	&::-webkit-scrollbar {
		width: 0.5rem;
	}
	
	&::-webkit-scrollbar-thumb {
		background-color: var(--clr-primary-500);
	}
}
```

## ✔️ Best practices

- ✅ **Do:** Define scrollbar colors in themes
- ✅ **Do:** Test in both Firefox and Chrome
- ✅ **Do:** Keep scrollbar width reasonable (0.5-1rem)
- ❌ **Don't:** Hide scrollbars entirely (bad for UX)
- ❌ **Don't:** Use bright colors (distracting)
- ❌ **Don't:** Forget hover states

## ❌ Common mistakes

**Missing theme variables:**

```scss
// ❌ Bad: Scrollbar breaks without theme variables
html::-webkit-scrollbar-thumb {
	background-color: var(--clr-scrollbar-thumb);  // Undefined!
}

// ✅ Good: Theme provides variables
[data-theme='dark'] {
	--clr-scrollbar-thumb: var(--clr-neutral-400);
	--clr-scrollbar-track: var(--clr-neutral-100);
}
```