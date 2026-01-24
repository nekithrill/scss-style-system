> **📁 Location:** `styles/base/_selection.scss`
> **📦 Type:** Basic

## 🖱️ Text selection

Custom styling for text selection highlight using theme colors.

<br>

### 🧠 How it works

The `::selection` pseudo-element styles the background and text color when users select (highlight) text with their mouse or keyboard.

**Theme integration:** Uses semantic variables (`--clr-selection-bg`, `--clr-selection-text`) that themes define, ensuring selection highlight matches your theme.

**Automatic application:** Applies to all selectable text automatically - no additional code needed.

---

### 🚀 Usage

```scss
// Selection styles apply automatically
// Theme must provide these variables:

:root {
	--clr-selection-bg: var(--clr-primary-200);
	--clr-selection-text: var(--clr-primary-900);
}

[data-theme='dark'] {
	--clr-selection-bg: var(--clr-primary-700);
	--clr-selection-text: var(--clr-neutral-100);
}
```

---

### ⚙️ Configuration

```scss
// base/_selection.scss

::selection {
	background-color: var(--clr-selection-bg);
	color: var(--clr-selection-text);
}
```

---

### 🔧 Customization

```scss
// Different selection per element
.code-block::selection {
	background-color: var(--clr-success-bg);
	color: var(--clr-success-text);
}

// Transparent selection
::selection {
	background-color: rgba(99, 102, 241, 0.3);
	color: inherit;
}
```

---

### ✔️ Best practices

- ✅ **Do:** Ensure sufficient contrast (4.5:1 for text)
- ✅ **Do:** Test selection in both themes
- ✅ **Do:** Keep selection colors subtle but visible
- ❌ **Don't:** Use same color as background (invisible)
- ❌ **Don't:** Use extremely bright colors (harsh)

---

### ❌ Common mistakes

**Low contrast:**
```scss
// ❌ Bad: Can't read selected text
[data-theme='light'] {
	--clr-selection-bg: var(--clr-neutral-200);
	--clr-selection-text: var(--clr-neutral-300);  // Too similar!
}

// ✅ Good: High contrast
[data-theme='light'] {
	--clr-selection-bg: var(--clr-primary-200);
	--clr-selection-text: var(--clr-primary-900);
}
```