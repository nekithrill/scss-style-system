## 📂 Folder structure

- **/base** - fonts connection, global styles, basic styles reset, custom scrollbar, selection styling, utility classes, variables generation;
- **/core** - mixins and functions;
- **/themes** - theme schema, theme modules and theme application;
- **/tokens** - core values: animation (duration, easing, etc.), breakpoints (media queries sizes), spacing, radius, shadows, typography, z-indexes.

```md
📁 styles
├── 📁 base
│    ├── 📄 _fonts.scss
│    ├── 📄 _globals.scss
│    ├── 📄 _reset.scss
│    ├── 📄 _scrollbar.scss
│    ├── 📄 _selection.scss
│    ├── 📄 _utilities.scss
│    └── 📄 _variables.scss
│
├── 📁 core
│    ├── 📁 functions
│    │    └── 📄 _px-to-rem.scss
│    │
│    └── 📁 mixins
│         ├── 📄 _breakpoint.scss
│         ├── 📄 _generate-tokens.scss
│         ├── 📄 _generate-theme.scss
│         └── 📄 _validate-theme.scss
│
├── 📁 themes
│    ├── 📄 _apply.scss
│    ├── 📄 _dark.scss
│    ├── 📄 _light.scss
│    └── 📄 _schema.scss
│
├── 📁 tokens
│    ├── 📄 _animations.scss
│    ├── 📄 _breakpoints.scss
│    ├── 📄 _colors.scss
│    ├── 📄 _radius.scss
│    ├── 📄 _shadow.scss
│    ├── 📄 _spacing.scss
│    ├── 📄 _typography.scss
│    └── 📄 _z-index.scss
│
└── 📄 main.scss
```

> 💡 **Customization tips:**
> - **Optional files:** You can safely remove `_scrollbar.scss`, `_selection.scss`, or `_dark.scss` if not needed. Just remember to remove their `@use` imports from `main.scss`.
> - **Token files:** All files in `/tokens` are meant to be customized to match your project's design system.
> - **Core files:** Files in `/core` contain the system logic - modify with caution or extend functionality as needed.

> 💡 **File removal checklist:**
> 1. Delete the file from its folder
> 2. Remove the corresponding `@use` statement from `main.scss`
> 3. Remove any related variable usage from your codebase
