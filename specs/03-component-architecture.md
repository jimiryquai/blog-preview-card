# Component Architecture: CUBE CSS & Every Layout

## Overview

This specification details the component architecture using CUBE CSS methodology combined with Every Layout patterns. The architecture prioritizes composition, maintainability, and scalability while avoiding media queries through intrinsic design principles.

## CUBE CSS Layer Structure

### 1. Composition Layer (Every Layout Patterns)

The composition layer establishes layout primitives that handle spacing, alignment, and responsive behavior intrinsically.

#### Center Pattern
```css
.center {
  --center-max-width: var(--container-max-width);
  --center-padding: var(--container-padding);
  
  max-width: var(--center-max-width);
  margin-inline: auto;
  padding-inline: var(--center-padding);
}
```
**Usage**: Centers the page content and provides consistent horizontal padding.

#### Stack Pattern
```css
.stack {
  --stack-space: var(--space-stack);
  
  display: flex;
  flex-direction: column;
}

.stack > * + * {
  margin-block-start: var(--stack-space);
}
```
**Usage**: Manages vertical spacing between card elements with consistent rhythm.

#### Cluster Pattern
```css
.cluster {
  --cluster-gap: var(--space-inline);
  --cluster-align: center;
  
  display: flex;
  flex-wrap: wrap;
  gap: var(--cluster-gap);
  align-items: var(--cluster-align);
}
```
**Usage**: Handles the author section with avatar and name.

#### Frame Pattern
```css
.frame {
  --frame-aspect-ratio: 16 / 9;
  
  position: relative;
  overflow: hidden;
  aspect-ratio: var(--frame-aspect-ratio);
}

.frame > * {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```
**Usage**: Maintains consistent aspect ratio for the article illustration.

#### Box Pattern
```css
.box {
  --box-padding: var(--space-card-padding);
  --box-background: var(--color-surface);
  --box-border-radius: var(--radius-card);
  
  padding: var(--box-padding);
  background-color: var(--box-background);
  border-radius: var(--box-border-radius);
}
```
**Usage**: Provides consistent padding and background for the card container.

### 2. Utilities Layer

Utilities provide single-purpose classes for common styling needs.

#### Color Utilities
```css
/* Text Colors */
.text-primary { color: var(--color-text-primary); }
.text-secondary { color: var(--color-text-secondary); }

/* Background Colors */
.bg-primary { background-color: var(--color-primary); }
.bg-surface { background-color: var(--color-surface); }
```

#### Typography Utilities
```css
/* Font Sizes */
.text-xs { font-size: var(--font-size-xs); }
.text-sm { font-size: var(--font-size-sm); }
.text-base { font-size: var(--font-size-base); }
.text-lg { font-size: var(--font-size-lg); }

/* Font Weights */
.font-normal { font-weight: var(--font-weight-normal); }
.font-bold { font-weight: var(--font-weight-bold); }

/* Line Heights */
.leading-tight { line-height: var(--line-height-tight); }
.leading-base { line-height: var(--line-height-base); }
```

#### Spacing Utilities
```css
/* Margin Utilities */
.mt-xs { margin-block-start: var(--space-xs); }
.mt-sm { margin-block-start: var(--space-sm); }
.mt-md { margin-block-start: var(--space-md); }

/* Padding Utilities */
.p-xs { padding: var(--space-xs); }
.p-sm { padding: var(--space-sm); }
.p-md { padding: var(--space-md); }
```

#### Layout Utilities
```css
/* Display */
.block { display: block; }
.inline-block { display: inline-block; }
.flex { display: flex; }

/* Positioning */
.relative { position: relative; }
.absolute { position: absolute; }
```

### 3. Block Layer (Component Styles)

The block layer contains component-specific styles using BEM-like naming.

#### Card Component Structure
```css
.card {
  --card-shadow: var(--shadow-card);
  --card-max-width: var(--card-max-width);
  
  max-width: var(--card-max-width);
  box-shadow: var(--card-shadow);
  overflow: hidden;
}

.card__image {
  --image-aspect-ratio: 16 / 9;
}

.card__content {
  --content-spacing: var(--space-stack);
}

.card__tag {
  --tag-background: var(--color-primary);
  --tag-color: var(--color-text-primary);
  --tag-padding-inline: var(--space-sm);
  --tag-padding-block: var(--space-xs);
  --tag-radius: var(--radius-sm);
  
  display: inline-block;
  padding-inline: var(--tag-padding-inline);
  padding-block: var(--tag-padding-block);
  background-color: var(--tag-background);
  color: var(--tag-color);
  border-radius: var(--tag-radius);
}

.card__date {
  color: var(--color-text-secondary);
}

.card__title {
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-bold);
  line-height: var(--line-height-tight);
}

.card__description {
  color: var(--color-text-secondary);
  line-height: var(--line-height-relaxed);
}

.card__author {
  --author-gap: var(--space-sm);
}

.card__avatar {
  --avatar-size: 2rem;
  
  width: var(--avatar-size);
  height: var(--avatar-size);
  border-radius: 50%;
}
```

### 4. Exceptions Layer (State Modifications)

Exceptions handle interactive states and variations.

#### Interactive States
```css
/* Focus States */
.card__title:focus-visible,
.card__tag:focus-visible {
  outline: var(--focus-outline-width) solid var(--focus-outline-color);
  outline-offset: var(--focus-outline-offset);
}

/* Hover States */
.card__title {
  transition: var(--transition-color);
}

.card__title:hover {
  color: var(--color-interactive);
  cursor: pointer;
}

/* Active States */
.card__title:active {
  transform: scale(0.98);
}
```

#### Card Variations
```css
/* Featured Card */
.card--featured {
  --card-shadow: var(--shadow-lg);
  --card-max-width: calc(var(--card-max-width) * 1.25);
}

/* Minimal Card */
.card--minimal {
  --card-shadow: none;
  --card-padding: var(--space-md);
}
```

## Component Assembly

### HTML Structure with CUBE CSS Classes

```html
<article class="card box">
  <div class="frame card__image">
    <img src="..." alt="..." />
  </div>
  
  <div class="stack card__content">
    <div>
      <span class="card__tag text-xs font-bold">Learning</span>
      <time class="card__date text-sm mt-sm block">Published 21 Dec 2023</time>
    </div>
    
    <h2 class="card__title">
      <a href="#" class="text-primary">HTML & CSS foundations</a>
    </h2>
    
    <p class="card__description text-base">
      These languages are the backbone of every website...
    </p>
    
    <div class="cluster card__author">
      <img class="card__avatar" src="..." alt="..." />
      <span class="text-sm font-bold">Greg Hooper</span>
    </div>
  </div>
</article>
```

## CSS Organization

### File Structure
```
styles/
├── composition/
│   ├── _center.css
│   ├── _stack.css
│   ├── _cluster.css
│   ├── _frame.css
│   └── _box.css
├── utilities/
│   ├── _colors.css
│   ├── _typography.css
│   ├── _spacing.css
│   └── _layout.css
├── blocks/
│   └── _card.css
├── exceptions/
│   ├── _states.css
│   └── _variations.css
└── main.css
```

### Import Order (main.css)
```css
/* Design Tokens */
@import 'tokens.css';

/* Composition Layer */
@import 'composition/_center.css';
@import 'composition/_stack.css';
@import 'composition/_cluster.css';
@import 'composition/_frame.css';
@import 'composition/_box.css';

/* Utilities Layer */
@import 'utilities/_colors.css';
@import 'utilities/_typography.css';
@import 'utilities/_spacing.css';
@import 'utilities/_layout.css';

/* Blocks Layer */
@import 'blocks/_card.css';

/* Exceptions Layer */
@import 'exceptions/_states.css';
@import 'exceptions/_variations.css';
```

## Key Architectural Decisions

### Composition First
- Every Layout patterns handle all responsive behavior
- No media queries needed due to intrinsic design
- Fluid spacing and typography scale naturally

### Utility Usage
- Utilities complement, not replace, semantic styles
- Used for common, reusable properties
- Keep specificity low for easy overrides

### Block Naming
- BEM-like convention for clarity
- Component custom properties for easy theming
- Scoped variables prevent conflicts

### Exception Handling
- States use CSS pseudo-classes
- Variations use modifier classes
- Progressive enhancement approach

## Benefits of This Architecture

1. **Maintainability**: Clear separation of concerns
2. **Scalability**: Easy to add new components or variations
3. **Performance**: Minimal CSS, efficient selectors
4. **Flexibility**: Components work in any context
5. **Accessibility**: Semantic HTML with proper states
6. **Responsive**: Intrinsic design without media queries