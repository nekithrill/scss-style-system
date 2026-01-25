> **📁 Location:** `styles/tokens/_animations.scss`
> **🧭 Scope:** Motion, transitions and interaction feedback
> **📦 Type:** Token

## 🎞️ Animation tokens

Define timing parameters for consistent motion design across the project. Includes `duration`, `easing` and `delay` tokens for orchestrating smooth, predictable animations.


<br>

### 🧠 How it works

Animation tokens provide three types of timing values:

**Duration tokens (`--dur-*`)** control how long animations and transitions take. The system uses a scale from `instant` (100ms) to `slower` (700ms), optimized for different interaction speeds.

**Easing tokens (`--tf-*`)** define the timing function (acceleration curve) of animations. These cubic-bezier curves create natural motion by controlling how an animation progresses from start to finish. The prefix `tf` stands for "timing-function" (from CSS's `animation-timing-function`).

**Delay tokens (`--delay-*`)** add time offsets before animations start, useful for creating staggered effects in lists or sequential reveals.

All tokens are generated as CSS custom properties in `:root` and can be used anywhere in your styles.

---

### 🚀 Usage

```scss
// Simple transition
.button {
	transition:
		background-color var(--dur-fast) var(--tf-ease-out),
		transform var(--dur-fast) var(--tf-ease-out);

	&:hover {
		transform: scale(1.05);
	}
}

// Keyframe animation
@keyframes slideIn {
	from {
		transform: translateX(-100%);
		opacity: 0;
	}
	to {
		transform: translateX(0);
		opacity: 1;
	}
}

.menu {
	animation: slideIn var(--dur-normal) var(--tf-ease-out);
}

// Staggered list items
.list-item {
	animation: fadeIn var(--dur-fast) var(--tf-ease-out);

	&:nth-child(1) {
		animation-delay: var(--delay-none);
	}
	&:nth-child(2) {
		animation-delay: var(--delay-short);
	}
	&:nth-child(3) {
		animation-delay: calc(var(--delay-short) * 2);
	}
}
```

---

### ⚙️ Basic configuration

```scss
// tokens/_animations.scss

// Duration: animation/transition speeds
$duration: (
	instant: 100ms,  // Quick feedback (hovers, focus states)
	fast: 200ms,     // Standard interactions (buttons, toggles)
	normal: 300ms,   // Default transitions (modals, dropdowns)
	slow: 500ms,     // Complex animations (page transitions)
	slower: 700ms    // Elaborate effects (carousels, reveals)
);

// Easing: timing functions for natural motion
$easing: (
	linear: linear,                                // Constant speed
	ease-in: cubic-bezier(0.4, 0, 1, 1),           // Starts slow, ends fast
	ease-out: cubic-bezier(0, 0, 0.2, 1),          // Starts fast, ends slow
	ease-in-out: cubic-bezier(0.4, 0, 0.2, 1),     // Smooth acceleration/deceleration
	bounce: cubic-bezier(0.68, -0.55, 0.265, 1.55) // Playful bounce effect
);

// Delay: timing offsets for staggered animations
$delay: (
	none: 0ms,     // No delay
	short: 50ms,   // Minimal stagger
	medium: 100ms, // Standard stagger
	long: 200ms    // Pronounced stagger
);
```

---

### 🔧 Customization

```scss
// Adjust animation speeds (faster for snappier feel)
$duration: (
	instant: 100ms,
	fast: 150ms,    // Faster
	normal: 250ms,  // Faster
	slow: 400ms,    // Faster
	slower: 600ms   // Faster
);

// Add custom easing
$easing: (
	// ... existing values
	spring: cubic-bezier(0.175, 0.885, 0.32, 1.275), // New spring effect
	elastic: cubic-bezier(0.68, -0.6, 0.32, 1.6)     // New elastic effect
);

// Extend delay options
$delay: (
	none: 0ms,
	short: 50ms,
	medium: 100ms,
	long: 200ms,
	extra-long: 400ms // New for dramatic reveals
);
```

---

### ✔️ Best practices

**Duration:**

- Use `instant` for immediate feedback (hover states, focus rings)
- Use `fast` for standard UI interactions (button clicks, form inputs)
- Use `normal` for medium complexity (dropdowns, tooltips, modals)
- Use `slow` for elaborate transitions (page changes, large panels)

**Easing:**

- Use `ease-out` for entrances (elements appearing)
- Use `ease-in` for exits (elements disappearing)
- Use `ease-in-out` for continuous motion (carousels, sliders)
- Use `linear` for loading indicators and infinite loops

**Delay:**

- Use staggered delays for list animations (creates cascading effect)
- Keep delays short to avoid perceived lag
- Avoid delays on critical user interactions

---

### ❌ Common mistakes