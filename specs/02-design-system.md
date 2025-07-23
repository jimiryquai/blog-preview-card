# Design System Specification

## Overview

This design system defines the visual language for the blog preview card component based on the provided Frontend Mentor style guide. All values are derived directly from the style guide without unnecessary elaboration.

## Color Tokens

### Base Colors (From Style Guide)

```css
:root {
  /* Exact colors from style guide */
  --color-yellow: hsl(47, 88%, 63%);       /* #F4D04E */
  --color-white: hsl(0, 0%, 100%);         /* #FFFFFF */
  --color-gray-950: hsl(0, 0%, 7%);        /* #111111 */
  --color-gray-500: hsl(0, 0%, 42%);       /* #6B6B6B */
  
  /* Semantic Usage */
  --color-background: var(--color-yellow);
  --color-surface: var(--color-white);
  --color-text-primary: var(--color-gray-950);
  --color-text-secondary: var(--color-gray-500);
  --color-accent: var(--color-yellow);
}
```

### Color Usage

- **Yellow**: Page background, category tags, hover states
- **White**: Card background, content areas
- **Gray-950**: Main text, headings, author names
- **Gray-500**: Secondary text, dates, descriptions

## Typography System

### Font Configuration (From Style Guide)

```css
:root {
  /* Font Family */
  --font-family-base: 'Figtree', sans-serif;
  
  /* Font Weights (from style guide) */
  --font-weight-medium: 500;
  --font-weight-extra-bold: 800;
}
```

### Typography Presets (Exact from Style Guide)

```css
:root {
  /* Text Preset 1: Figtree Extra Bold, 24px, 150% line height */
  --text-preset-1-size: 1.5rem;        /* 24px */
  --text-preset-1-weight: var(--font-weight-extra-bold);
  --text-preset-1-line-height: 1.5;    /* 150% */
  
  /* Text Preset 2: Figtree Medium, 16px, 150% line height */
  --text-preset-2-size: 1rem;          /* 16px */
  --text-preset-2-weight: var(--font-weight-medium);
  --text-preset-2-line-height: 1.5;    /* 150% */
  
  /* Text Preset 3: Figtree Medium, 14px, 150% line height */
  --text-preset-3-size: 0.875rem;      /* 14px */
  --text-preset-3-weight: var(--font-weight-medium);
  --text-preset-3-line-height: 1.5;    /* 150% */
  
  /* Text Preset 3 (Bold): Figtree Extra Bold, 14px, 150% line height */
  --text-preset-3-bold-size: 0.875rem;     /* 14px */
  --text-preset-3-bold-weight: var(--font-weight-extra-bold);
  --text-preset-3-bold-line-height: 1.5;   /* 150% */
}
```

### Typography Usage

- **Card Title**: Text Preset 1 (24px, Extra Bold, 150% line height)
- **Body Text**: Text Preset 2 (16px, Medium, 150% line height)
- **Metadata/Date**: Text Preset 3 (14px, Medium, 150% line height)
- **Category Tag**: Text Preset 3 Bold (14px, Extra Bold, 150% line height)

## Spacing System

### Spacing Scale (Exact from Style Guide)

```css
:root {
  /* Exact spacing values from style guide */
  --space-50: 0.25rem;   /* 4px */
  --space-100: 0.5rem;   /* 8px */
  --space-150: 0.75rem;  /* 12px */
  --space-300: 1.5rem;   /* 24px */
}
```

### Spacing Usage

Based on visual inspection of the design and provided spacing values:

- **Card internal padding**: `--space-300` (24px)
- **Vertical spacing between elements**: `--space-150` (12px) 
- **Small gaps**: `--space-100` (8px)
- **Minimal spacing**: `--space-50` (4px)

## Layout & Visual Properties

### Basic Layout Constraints

```css
:root {
  /* Layout references from style guide */
  --layout-mobile: 23.4375rem;    /* 375px */
  --layout-desktop: 90rem;        /* 1440px */
  
  /* Card will be sized intrinsically */
  --card-max-width: 24rem;        /* Approximate based on design */
  
  /* Simple border radius (estimated from design) */
  --radius-card: 0.75rem;         /* 12px */
  --radius-tag: 0.25rem;          /* 4px */
}
```

### Shadow (From Design)

From visual inspection of the design, a hard drop shadow:

```css
:root {
  /* Hard drop shadow - 0.5rem right, 0.5rem down, no blur, black */
  --shadow-card: 0.5rem 0.5rem 0 0 #000;
}
```

## Responsive Strategy

### No Media Queries Approach

For responsive design without media queries:

```css
:root {
  /* Use intrinsic sizing */
  --card-width: min(100% - 2rem, var(--card-max-width));
  
  /* Optional: Fluid typography for better mobile experience */
  --font-size-fluid-title: clamp(1.25rem, 4vw, 1.5rem); /* 20px-24px */
}
```

### Interaction States (Minimal)

```css
:root {
  /* Simple transitions */
  --transition-base: 0.2s ease;
  
  /* Hover color (title turns yellow) */
  --color-interactive-hover: var(--color-yellow);
}
```

## Implementation Notes

### Evidence-Based Design System

This simplified design system is based directly on the provided style guide:
- **4 colors** (exact HSL values)
- **4 typography presets** (exact sizes, weights, line heights)
- **4 spacing values** (exact pixel values)
- **Minimal visual properties** (estimated from design)

### Responsive Without Media Queries

- Use `min()` and `max()` for intrinsic sizing
- Optional `clamp()` for fluid typography
- Every Layout patterns for natural responsiveness
- Percentage-based widths with max-width constraints

### Token Philosophy

- **Minimal**: Only include what's provided or visually evident
- **Direct**: Map tokens to exact style guide values
- **Semantic**: Create meaningful aliases for component usage
- **Simple**: Avoid complex calculations or elaborate scales