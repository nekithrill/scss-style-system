> **📁 Location:** JavaScript theme switcher
> **📦 Type:** Theme

## 🔄 Theme switching

JavaScript implementation for switching between themes at runtime.

<br>

### 🧠 How it works

Theme switching works by changing the `data-theme` attribute on the `<html>` element:

**Attribute-based approach:** CSS selects themes using `[data-theme='dark']` selector. When you change this attribute, CSS automatically applies the corresponding theme variables.

**Persistence:** Store user preference in `localStorage` so the theme persists across page reloads and sessions.

**System preference detection:** Optionally detect user's OS theme preference using `prefers-color-scheme` media query and apply matching theme automatically.

**No page reload required:** Theme changes happen instantly via CSS variable reassignment.

---

### 🚀 Usage

**Basic theme switcher (HTML + JS):**

```html
<!-- Theme toggle button -->
<button id="theme-toggle">
	<span class="light-icon">🌞</span>
	<span class="dark-icon">🌙</span>
</button>

<script>
const themeToggle = document.getElementById('theme-toggle');
const html = document.documentElement;

// Get stored theme or default to 'light'
const currentTheme = localStorage.getItem('theme') || 'light';

// Apply theme on load
html.setAttribute('data-theme', currentTheme);

// Toggle theme on click
themeToggle.addEventListener('click', () => {
	const newTheme = html.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
	
	html.setAttribute('data-theme', newTheme);
	localStorage.setItem('theme', newTheme);
});
</script>
```

---

### ⚙️ Advanced examples

**With system preference detection:**

```javascript
// Get theme from localStorage or system preference
function getInitialTheme() {
	// Check localStorage first
	const storedTheme = localStorage.getItem('theme');
	if (storedTheme) {
		return storedTheme;
	}
	
	// Fall back to system preference
	const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
	return prefersDark ? 'dark' : 'light';
}

// Apply theme
const theme = getInitialTheme();
document.documentElement.setAttribute('data-theme', theme);

// Listen for system preference changes
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
	// Only auto-switch if user hasn't set preference
	if (!localStorage.getItem('theme')) {
		const newTheme = e.matches ? 'dark' : 'light';
		document.documentElement.setAttribute('data-theme', newTheme);
	}
});
```

**Multiple theme selector:**

```html
<select id="theme-selector">
	<option value="light">Light</option>
	<option value="dark">Dark</option>
	<option value="custom">Custom</option>
	<option value="high-contrast">High Contrast</option>
</select>

<script>
const themeSelector = document.getElementById('theme-selector');
const html = document.documentElement;

// Set initial value
const currentTheme = localStorage.getItem('theme') || 'light';
themeSelector.value = currentTheme;
html.setAttribute('data-theme', currentTheme);

// Handle theme change
themeSelector.addEventListener('change', (e) => {
	const theme = e.target.value;
	html.setAttribute('data-theme', theme);
	localStorage.setItem('theme', theme);
});
</script>
```

**React component:**

```jsx
import { useEffect, useState } from 'react';

function ThemeToggle() {
	const [theme, setTheme] = useState('light');
	
	// Initialize theme on mount
	useEffect(() => {
		const storedTheme = localStorage.getItem('theme') || 'light';
		setTheme(storedTheme);
		document.documentElement.setAttribute('data-theme', storedTheme);
	}, []);
	
	// Toggle theme
	const toggleTheme = () => {
		const newTheme = theme === 'light' ? 'dark' : 'light';
		setTheme(newTheme);
		document.documentElement.setAttribute('data-theme', newTheme);
		localStorage.setItem('theme', newTheme);
	};
	
	return (
		<button onClick={toggleTheme} aria-label="Toggle theme">
			{theme === 'light' ? '🌙' : '🌞'}
		</button>
	);
}
```

**With smooth transition:**

```javascript
// Add transition class to prevent flash
document.documentElement.classList.add('theme-transition');

// Change theme
function setTheme(themeName) {
	document.documentElement.setAttribute('data-theme', themeName);
	localStorage.setItem('theme', themeName);
	
	// Remove transition class after animation
	setTimeout(() => {
		document.documentElement.classList.remove('theme-transition');
	}, 300);
}

// CSS for smooth transition
```
```css
html.theme-transition,
html.theme-transition *,
html.theme-transition *::before,
html.theme-transition *::after {
	transition: background-color 0.3s ease, color 0.3s ease !important;
	transition-delay: 0s !important;
}
```

---

### 🔧 Customization

**Prevent flash of unstyled content (FOUC):**

```html
<script>
	// CRITICAL: Run before page renders
	(function() {
		const theme = localStorage.getItem('theme') || 'light';
		document.documentElement.setAttribute('data-theme', theme);
	})();
</script>
```

**Store user preference separately from auto-detection:**

```javascript
function getTheme() {
	const userPreference = localStorage.getItem('theme-preference'); // 'light', 'dark', or null
	
	if (userPreference) {
		return userPreference;
	}
	
	// Auto-detect if no preference
	const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
	return prefersDark ? 'dark' : 'light';
}

function setTheme(theme) {
	document.documentElement.setAttribute('data-theme', theme);
	localStorage.setItem('theme-preference', theme);
}

function clearThemePreference() {
	localStorage.removeItem('theme-preference');
	// Re-apply based on system preference
	const theme = getTheme();
	document.documentElement.setAttribute('data-theme', theme);
}
```

**Theme-specific icons:**

```html
<button id="theme-toggle" aria-label="Toggle theme">
	<svg class="theme-icon-light" viewBox="0 0 24 24">
		<!-- Sun icon -->
	</svg>
	<svg class="theme-icon-dark" viewBox="0 0 24 24">
		<!-- Moon icon -->
	</svg>
</button>

<style>
[data-theme='light'] .theme-icon-dark { display: none; }
[data-theme='dark'] .theme-icon-light { display: none; }
</style>
```

---

### ✔️ Best practices

- ✅ **Do:** Apply theme before page renders (prevent flash)
- ✅ **Do:** Store preference in localStorage
- ✅ **Do:** Respect system preferences when no user preference exists
- ✅ **Do:** Provide accessible toggle button (ARIA labels)
- ✅ **Do:** Show current theme state visually
- ❌ **Don't:** Force theme without user control
- ❌ **Don't:** Use transitions on initial page load (slow)
- ❌ **Don't:** Forget to sync toggle UI with current theme
- ❌ **Don't:** Apply theme changes on every page load (use cached value)

```javascript
// ✅ Good: Cached, prevents flash
const theme = localStorage.getItem('theme') || 'light';
document.documentElement.setAttribute('data-theme', theme);

// ❌ Bad: Checks system preference every time (slow)
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
document.documentElement.setAttribute('data-theme', prefersDark ? 'dark' : 'light');
```

---

### ❌ Common mistakes

**Flash of unstyled content:**
```javascript
// ❌ Bad: Theme applied after DOM loads (flash)
window.addEventListener('DOMContentLoaded', () => {
	const theme = localStorage.getItem('theme');
	document.documentElement.setAttribute('data-theme', theme);
});

// ✅ Good: Inline script in <head> (runs before render)
<script>
	const theme = localStorage.getItem('theme') || 'light';
	document.documentElement.setAttribute('data-theme', theme);
</script>
```

**Not updating toggle UI:**
```javascript
// ❌ Bad: Toggle changes theme but icon stays same
toggleBtn.addEventListener('click', () => {
	const newTheme = currentTheme === 'light' ? 'dark' : 'light';
	document.documentElement.setAttribute('data-theme', newTheme);
	// Forgot to update button icon!
});

// ✅ Good: Update UI state
toggleBtn.addEventListener('click', () => {
	const newTheme = currentTheme === 'light' ? 'dark' : 'light';
	document.documentElement.setAttribute('data-theme', newTheme);
	localStorage.setItem('theme', newTheme);
	updateToggleIcon(newTheme);  // Update UI
});
```

**Ignoring system preference:**
```javascript
// ❌ Bad: Always defaults to light
const theme = localStorage.getItem('theme') || 'light';

// ✅ Good: Check system preference as fallback
function getTheme() {
	const stored = localStorage.getItem('theme');
	if (stored) return stored;
	
	const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
	return prefersDark ? 'dark' : 'light';
}
```

---

### 🎯 Complete example

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Theme Switching Example</title>
	
	<!-- CRITICAL: Apply theme before render -->
	<script>
		(function() {
			const getTheme = () => {
				const stored = localStorage.getItem('theme');
				if (stored) return stored;
				
				const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
				return prefersDark ? 'dark' : 'light';
			};
			
			document.documentElement.setAttribute('data-theme', getTheme());
		})();
	</script>
	
	<link rel="stylesheet" href="styles/main.css">
</head>
<body>
	<header>
		<h1>My App</h1>
		<button id="theme-toggle" aria-label="Toggle dark mode">
			<span class="icon-light">☀️</span>
			<span class="icon-dark">🌙</span>
		</button>
	</header>
	
	<main>
		<p>Content goes here...</p>
	</main>
	
	<script>
		const toggle = document.getElementById('theme-toggle');
		const html = document.documentElement;
		
		// Update toggle icon based on theme
		function updateIcon() {
			const isDark = html.getAttribute('data-theme') === 'dark';
			document.querySelector('.icon-light').style.display = isDark ? 'none' : 'inline';
			document.querySelector('.icon-dark').style.display = isDark ? 'inline' : 'none';
		}
		
		// Initialize icon
		updateIcon();
		
		// Toggle theme
		toggle.addEventListener('click', () => {
			const current = html.getAttribute('data-theme');
			const newTheme = current === 'light' ? 'dark' : 'light';
			
			html.setAttribute('data-theme', newTheme);
			localStorage.setItem('theme', newTheme);
			updateIcon();
		});
		
		// Listen for system preference changes
		window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
			if (!localStorage.getItem('theme')) {
				const newTheme = e.matches ? 'dark' : 'light';
				html.setAttribute('data-theme', newTheme);
				updateIcon();
			}
		});
	</script>
</body>
</html>
```