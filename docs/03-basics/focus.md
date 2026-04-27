> 📁 **Location:** `styles/base/_focus.scss`
> 🎯 **Scope:** Focus visibility and keyboard navigation
> 🏷️ **Type:** Basic

# ⌨️ Focus styles

Focus rings visible only during keyboard navigation. Uses `:focus-visible` to hide outlines for mouse and touch users while keeping them for keyboard users.

## 🧠 How it works

- **Keyboard navigation** — browser adds `:focus-visible`, outline appears.
- **Mouse / touch** — browser adds only `:focus`, outline is hidden.

This keeps the interface clean for pointer users while maintaining full accessibility for keyboard users.

## ⚙️ Configuration

```scss
// styles/base/_focus.scss

input:focus-visible,
textarea:focus-visible,
select:focus-visible,
button:focus-visible,
a:focus-visible,
[role='button']:focus-visible,
[tabindex]:focus-visible {
	outline: var(--bw-normal, 2px) solid var(--clr-focus, red);
}

input:focus:not(:focus-visible),
textarea:focus:not(:focus-visible),
select:focus:not(:focus-visible),
button:focus:not(:focus-visible),
a:focus:not(:focus-visible),
[role='button']:focus:not(:focus-visible),
[tabindex]:focus:not(:focus-visible) {
	outline: none;
}
```

`--clr-focus` is defined in themes. Fallback `red` is intentionally obvious — replace it in your theme.

## 🔧 Customization

**Box-shadow instead of outline:**

```scss
button:focus-visible {
	outline: none;
	box-shadow: 0 0 0 var(--bw-normal, 2px) var(--clr-focus, red);
}
```

**Per-element styles:**

```scss
input:focus-visible {
	outline: var(--bw-normal) solid var(--clr-primary-500);
	outline-offset: 2px;
}
```

**Define focus color in theme:**

```scss
// themes/_light.scss
:root {
	--clr-focus: var(--clr-primary-500);
}

// themes/_dark.scss
[data-theme='dark'] {
	--clr-focus: var(--clr-primary-300);
}
```