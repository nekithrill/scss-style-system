# 🔄 Overriding system defaults

How to override CSS variables and extend the system with your own values.

## 🧠 How overrides work

The system generates CSS variables in `:root` that can be overridden at any scope level:

- **Global override** → Override in `:root`  
- **Component override** → Override in component selector  
- **Theme override** → Override in `[data-theme='...']` selector  
- **State override** → Override in pseudo-class (`:hover`, `:focus`)

## 🌍 Global overrides

Override CSS variables globally by redefining them in `:root`:

```css
/* After system CSS is loaded */
:root {
    /* Override existing variables */
    --clr-primary-500: oklch(55% 0.25 180deg);  /* Different color */
    --sp-4: 2.5rem;                             /* Different spacing */
    --rd-md: 0.5rem;                            /* Different radius */
    
    /* Add new variables */
    --custom-padding: 1.5rem;
    --custom-color: oklch(60% 0.2 120deg);
}
```

**When to use:**

- Adjusting token values without recompiling SCSS
- Quick prototyping
- Runtime customization


## 🎨 Component-level overrides

Override variables within specific components:

```scss
.card {
    /* Use system defaults */
    padding: var(--sp-4);
    background: var(--clr-secondary-100);
    border-radius: var(--rd-md);
    
    /* Component-specific overrides */
    --sp-4: 2rem;           /* Smaller padding for cards only */
    --rd-md: 1rem;          /* Larger radius for cards only */
    
    &.card-compact {
        --sp-4: 1rem;       /* Even smaller for compact variant */
    }
}

.button {
    padding: var(--sp-2) var(--sp-4);
    
    &.button-large {
        /* Override spacing for large variant */
        --sp-2: 1rem;
        --sp-4: 2rem;
    }
}
```

**Benefits:**

- Scoped changes don't affect other components
- Easy variant creation
- No need to recompile SCSS

## 🌗 Theme overrides

Override variables per theme:

```css
[data-theme='light'] {
    --clr-text: var(--clr-neutral-900);
    --clr-main-bg: var(--clr-secondary-100);
}

[data-theme='dark'] {
    --clr-text: var(--clr-neutral-100);
    --clr-main-bg: var(--clr-neutral-800);
}

/* Custom theme with overrides */
[data-theme='high-contrast'] {
    /* Override base colors */
    --clr-primary-500: oklch(50% 0.3 270deg);  /* More vibrant */
    --clr-neutral-900: oklch(5% 0 0deg);       /* Darker black */
    --clr-neutral-100: oklch(99% 0 0deg);      /* Brighter white */
    
    /* Override semantic variables */
    --clr-text: var(--clr-neutral-900);
    --clr-main-bg: var(--clr-neutral-100);
}
```

## 🔁 State-based overrides

Override variables for hover, focus, active states:

```scss
.button {
    background: var(--clr-primary-500);
    transition: background var(--dur-fast);
    
    &:hover {
        /* Override on hover */
        --clr-primary-500: var(--clr-primary-600);
    }
    
    &:active {
        /* Override on press */
        --clr-primary-500: var(--clr-primary-700);
    }
    
    &:disabled {
        /* Override when disabled */
        --clr-primary-500: var(--clr-neutral-300);
        opacity: 0.6;
    }
}
```

## 🎯 Context-based overrides

Override variables based on parent context:

```scss
/* Default card */
.card {
    background: var(--clr-secondary-100);
    color: var(--clr-neutral-900);
}

/* Card inside sidebar */
.sidebar .card {
    /* Override for sidebar context */
    --clr-secondary-100: var(--clr-neutral-200);
}

/* Card inside modal */
.modal .card {
    /* Override for modal context */
    --clr-secondary-100: white;
    box-shadow: var(--shadow-xl);
}

/* Dark theme cards */
[data-theme='dark'] .card {
    --clr-secondary-100: var(--clr-neutral-800);
    --clr-neutral-900: var(--clr-neutral-100);
}
```

## 📱 Responsive overrides

Override variables at different breakpoints:

```scss
:root {
    --container-padding: var(--sp-6);  /* Desktop: 48px */
}

@media (max-width: 1024px) {
    :root {
        --container-padding: var(--sp-4);  /* Tablet: 32px */
    }
}

@media (max-width: 768px) {
    :root {
        --container-padding: var(--sp-3);  /* Mobile: 24px */
    }
}

/* Usage */
.container {
    padding: var(--container-padding);  /* Responsive automatically */
}
```

**With breakpoint mixin:**

```scss
@use '../core/mixins/breakpoint' as *;

.container {
    --container-padding: var(--sp-6);
    padding: var(--container-padding);
    
    @include breakpoint('lg') {
        --container-padding: var(--sp-4);
    }
    
    @include breakpoint('sm') {
        --container-padding: var(--sp-2);
    }
}
```

## 🔧 Adding new variables

Extend the system with your own CSS variables:

```css
:root {
    /* Custom layout variables */
    --header-height: 64px;
    --sidebar-width: 280px;
    --footer-height: 120px;
    
    /* Custom component variables */
    --card-padding: var(--sp-4);
    --button-height: 40px;
    --input-border-width: 2px;
    
    /* Custom animation variables */
    --slide-duration: 300ms;
    --fade-duration: 200ms;
}

/* Usage */
.header {
    height: var(--header-height);
}

.sidebar {
    width: var(--sidebar-width);
}

.card {
    padding: var(--card-padding);
}
```

## 🎯 Real-world examples

**Dashboard with custom sidebar:**
```scss
.dashboard {
    /* Custom layout variables */
    --sidebar-width: 240px;
    --header-height: 56px;
    --content-padding: var(--sp-6);
    
    display: grid;
    grid-template-areas:
        "sidebar header"
        "sidebar content";
    grid-template-columns: var(--sidebar-width) 1fr;
    grid-template-rows: var(--header-height) 1fr;
    
    @include breakpoint('md') {
        --sidebar-width: 64px;  /* Collapsed on tablet */
        --content-padding: var(--sp-4);
    }
    
    @include breakpoint('sm') {
        /* Stack on mobile */
        grid-template-areas:
            "header"
            "content";
        grid-template-columns: 1fr;
        --content-padding: var(--sp-2);
    }
}
```

**Theme-aware component:**

```scss
.alert {
    padding: var(--sp-4);
    border-radius: var(--rd-md);
    border-left: 4px solid var(--alert-color);
    background: var(--alert-bg);
    color: var(--alert-text);
    
    &.alert-info {
        --alert-color: var(--clr-info-solid);
        --alert-bg: var(--clr-info-bg);
        --alert-text: var(--clr-info-text);
    }
    
    &.alert-success {
        --alert-color: var(--clr-success-solid);
        --alert-bg: var(--clr-success-bg);
        --alert-text: var(--clr-success-text);
    }
    
    &.alert-warning {
        --alert-color: var(--clr-warning-solid);
        --alert-bg: var(--clr-warning-bg);
        --alert-text: var(--clr-warning-text);
    }
}
```

## ✔️ Best practices

- ✅ **Do:** Override in smaller scopes when possible
- ✅ **Do:** Use semantic naming for custom variables
- ✅ **Do:** Keep overrides organized by purpose
- ✅ **Do:** Document why overrides exist
- ❌ **Don't:** Override too many variables globally
- ❌ **Don't:** Create circular references
- ❌ **Don't:** Use arbitrary values (reference existing variables)

```css
/* ✅ Good: Scoped override */
.card-special {
    --clr-secondary-100: var(--clr-primary-200);
    background: var(--clr-secondary-100);
}

/* ❌ Bad: Hardcoded value */
.card-special {
    background: #e0e7ff;  /* Doesn't adapt to themes */
}

/* ✅ Good: Semantic custom variable */
:root {
    --nav-height: 64px;
    --nav-padding: var(--sp-4);
}

/* ❌ Bad: Non-semantic naming */
:root {
    --height-1: 64px;
    --padding-x: 2rem;
}
```

## ❌ Common mistakes

**Circular references:**

```css
/* ❌ Bad: Circular reference */
:root {
    --color-a: var(--color-b);
    --color-b: var(--color-a);  /* Breaks! */
}

/* ✅ Good: Clear hierarchy */
:root {
    --color-base: oklch(60% 0.2 270deg);
    --color-variant: var(--color-base);
}
```

**Specificity issues:**

```css
/* ❌ Bad: Override doesn't work due to specificity */
.card {
    background: var(--card-bg);
}

:root {
    --card-bg: white;  /* Defined after component */
}

/* ✅ Good: Define variables before components */
:root {
    --card-bg: white;
}

.card {
    background: var(--card-bg);
}
```

**Type mismatches:**

```css
/* ❌ Bad: Wrong unit type */
:root {
    --sp-4: 32;  /* Missing unit */
    --rd-md: 8;  /* Missing unit */
}

/* ✅ Good: Correct units */
:root {
    --sp-4: 2rem;
    --rd-md: 0.5rem;
}
```