> 📁 **Location:** `styles/base/_fonts.scss`
> 🎯 **Scope:** Custom font loading
> 🏷️ **Type:** Basic

# 🔤 Font loading

`@font-face` declarations for loading custom web fonts. The file ships as a commented-out template — uncomment and update paths to activate.

## ⚙️ Configuration

```scss
// styles/base/_fonts.scss

// ⚠️ Update paths and font-family to match your font files

// @font-face {
// 	font-family: 'YourFont';
// 	src: url('../fonts/YourFont.woff2') format('woff2');
// 	font-weight: 400;
// 	font-style: normal;
// 	font-display: swap;
// }
```

## 🔧 Customization

**Load multiple weights:**

```scss
@font-face {
	font-family: 'Inter';
	src: url('/fonts/Inter-Regular.woff2') format('woff2');
	font-weight: 400;
	font-style: normal;
	font-display: swap;
}

@font-face {
	font-family: 'Inter';
	src: url('/fonts/Inter-Bold.woff2') format('woff2');
	font-weight: 700;
	font-style: normal;
	font-display: swap;
}
```

**Variable font:**

```scss
@font-face {
	font-family: 'Inter';
	src: url('/fonts/Inter-Variable.woff2') format('woff2');
	font-weight: 100 900;
	font-style: normal;
	font-display: swap;
}
```

After loading, update font families in `tokens/_typography.scss`:

```scss
$font-families: (
	primary: ('Inter', system-ui, sans-serif),
	// ...
) !default;
```

**Preload critical fonts in HTML:**

```html
<link rel="preload" href="/fonts/Inter-Regular.woff2" as="font" type="font/woff2" crossorigin>
```