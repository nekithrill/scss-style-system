## 🧱 Modularity

This system is designed to be **modular** by default.
You are encouraged to remove anything you don't need.
Nothing here is mandatory - everything is opt-in.

---

### What can be removed?

All imports are centralized in `main.scss`, making it easy to remove any module you don't need.

> ⚠️ **Note:** Order of imports matters!
> Keep tokens → core → base → themes sequence.

**To remove a module:**

1. Comment out its `@use` statement in `main.scss`
2. Test your build for errors
3. Delete the file if it's no longer needed anywhere

**Example:**

```scss
// main.scss

/// 1. Tokens import
@use './tokens/colors' as *;
@use './tokens/spacing' as *;
// @use './tokens/shadows' as *;     ← Not using shadows? Comment out!
// @use './tokens/animations' as *;  ← No animations? Comment out!

// 2. Core import
@use './core/mixins/breakpoint' as *;
// @use './core/mixins/generate-theme' as *;  ← Single theme? Remove this!

// 3. Basics import
@use './base/reset' as *;
// @use './base/scrollbar' as *;  ← Default scrollbar? Comment out!

// 4. Theming
@use './themes/apply' as *;  ← Single theme project? Comment out!
```

📝 For complete file structure, see [Folder Structure Guide](folder-structure.md)

---

#### Removing token groups

If you don't need a specific token group (like shadows or animations):

**Step 1:** Remove the `@use` import from `main.scss`

```scss
// main.scss
// @use './tokens/shadows' as *;  ← Comment out
```

**Step 2:** Remove its configuration from `$base-tokens` in `/base/_variables.scss`

```scss
// base/_variables.scss

$base-tokens: (
	colors: (
		map: $all-colors,
		prefix: 'clr'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	),
	// shadows: (               ← Remove this entire block
	// 	map: $shadows,
	// 	prefix: 'shd',
	// 	transform: 'rem'
	 // ),
);
```

---

#### Removing color palettes

Remove unused semantic colors from `/tokens/_colors.scss`:

```scss
// tokens/_colors.scss

$all-colors: (
	'primary': $primary,
	'neutral': $neutral,
	// 'secondary': $secondary,  ← Remove if not using
	// 'success': $success,      ← Remove semantic colors
	// 'warning': $warning,      ← if not building alerts/forms
	// 'danger': $danger,
	 // 'info': $info,
);
```

---

#### Removing theme system

For single-theme projects, you can remove the entire theming system:

**Step 1:** Comment out theme imports in `main.scss`

```scss
// main.scss
// @use './themes/apply' as *;  ← Remove themes
```

**Step 2:** Remove theme-related mixins

```scss
// main.scss
// @use './core/mixins/generate-theme' as *;  ← Not needed
// @use './core/mixins/validate-theme' as *;  ← Not needed
```

**Step 3:** (Optional) Delete the `/themes` folder entirely

**Result:** Use color tokens directly in your components instead of theme variables.

---

#### Removing individual themes

If you want theming but only need one theme (e.g., light only):

```scss
// themes/_apply.scss

@use '../themes/light' as *;
// @use '../themes/dark' as *;  ← Remove dark theme

@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);
// @include validate-theme($dark, ...);  ← Remove validation

:root {
	@include generate-theme($light);
}

// [data-theme='dark'] {          ← Remove dark theme generation
// 	@include generate-theme($dark);
// }
```

---

#### Removing base styles

You can remove any base styles you don't need:

```scss
// main.scss

@use './base/fonts' as *;
@use './base/reset' as *; // ← Remove if using external reset
@use './base/variables' as *;
@use './base/globals' as *; // ← Remove if not using global styles
@use './base/scrollbar' as *; // ← Remove custom scrollbar
@use './base/selection' as *; // ← Remove custom selection
@use './base/utilities' as *; // ← Remove utility classes
```

---

### Common removal scenarios

#### Scenario 1: Simple landing page (no themes, minimal tokens)

```scss
// main.scss

// Keep only essentials
@use './tokens/colors' as *;
@use './tokens/spacing' as *;
@use './tokens/typography' as *;
// Remove: shadows, animations, z-index, radius

@use './base/variables';
@use './base/reset';
// Remove: themes, scrollbar, selection, globals

// No themes needed - use tokens directly in components
```

#### Scenario 2: React app with CSS-in-JS (tokens only)

```scss
// main.scss

// Import only needed tokens
@use './tokens/colors' as *;
@use './tokens/spacing' as *;
@use './tokens/typography' as *;
// Add more as needed: radius, shadows, breakpoints, etc.

@use './core/mixins/generate-tokens' as *;
@use './base/variables' as *; // Generates CSS variables

// Remove: base/reset, base/globals, themes

// Usage in styled-components:
// const Button = styled.button`
//   color: var(--clr-primary-500);
//   padding: var(--sp-2);
//   font-family: var(--ff-primary);
// `;
```

#### Scenario 3: Prototype (only colors and spacing)

```scss
// main.scss - absolute minimum

@use './tokens/colors' as *;
@use './tokens/spacing' as *;
@use './core/mixins/generate-tokens' as *;

$base-tokens: (
	colors: (
		map: $all-colors,
		prefix: 'clr'
	),
	spacing: (
		map: $spacing,
		prefix: 'sp',
		transform: 'rem'
	)
);

:root {
	@include generate-tokens($base-tokens);
}

// That's it! No themes, no extra mixins, no base styles
```

---

### How to safely remove modules

**Step 1: Identify unused features**

- Check if you're using themes → If not, remove theme system
- Check which token groups are used → Remove unused ones
- Check which mixins are imported → Remove unused ones

**Step 2: Comment out imports**

```scss
// Start by commenting out, not deleting
// @use './themes/apply' as *;  ← Comment first to test
```

**Step 3: Test your build**

- Run your build process
- Check for Sass errors
- Fix any missing dependencies

**Step 4: Delete unused files**

```bash
# Once you're sure, delete the unused files

# Example (adjust paths to match your project):
rm -rf src/styles/themes/              # Remove entire themes folder
rm src/styles/tokens/_shadows.scss     # Remove specific token file

# Or manually delete through your file explorer/IDE
```

---

### Benefits of removing unused modules

**Smaller output size:**

- Fewer generated variables
- Reduces CSS bundle size
- Faster load times

**Simpler maintenance:**

- Less code to understand and maintain
- Fewer files to manage
- Easier onboarding for new developers

**Clearer intent:**

- Codebase reflects actual project needs
- No unused or misleading artifacts
- Cleaner and more predictable structure

---

### When NOT to remove modules

**Keep modules if:**

- You might need them in the future (early project phase)
- They're part of a shared design system
- Removal saves minimal space (<5% of output)
- Team members might need them for their work

**Remember:** You can always add modules back later. Start minimal, add complexity only when needed.

---

### Quick reference: What to keep vs remove

| Module               | Keep if...                 | Remove if...                |
| -------------------- | -------------------------- | --------------------------- |
| **Themes**           | Multiple themes are needed | Single-theme project        |
| **Color palettes**   | Using semantic colors      | Only primary/neutral colors |
| **Shadows**          | Cards, modals, dropdowns   | Flat design                 |
| **Animations**       | Interactive UI             | Static content              |
| **Z-index tokens**   | Overlays and modals        | Simple layouts              |
| **Border radius**    | Rounded UI elements        | Sharp/minimal design        |
| **Breakpoint mixin** | Responsive layouts         | Mobile-only / desktop-only  |
| **Base reset**       | Browser normalization      | External reset in use       |
| **Custom scrollbar** | Branded UI experience      | Default browser scrollbar   |
| **Selection styles** | Branded experience         | Default selection behavior  |

---

### Key Principles

#### Flexibility over dogma

- Use what makes sense for your project
- There is no single “correct” setup
- Start simple and introduce complexity only when needed

#### Modularity

- Every feature is optional
- Remove unused tokens, themes, or mixins
- Keep only what provides real value

#### Progressive enhancement

- Start with tokens only
- Add themes when multiple variants are required
- Scale the system up or down as your project evolves

#### No lock-in

- CSS variables can be overridden or extended
- Tokens can be used independently of the system
- Easy to migrate away or integrate elsewhere

---

**Philosophy:** The system provides everything you might need, but keep only what you actually use. Less is more.
