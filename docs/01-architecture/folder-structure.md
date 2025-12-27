## 📂 **Folder structure**

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
│    ├── 📄 _variables.scss
│    └── 📄 _index.scss
│
├── 📁 core
│    ├── 📁 functions
│    │    ├── 📄 _px-to-rem.scss
│    │    └── 📄 _index.scss
│    │
│    ├── 📁 mixins
│    │    ├── 📄 _breakpoint.scss
│    │    ├── 📄 _generate-theme.scss
│    │    ├── 📄 _generate-tokens.scss
│    │    ├── 📄 _validate-theme.scss
│    │    └── 📄 _index.scss
│    │
│    └── 📄 _index.scss
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
│    ├── 📄 _z-index.scss
│    └── 📄 _index.scss
│
└── 📄 main.scss
```
