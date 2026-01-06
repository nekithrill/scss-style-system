## ✨ Improvements

> 💡 This system is designed to be practical and straightforward. Before considering any improvements, it's recommended to use the current setup in real projects and identify actual pain points. The improvements listed below are potential enhancements that may be implemented if they prove necessary through real-world usage.

<br>

### Template to dependency migration

**Current state:**  
The system is designed as a **starter template** - users copy files to their project and customize as needed. This approach prioritizes simplicity and full control over the codebase.

**Potential improvement:**  
If demand grows and the system proves stable across multiple projects, it may be packaged as an **npm dependency** for easier distribution and updates.

**Planned features:**

- **Centralized configuration:** Single config file for all customization
- **Module system:** Import only what you need
- **Version management:** Semantic versioning and changelogs
- **Update mechanism:** Get bug fixes and improvements without manual file copying
- **Configuration API:** Override defaults without modifying source files

**Example API (proposed):**
```scss
// Install as dependency
npm install @yourname/scss-system

// Configure via Sass modules
@use '@yourname/scss-system' with (
	$base-font-size: 18,
	$primary-color: #6366f1,
	$breakpoints: (
		sm: 640px,
		md: 768px,
		lg: 1024px
	)
);

// Use tokens in your components
.card {
	padding: var(--sp-4);
	background: var(--theme-card-bg);
}
```

**Migration requirements:**

Before transitioning from template to dependency, the following would need to be implemented:

- **Centralized config system:** All customizable values exposed through Sass module API
- **Package structure:** Proper npm package with exports, versioning, and documentation
- **Breaking changes policy:** Clear migration guides between major versions
- **Distribution strategy:** Compiled CSS option for non-Sass users
- **Documentation overhaul:** Separate docs for template vs dependency usage

**Benefits of dependency approach:**

- ✅ Easier updates (npm update instead of manual file copying)
- ✅ Version control (lock to specific version, upgrade when ready)
- ✅ Smaller git diffs (no system files in project repo)
- ✅ Centralized bug fixes (update package, not every project)

**Trade-offs to consider:**

- ⚠️ Less flexibility (can't directly edit system files)
- ⚠️ Configuration complexity (must expose all customization points)
- ⚠️ Breaking changes (major version updates require migration)
- ⚠️ Learning curve (users need to learn configuration API)

**When to implement:**  
Only after the template approach has been validated through real-world usage in multiple projects, and if user feedback indicates strong demand for a dependency-based distribution model. The template approach will remain available for users who prefer maximum flexibility.

> 💡 **Current recommendation:** Use the template approach (copy files). It's simpler, more flexible, and you own the code. Consider the dependency approach only for large teams managing multiple projects with the same design system.

<br>

---

<br>

### Color system automation

**Current state:**  
Color management is fully manual. Each color shade must be defined explicitly in the tokens file.

**Potential improvement:**  
If manual color management becomes difficult to maintain across multiple projects, implement automatic palette generation from base colors.

**Planned features:**

- Generate full palettes (100-900 shades) from base colors
- Support any input color format (HEX, RGB, HSL, OKLCH)
- Output in any desired format (preferably OKLCH for consistency)
- Automatic lightness and chroma calculations for perceptually uniform scales

**Example API:**
```scss
// Proposed future API
@use 'core/functions/generate-palette' as *;

$primary: generate-palette(
	$base: #6366f1,      // Input: any format
	$output: 'oklch',    // Output: OKLCH
	$shades: 9           // Generate 100-900
);

// Result:
// $primary: (
//   100: oklch(95% 0.06 270deg),
//   200: oklch(85% 0.1 270deg),
//   ...
//   900: oklch(12% 0.11 270deg)
// )
```

**When to implement:**  
After testing the current system on multiple projects, if color maintenance becomes a pain point.

<br>

---

<br>

### Token system improvement

**Current state:**  
The token system works as designed but may have limitations that only become apparent through real-world usage.

**Potential improvements:**  
Based on feedback and testing across different projects, the token system may need:

- **Automation:** Auto-generate related tokens (e.g., hover states from base colors)
- **Simplification:** Reduce boilerplate or complexity if certain patterns emerge
- **Restructuring:** Reorganize token categories if the current structure proves inflexible
- **Extension:** Add new token categories based on common project needs

**When to implement:**  
After identifying specific pain points through practical use. Changes will be driven by actual needs, not speculation.

<br>

---

<br>

### Base styles improvement

**Current state:**  
Base styles provide essential defaults for global elements (typography, links, etc.).

**Potential improvements:**  
If the current base styles have gaps, errors, or don't cover common use cases discovered during testing:

- Fix any styling inconsistencies or bugs
- Add missing element defaults (forms, tables, etc.)
- Improve accessibility features
- Better integration with design tokens
- More comprehensive typography baseline

**When to implement:**  
After real-world testing reveals specific issues or missing features in base styles.

<br>

---

<br>

### Reset improvements

**Current state:**  
The reset provides a minimal foundation by removing browser inconsistencies.

**Potential improvements:**  
If the current reset doesn't cover important edge cases or resets too much:

- **Optimize coverage:** Add resets for elements that show cross-browser inconsistencies
- **Reduce over-resetting:** Preserve useful browser defaults where appropriate
- **Modern features:** Add support for newer CSS features (focus-visible, prefers-reduced-motion)
- **Accessibility:** Improve focus management and screen reader support
- **Form elements:** Better normalization of inputs, buttons, selects

**Example additions:**
```scss
// Potential improvements
@media (prefers-reduced-motion: reduce) {
	*,
	*::before,
	*::after {
		animation-duration: 0.01ms !important;
		transition-duration: 0.01ms !important;
	}
}

:focus-visible {
	outline: 2px solid var(--clr-primary-500);
	outline-offset: 2px;
}
```

**When to implement:**  
After identifying specific browser inconsistencies or accessibility issues through testing.