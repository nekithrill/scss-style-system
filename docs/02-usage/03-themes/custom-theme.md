## 🎨✨ Custom theme creation

> 💡 To customize theme elements you need to edit [theme schema](theme-schema.md)

<br>

### Create a new theme file
```scss
// themes/_high-contrast.scss

$high-contrast: (
	selection: (
		bg: (
			_: #000000
		),
		text: (
			_: #ffffff
		)
	),
	scrollbar: (
		thumb: (
			_: #000000,
			hover: #333333
		),
		track: (
			_: #ffffff
		)
	),
	header: (
		bg: (
			_: #000000
		),
		text: (
			_: #ffffff
		)
	),
	main: (
		bg: (
			_: #ffffff,
			hover: #f0f0f0
		),
		text: (
			_: #000000
		)
	),
	footer: (
		bg: (
			_: #000000
		),
		text: (
			_: #ffffff
		)
	)
);
```

<br>

### Add to application
```scss
// themes/_apply.scss

@use 'light' as *;
@use 'dark' as *;
@use 'high-contrast' as *; // Import new theme
@use 'schema' as *;
@use '../core/mixins/generate-theme' as *;
@use '../core/mixins/validate-theme' as *;

// Validate all themes
@include validate-theme($light, $theme-required-keys, $theme-leaf-keys);
@include validate-theme($dark, $theme-required-keys, $theme-leaf-keys);
@include validate-theme(
	$high-contrast,
	$theme-required-keys,
	$theme-leaf-keys
); // Validate new theme

// Generate theme CSS
[data-theme='light'] {
	@include generate-theme($light);
}

[data-theme='dark'] {
	@include generate-theme($dark);
}

[data-theme='high-contrast'] {
	@include generate-theme($high-contrast); // Generate new theme
}
```