## 📂 Folder structure

- `/base` - fonts connection, global styles, basic styles reset, custom scrollbar, selection styling, utility classes, variables generation;
- `/core` - mixins and functions;
- `/themes` - theme schema, theme modules and theme application;
- `/tokens` - core values: animation (duration, easing, etc.), breakpoints (media queries sizes), spacing, radius, shadows, typography, z-indexes.

```md
📁 styles
├── 📁 base
│    ├── 📄 _focus.scss
│    ├── 📄 _fonts.scss
│    ├── 📄 _globals.scss
│    ├── 📄 _reset.scss
│    ├── 📄 _scrollbar.scss
│    ├── 📄 _selection.scss
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
│    ├── 📄 _borders.scss
│    ├── 📄 _breakpoints.scss
│    ├── 📄 _colors.scss
│    ├── 📄 _shadows.scss
│    ├── 📄 _spacing.scss
│    ├── 📄 _typography.scss
│    └── 📄 _z-index.scss
│
└── 📄 main.scss
```
