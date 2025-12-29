## 🌓 Basic themes handling

The system includes `light` and `dark` themes by default.

> 💡 To customize theme elements you need to edit [theme schema](theme-schema.md)

---

### 🌞 Light Theme (\_light.scss)

```scss
// themes/_light.scss

$light: (
	text: (
		_: var(--clr-neutral-900),
		accent: var(--clr-primary-500)
	),
	selection: (
		bg: (
			_: var(--clr-primary-200)
		),
		text: (
			_: var(--clr-primary-900)
		)
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-400),
			hover: var(--clr-neutral-500)
		),
		track: (
			_: var(--clr-neutral-100)
		)
	),
	header: (
		bg: (
			_: var(--clr-secondary-100)
		),
		text: (
			_: var(--clr-neutral-900)
		)
	),
	main: (
		bg: (
			_: var(--clr-secondary-100),
			hover: var(--clr-secondary-200)
		),
		text: (
			_: var(--clr-neutral-800)
		)
	),
	footer: (
		bg: (
			_: var(--clr-secondary-200)
		),
		text: (
			_: var(--clr-neutral-700)
		)
	)
);
```

---

### 🌑 Dark Theme (\_dark.scss)

```scss
// themes/_dark.scss

$dark: (
	text: (
		_: var(--clr-neutral-100),
		accent: var(--clr-primary-400)
	),
	selection: (
		bg: (
			_: var(--clr-primary-700)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	),
	scrollbar: (
		thumb: (
			_: var(--clr-neutral-600),
			hover: var(--clr-neutral-500)
		),
		track: (
			_: var(--clr-neutral-900)
		)
	),
	header: (
		bg: (
			_: var(--clr-neutral-900)
		),
		text: (
			_: var(--clr-neutral-100)
		)
	),
	main: (
		bg: (
			_: var(--clr-neutral-800),
			hover: var(--clr-neutral-700)
		),
		text: (
			_: var(--clr-neutral-200)
		)
	),
	footer: (
		bg: (
			_: var(--clr-neutral-900)
		),
		text: (
			_: var(--clr-neutral-400)
		)
	)
);
```
