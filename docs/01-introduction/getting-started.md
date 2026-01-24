## 🚀 Getting started

Get up and running with the SCSS Style System in minutes.

<br>

### Prerequisites

Before you begin, make sure you have:

- **Node.js** and **npm** installed
- **Basic SCSS/Sass knowledge** - Understanding of variables, mixins, and imports
- **A project** where you want to use the system

---

### Step 1: Install Sass

Install Sass as a dev dependency in your project:

```bash
npm install --save-dev sass
```

**Verify installation:**

```bash
npx sass --version
# Output: 1.xx.x compiled with dart2js 2.xx.x
```

---

### Step 2: Add system to your project

#### Option A: Download and copy

1. Download the latest release
2. Copy the `styles/` folder to your project root:

```
your-project/
├── node_modules/
├── src/
└── styles/              ← Copy this entire folder
    ├── tokens/
    ├── core/
    ├── base/
    ├── themes/
    └── main.scss
```

#### Option B: Clone repository

```bash
git clone https://github.com/yourusername/scss-style-system.git
cp -r scss-style-system/styles ./your-project/styles
```

---

### Step 3: Compile styles

#### One-time compilation

```bash
sass styles/main.scss dist/styles.css
```

This compiles the SCSS to CSS and places it in `dist/styles.css`.

#### Watch mode (recommended for development)

```bash
sass --watch styles/main.scss:dist/styles.css
```

Sass will now watch for changes and automatically recompile:

```
Compiled styles/main.scss to dist/styles.css.
Sass is watching for changes. Press Ctrl-C to stop.
```

#### Add to package.json scripts

For convenience, add compilation scripts to your `package.json`:

```json
{
  "scripts": {
    "build:css": "sass styles/main.scss dist/styles.css",
    "watch:css": "sass --watch styles/main.scss:dist/styles.css",
    "dev": "npm run watch:css"
  }
}
```

**Run scripts:**

```bash
npm run build:css    # Build once
npm run watch:css    # Watch mode
npm run dev          # Start development
```

---

### Step 4: Link compiled CSS

#### In HTML

Add the compiled CSS to your HTML file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My App</title>
    
    <!-- Link compiled CSS -->
    <link rel="stylesheet" href="/dist/styles.css">
</head>
<body>
    <h1>Hello World!</h1>
    <p>CSS variables are ready!</p>
</body>
</html>
```

#### In JavaScript/React

```jsx
// App.jsx
import './dist/styles.css';

function App() {
    return <h1>Hello World!</h1>;
}
```

---

### Step 5: Use CSS variables

Now you can use the generated CSS variables in your styles!

#### Example 1: Simple button

```html
<button class="btn">Click me</button>
```

```css
.btn {
    /* Use generated CSS variables */
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    color: var(--clr-neutral-100);
    border: none;
    border-radius: var(--radius-md);
    font-weight: var(--fw-bold);
    cursor: pointer;
    transition: background var(--dur-normal) var(--ease-ease-out);
}

.btn:hover {
    background: var(--clr-primary-600);
}
```

#### Example 2: Card component

```html
<div class="card">
    <h2 class="card-title">Welcome</h2>
    <p class="card-text">Start using the system!</p>
</div>
```

```css
.card {
    padding: var(--sp-6);
    background: var(--clr-secondary-100);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-md);
}

.card-title {
    color: var(--clr-primary-600);
    font-size: var(--fs-h2);
    font-weight: var(--fw-bold);
    margin-bottom: var(--sp-4);
}

.card-text {
    color: var(--clr-neutral-700);
    line-height: 1.6;
}
```

#### Example 3: With CSS Modules

```jsx
// Button.tsx
import styles from './Button.module.scss';

export function Button({ children }) {
    return <button className={styles.button}>{children}</button>;
}
```

```scss
// Button.module.scss
.button {
    padding: var(--sp-4);
    background: var(--clr-primary-500);
    border-radius: var(--radius-md);
    
    &:hover {
        background: var(--clr-primary-600);
    }
}
```

---

### Step 6: Customize (optional)

The system is ready to use with default values, but you can customize everything to match your design.

#### Change brand color

Open `styles/tokens/_colors.scss` and modify the hue parameter:

```scss
// Change from purple (270deg) to blue (200deg)
$primary-hue: 200deg !default;
```

**Save and recompile:**

```bash
npm run build:css
```

All primary colors (100-900) will now be blue! 🎉

#### Adjust typography scale

Open `styles/tokens/_typography.scss`:

```scss
// Make text smaller
$base-font-size: 14px !default;  // Was: 16px
```

All font sizes scale down proportionally.

#### Tighter spacing

Open `styles/tokens/_spacing.scss`:

```scss
// More compact spacing
$base-spacing: 4px !default;  // Was: 8px
```

Entire spacing scale becomes tighter (4px, 8px, 12px...).

See [Customizing](../06-usage/customizing.md) for complete customization guide.

---

### Verify everything works

After compilation, check that CSS variables are generated:

1. **Open `dist/styles.css`** in your editor
2. **Search for** `--clr-primary-500`
3. **You should see:**

```css
:root {
    --clr-primary-100: oklch(95% 0.06 270deg);
    --clr-primary-500: oklch(60% 0.2 270deg);
    --clr-primary-900: oklch(12% 0.11 270deg);
    /* ... many more variables ... */
}
```

If you see these variables, everything is working correctly! ✅

---

### Available CSS variables

After compilation, you'll have access to these variables:

#### Colors

```css
--clr-primary-100 ... --clr-primary-900
--clr-secondary-100 ... --clr-secondary-900
--clr-neutral-100 ... --clr-neutral-900
--clr-success-bg, --clr-success-text, --clr-success-solid
--clr-warning-bg, --clr-warning-text, --clr-warning-solid
--clr-danger-bg, --clr-danger-text, --clr-danger-solid
--clr-info-bg, --clr-info-text, --clr-info-solid
```

#### Typography

```css
--ff-primary, --ff-accent, --ff-system
--fw-light, --fw-regular, --fw-medium, --fw-bold, --fw-extra-bold
--fs-default, --fs-h1, --fs-h2, --fs-h3, --fs-h4, --fs-h5, --fs-h6
```

#### Spacing (in rem)

```css
--sp-0, --sp-1, --sp-2, --sp-3, --sp-4, --sp-5, --sp-6, --sp-7, --sp-8
```

#### Borders

```css
--radius-none, --radius-xs, --radius-sm, --radius-md, --radius-lg, --radius-xl, --radius-pill, --radius-full
--stroke-thin, --stroke-normal, --stroke-thick
```

#### Shadows

```css
--shadow-xs, --shadow-sm, --shadow-md, --shadow-lg, --shadow-xl, --shadow-inset
```

#### Animations

```css
--dur-instant, --dur-fast, --dur-normal, --dur-slow, --dur-slower
--ease-linear, --ease-ease-in, --ease-ease-out, --ease-ease-in-out, --ease-bounce
--delay-none, --delay-short, --delay-medium, --delay-long
```

#### Z-index

```css
--z-base, --z-content, --z-header, --z-sidebar, --z-footer
--z-dropdown, --z-sticky, --z-modal, --z-tooltip, --z-notification
```

See individual token documentation for complete lists.

---

### Troubleshooting

#### Styles not compiling?

**Check Sass installation:**

```bash
npx sass --version
```

If not installed, run `npm install --save-dev sass`.

**Check file paths:**

Make sure `styles/main.scss` exists and imports are correct.

#### Variables not working in browser?

**Check CSS is linked:**

Open browser DevTools → Network tab → Look for `styles.css` → Should be 200 OK

**Check browser support:**

CSS custom properties work in all modern browsers. IE11 is not supported.

#### Changes not updating?

**Use watch mode:**

```bash
sass --watch styles/main.scss:dist/styles.css
```

**Hard refresh browser:**

- Windows/Linux: `Ctrl + Shift + R`
- Mac: `Cmd + Shift + R`

**Clear Sass cache:**

```bash
sass styles/main.scss dist/styles.css --no-cache
```

---

### Next steps

Now that you're set up, explore these topics:

#### Essential reading

- [Folder structure](folder-structure.md) - Understand the organization
- [Architecture](architecture.md) - How the system works
- [Customizing](../06-usage/customizing.md) - Make it your own

#### Token documentation

- [Colors](../02-tokens/colors.md) - OKLCH color system with hue parameters
- [Typography](../02-tokens/typography.md) - Font system
- [Spacing](../02-tokens/spacing.md) - 8px grid system
- [Borders](../02-tokens/borders.md) - Radius and stroke widths

#### Theming

- [Basic themes](../05-themes/basic-themes.md) - Light/dark mode setup
- [Custom theme creation](../05-themes/custom-theme.md) - Build your own theme
- [Theme switching](../05-themes/switching.md) - Toggle themes with JavaScript

#### Best practices

- [Best practices](../06-usage/best-practices.md) - Recommended patterns
- [Responsive design](../06-usage/responsive-design.md) - Mobile-first approach

---

### Need help?

- 📚 **Full documentation** - Browse the docs folder
- 🐛 **Found a bug?** - Open an issue
- 💬 **Have a question?** - Start a discussion
- 🤝 **Want to contribute?** - See contributing guidelines

**Happy coding!** 🚀