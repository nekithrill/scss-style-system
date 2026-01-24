> **📁 Location:** `styles/themes/_apply.scss`
> **📦 Type:** Theme

## 🚫 Disabling themes

How to remove or disable the theme system when you don't need multiple themes.

<br>

### 🧠 How it works

The theme system is optional. If you only need a single color scheme, you can:

**Option 1: Keep one theme** - Remove theme switching but keep the structure for easy future expansion

**Option 2: Inline colors** - Remove the entire theme system and use color tokens directly in components

**Option 3: Simplified variables** - Create static CSS variables without the theme structure

**Why disable themes?** 
- Simpler codebase if multi-theme not needed
- Slightly smaller CSS output
- Fewer files to maintain
- Direct color token usage

**Trade-offs:**
- Harder to add themes later (need to refactor components)
- No system preference support
- No user theme choice

---

### 🚀 Usage

**Option 1: Single theme (recommended)**

Keep theme structure but remove switching:

```scss
// themes/_apply.scss

@use 'light' as *;  // Keep only one theme
@use 'schema' as *;
@use '../core/mixins/generate-theme' as *;
@use '../core/mixins/validate-theme' as *;

// Validate single theme
@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);

// Generate only in :root (no data-theme selector)
:root {
	@include generate-theme($light);
}

// Remove:
// [data-theme='dark'] { ... }
```

Remove theme switcher JavaScript - no longer needed.

**Option 2: Direct token usage**

Remove theme system entirely and use base tokens directly:

```scss
// components/_button.scss

// Before (with themes):
.button {
	background: var(--clr-header-bg);
	color: var(--clr-header-text);
}

// After (direct tokens):
.button {
	background: var(--clr-primary-500);
	color: var(--clr-neutral-100);
}
```

Delete theme files:
- `styles/themes/_light.scss`
- `styles/themes/_dark.scss`
- `styles/themes/_schema.scss`
- `styles/themes/_apply.scss`

**Option 3: Static variables**

Create simple CSS variables without theme structure:

```scss
// base/_colors.scss

:root {
	// Static color variables (not theme-aware)
	--color-text: var(--clr-neutral-900);
	--color-text-accent: var(--clr-primary-500);
	--color-bg: var(--clr-secondary-100);
	--color-bg-hover: var(--clr-secondary-200);
	
	// Use in components
	// No theme switching possible
}
```

---

### ⚙️ Configuration

**Before (with themes):**
```
styles/
├── themes/
│   ├── _light.scss
│   ├── _dark.scss
│   ├── _schema.scss
│   └── _apply.scss
└── main.scss

// main.scss imports:
@use 'themes/apply';
```

**After Option 1 (single theme):**
```
styles/
├── themes/
│   ├── _light.scss (keep)
│   ├── _schema.scss (keep)
│   └── _apply.scss (simplified)
└── main.scss

// _apply.scss only generates :root
```

**After Option 2 (no themes):**
```
styles/
├── base/
├── tokens/
└── main.scss

// No themes folder
// Components use tokens directly
```

**After Option 3 (static variables):**
```
styles/
├── base/
│   └── _static-colors.scss (new)
├── tokens/
└── main.scss

// Simple variable definitions
```

---

### 🔧 Migration steps

**Option 1: Single theme**

1. Edit `styles/themes/_apply.scss`:
```scss
// Remove dark theme import
// @use 'dark' as *;  ← Delete

@use 'light' as *;
@use 'schema' as *;
@use '../core/mixins/generate-theme' as *;
@use '../core/mixins/validate-theme' as *;

// Remove dark theme validation
// @include validate-theme($dark, ...);  ← Delete

@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);

:root {
	@include generate-theme($light);
}

// Remove dark theme generation
// [data-theme='dark'] { ... }  ← Delete
```

2. Remove theme switcher from HTML/JS
3. Delete `styles/themes/_dark.scss` (optional)

**Option 2: No themes**

1. Find all theme variable usages:
```bash
grep -r "var(--clr-text)" styles/
grep -r "var(--clr-header-bg)" styles/
# ... etc
```

2. Replace with direct tokens:
```scss
// Find: var(--clr-text)
// Replace with: var(--clr-neutral-900)

// Find: var(--clr-header-bg)
// Replace with: var(--clr-primary-500)
```

3. Delete `styles/themes/` folder
4. Remove theme import from `main.scss`

**Option 3: Static variables**

1. Create `styles/base/_static-colors.scss`:
```scss
:root {
	--color-text: var(--clr-neutral-900);
	--color-text-accent: var(--clr-primary-500);
	--color-bg: var(--clr-secondary-100);
	--color-bg-hover: var(--clr-secondary-200);
	--color-header-bg: var(--clr-primary-500);
	--color-header-text: var(--clr-neutral-100);
	// ... all colors you need
}
```

2. Update components:
```scss
.header {
	background: var(--color-header-bg);
	color: var(--color-header-text);
}
```

3. Delete `styles/themes/` folder
4. Import static colors in `main.scss`

---

### 🔄 Re-enabling themes later

If you disabled themes and want to add them back:

**From Option 1 (single theme):**
1. Uncomment dark theme in `_apply.scss`
2. Add theme switcher JavaScript
3. Test both themes

**From Option 2 (no themes):**
1. Recreate `styles/themes/` folder
2. Create theme files (`_light.scss`, `_dark.scss`, `_schema.scss`, `_apply.scss`)
3. Replace direct token usage with semantic theme variables
4. Add theme switcher

**From Option 3 (static variables):**
1. Convert static variables to theme structure
2. Create theme files
3. Update `_apply.scss` to generate themes
4. Add theme switcher

**Tip:** Option 1 is easiest to reverse - just uncomment code!

---

### 📊 Comparison table

| Feature | With Themes | Option 1 | Option 2 | Option 3 |
|---------|-------------|----------|----------|----------|
| Multiple themes | ✅ | ❌ | ❌ | ❌ |
| System preference | ✅ | ❌ | ❌ | ❌ |
| Easy to expand | ✅ | ✅ | ❌ | ⚠️ |
| CSS size | Medium | Small | Smallest | Small |
| Code complexity | High | Medium | Low | Medium |
| Maintenance | Medium | Low | Lowest | Low |

**Recommendations:**
- **Never need themes?** → Option 2 (simplest)
- **Might need themes?** → Option 1 (easy to expand)
- **Want structure?** → Option 3 (balanced)
- **Need themes now?** → Keep current system

---

### ✔️ Best practices

- ✅ **Do:** Choose Option 1 if you might add themes later
- ✅ **Do:** Choose Option 2 for simplest, most direct approach
- ✅ **Do:** Choose Option 3 for balance between simplicity and structure
- ✅ **Do:** Update all components consistently when migrating
- ✅ **Do:** Test thoroughly after removing theme system
- ❌ **Don't:** Mix approaches (use one method consistently)
- ❌ **Don't:** Leave unused theme files (delete what you don't use)
- ❌ **Don't:** Forget to update base styles (focus, scrollbar, selection)

```scss
// ✅ Good: Consistent approach (Option 2)
.header {
	background: var(--clr-primary-500);
	color: var(--clr-neutral-100);
}

.footer {
	background: var(--clr-neutral-800);
	color: var(--clr-neutral-200);
}

// ❌ Bad: Mixing approaches
.header {
	background: var(--clr-header-bg);  // Theme variable (removed)
	color: var(--clr-neutral-100);     // Direct token
}
```

---

### ❌ Common mistakes

**Forgetting to update base styles:**
```scss
// ❌ Bad: Scrollbar still references theme variables
// base/_scrollbar.scss
html::-webkit-scrollbar-thumb {
	background: var(--clr-scrollbar-thumb);  // Undefined after disabling themes!
}

// ✅ Good: Update to direct tokens
html::-webkit-scrollbar-thumb {
	background: var(--clr-neutral-400);
}
```

**Leaving unused imports:**
```scss
// ❌ Bad: Importing disabled themes
@use 'themes/apply';  // File still exists but not used

// ✅ Good: Remove import
// @use 'themes/apply';  ← Deleted
```

**Incomplete migration:**
```scss
// ❌ Bad: Some components still use theme variables
.button {
	background: var(--clr-header-bg);  // Theme variable
	color: var(--clr-neutral-100);     // Direct token
}

// ✅ Good: All components use same approach
.button {
	background: var(--clr-primary-500);
	color: var(--clr-neutral-100);
}
```