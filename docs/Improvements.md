## Improvements

> 💡 This system is designed to be practical and straightforward. Before considering any improvements, it's recommended to use the current setup in real projects and identify actual pain points. The improvements listed below are potential enhancements that may be implemented if they prove necessary through real-world usage.

---

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
	$base: #6366f1,
	// Input: any format
	$output: 'oklch',
	// Output: OKLCH
	$shades: 9 // Generate 100-900
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

---

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

---

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

---

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
