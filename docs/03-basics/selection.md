> 📁 **Location:** `styles/base/_selection.scss`
> 🎯 **Scope:** Text selection highlight
> 🏷️ **Type:** Basic

# 🖱️ Text selection

Custom highlight color for selected text. Uses semantic variables defined in themes.

## ⚙️ Configuration

```scss
// styles/base/_selection.scss

::selection {
	background-color: var(--clr-selection-bg, maroon);
	color: var(--clr-selection-text, red);
}
```

Fallback colors (`maroon`, `red`) are intentionally obvious — replace them in your theme.

## 🔧 Customization

**Define in theme:**

```scss
:root {
	--clr-selection-bg:   var(--clr-primary-300);
	--clr-selection-text: var(--clr-neutral-900);
}

[data-theme='dark'] {
	--clr-selection-bg:   var(--clr-primary-700);
	--clr-selection-text: var(--clr-neutral-100);
}
```

**Per-element selection:**

```scss
.code-block::selection {
	background-color: var(--clr-success-300);
}
```