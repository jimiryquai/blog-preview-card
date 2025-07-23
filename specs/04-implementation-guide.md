# Implementation Guide

## Overview

This guide provides step-by-step instructions for implementing the blog preview card component using semantic HTML, CUBE CSS, and Every Layout patterns. Follow these steps to build a responsive, accessible component without media queries.

## Phase 1: HTML Structure

### 1.1 Document Setup

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Blog preview card component showcasing HTML & CSS foundations">
  
  <!-- Favicon -->
  <link rel="icon" type="image/png" sizes="32x32" href="./assets/images/favicon-32x32.png">
  
  <!-- Local Fonts -->
  <style>
    @font-face {
      font-family: 'Figtree';
      src: url('./assets/fonts/Figtree-VariableFont_wght.ttf') format('truetype');
      font-weight: 100 900;
      font-display: swap;
    }
  </style>
  
  <!-- Styles -->
  <link rel="stylesheet" href="styles/main.css">
  
  <title>Frontend Mentor | Blog preview card</title>
</head>
```

### 1.2 Semantic HTML Structure

```html
<body>
  <main class="center">
    <article class="card box" itemscope itemtype="https://schema.org/BlogPosting">
      <!-- Article Illustration -->
      <figure class="frame card__image">
        <img 
          src="./assets/images/illustration-article.svg" 
          alt="Abstract illustration representing HTML and CSS concepts"
          width="336"
          height="200"
          itemprop="image"
        >
      </figure>
      
      <!-- Article Content -->
      <div class="stack card__content">
        <!-- Metadata -->
        <header>
          <span class="card__tag text-xs font-bold">Learning</span>
          <time 
            class="card__date text-sm mt-sm block" 
            datetime="2023-12-21"
            itemprop="datePublished"
          >
            Published 21 Dec 2023
          </time>
        </header>
        
        <!-- Title -->
        <h1 class="card__title" itemprop="headline">
          <a href="#" class="text-primary">HTML & CSS foundations</a>
        </h1>
        
        <!-- Description -->
        <p class="card__description text-base" itemprop="description">
          These languages are the backbone of every website, defining structure, 
          content, and presentation.
        </p>
        
        <!-- Author -->
        <footer class="cluster card__author" itemprop="author" itemscope itemtype="https://schema.org/Person">
          <img 
            class="card__avatar" 
            src="./assets/images/image-avatar.webp" 
            alt="Greg Hooper"
            width="32"
            height="32"
            itemprop="image"
          >
          <span class="text-sm font-bold" itemprop="name">Greg Hooper</span>
        </footer>
      </div>
    </article>
  </main>
  
  <!-- Attribution -->
  <footer class="attribution text-xs text-secondary">
    Challenge by <a href="https://www.frontendmentor.io?ref=challenge" target="_blank" rel="noopener">Frontend Mentor</a>. 
    Coded by <a href="#" rel="author">Your Name Here</a>.
  </footer>
</body>
```

### 1.3 HTML Best Practices Applied

- **Semantic Elements**: `<article>`, `<figure>`, `<header>`, `<footer>`, `<time>`
- **Microdata**: Schema.org BlogPosting for SEO
- **Accessibility**: Descriptive alt text, proper heading hierarchy
- **Performance**: Width/height attributes on images
- **Links**: rel="noopener" for external links

## Phase 2: CSS Implementation

### 2.1 CSS Reset and Base Styles

Create `styles/base.css`:

```css
/* Modern CSS Reset */
*, *::before, *::after {
  box-sizing: border-box;
}

* {
  margin: 0;
  padding: 0;
}

html {
  /* Fluid base font size */
  font-size: clamp(100%, 1rem + 0.5vw, 112.5%);
  -webkit-text-size-adjust: 100%;
}

body {
  min-height: 100vh;
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

img, picture, video, canvas, svg {
  display: block;
  max-width: 100%;
  height: auto;
}

input, button, textarea, select {
  font: inherit;
}

p, h1, h2, h3, h4, h5, h6 {
  overflow-wrap: break-word;
}

a {
  color: inherit;
  text-decoration: none;
}

/* Focus visible polyfill */
:focus-visible {
  outline: var(--focus-outline-width) solid var(--focus-outline-color);
  outline-offset: var(--focus-outline-offset);
}

:focus:not(:focus-visible) {
  outline: none;
}
```

### 2.2 Design Tokens Implementation

Create `styles/tokens.css`:

```css
:root {
  /* Import all design tokens from design system spec */
  /* Colors, Typography, Spacing, etc. */
  /* (Full token list in 02-design-system.md) */
}

/* Dark mode support (optional enhancement) */
@media (prefers-color-scheme: dark) {
  :root {
    /* Dark mode token overrides */
  }
}
```

### 2.3 Global Styles

Create `styles/global.css`:

```css
/* Base Typography */
body {
  font-family: var(--font-family-base);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-normal);
  line-height: var(--line-height-base);
  color: var(--color-text-primary);
  background-color: var(--color-background);
}

/* Global link styles */
a {
  position: relative;
  transition: var(--transition-color);
}

/* Attribution styles */
.attribution {
  position: fixed;
  bottom: 1rem;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  z-index: 10;
}

.attribution a {
  color: var(--color-text-primary);
  text-decoration: underline;
  text-underline-offset: 0.2em;
}
```

### 2.4 Main Stylesheet Organization

Create `styles/main.css`:

```css
/* Base Styles */
@import 'base.css';

/* Design Tokens */
@import 'tokens.css';

/* Global Styles */
@import 'global.css';

/* Composition Layer - Every Layout */
@import 'composition/center.css';
@import 'composition/stack.css';
@import 'composition/cluster.css';
@import 'composition/frame.css';
@import 'composition/box.css';

/* Utilities Layer */
@import 'utilities/colors.css';
@import 'utilities/typography.css';
@import 'utilities/spacing.css';
@import 'utilities/layout.css';

/* Blocks Layer */
@import 'blocks/card.css';

/* Exceptions Layer */
@import 'exceptions/states.css';
```

## Phase 3: Component Implementation

### 3.1 Card Component Styles

Create `styles/blocks/card.css`:

```css
/* Card Container */
.card {
  --card-shadow: var(--shadow-card);
  --card-max-width: var(--card-max-width);
  
  position: relative;
  width: 100%;
  max-width: var(--card-max-width);
  margin-inline: auto;
  box-shadow: var(--card-shadow);
  overflow: hidden;
  background-color: var(--color-surface);
}

/* Card Image */
.card__image {
  --image-aspect-ratio: 336 / 200;
  aspect-ratio: var(--image-aspect-ratio);
}

/* Card Content Container */
.card__content {
  --content-spacing: var(--space-stack);
}

/* Category Tag */
.card__tag {
  --tag-background: var(--color-primary);
  --tag-color: var(--color-text-primary);
  --tag-padding-inline: var(--space-sm);
  --tag-padding-block: calc(var(--space-xs) / 2);
  --tag-radius: var(--radius-sm);
  
  display: inline-block;
  padding-inline: var(--tag-padding-inline);
  padding-block: var(--tag-padding-block);
  background-color: var(--tag-background);
  color: var(--tag-color);
  border-radius: var(--tag-radius);
  font-size: var(--font-size-xs);
  font-weight: var(--font-weight-bold);
}

/* Date */
.card__date {
  color: var(--color-text-secondary);
  font-size: var(--font-size-sm);
}

/* Title */
.card__title {
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-bold);
  line-height: var(--line-height-tight);
}

.card__title a {
  display: block;
  color: var(--color-text-primary);
}

/* Description */
.card__description {
  color: var(--color-text-secondary);
  line-height: var(--line-height-relaxed);
}

/* Author Section */
.card__author {
  --author-gap: var(--space-sm);
  align-items: center;
}

/* Avatar */
.card__avatar {
  --avatar-size: 2rem;
  
  width: var(--avatar-size);
  height: var(--avatar-size);
  border-radius: 50%;
  object-fit: cover;
}
```

### 3.2 Interactive States

Create `styles/exceptions/states.css`:

```css
/* Hover States */
.card__title a:hover {
  color: var(--color-interactive);
}

.card:hover {
  --card-shadow: var(--shadow-lg);
}

/* Focus States */
.card__title a:focus-visible,
.card__tag:focus-visible,
.attribution a:focus-visible {
  outline: var(--focus-outline-width) solid var(--focus-outline-color);
  outline-offset: var(--focus-outline-offset);
  border-radius: var(--radius-sm);
}

/* Active States */
.card__title a:active {
  transform: scale(0.98);
}

/* Transition for smooth interactions */
.card,
.card__title a {
  transition: 
    var(--transition-color),
    var(--transition-transform),
    var(--transition-shadow);
}
```

## Phase 4: Testing & Validation

### 4.1 Cross-Browser Testing Checklist

- [ ] Chrome/Edge (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Mobile browsers (iOS Safari, Chrome Android)

### 4.2 Accessibility Testing

- [ ] Keyboard navigation works correctly
- [ ] Focus states are visible
- [ ] Screen reader announces content properly
- [ ] Color contrast meets WCAG AA standards
- [ ] Touch targets are at least 44×44px

### 4.3 Performance Validation

- [ ] Images are optimized (WebP with fallbacks)
- [ ] CSS is minified for production
- [ ] Fonts load efficiently (font-display: swap)
- [ ] No layout shifts during load

### 4.4 Responsive Testing

- [ ] 320px minimum width
- [ ] Smooth scaling without media queries
- [ ] Text remains readable at all sizes
- [ ] No horizontal scrolling

## Phase 5: Production Optimization

### 5.1 CSS Optimization

```bash
# Combine and minify CSS
npx cssnano styles/main.css styles/main.min.css

# Or use PostCSS with plugins
npx postcss styles/main.css -o dist/main.css
```

### 5.2 Image Optimization

```bash
# Convert images to WebP
cwebp assets/images/image-avatar.webp -o assets/images/image-avatar.webp

# Optimize SVGs
npx svgo assets/images/illustration-article.svg
```

### 5.3 Font Loading Strategy

For better performance, you can add the @font-face declaration directly in your CSS:

```css
/* In styles/global.css or styles/tokens.css */
@font-face {
  font-family: 'Figtree';
  src: url('../assets/fonts/Figtree-VariableFont_wght.ttf') format('truetype');
  font-weight: 100 900;
  font-display: swap;
}

/* Optional: Load specific weights for older browsers */
@font-face {
  font-family: 'Figtree';
  src: url('../assets/fonts/static/Figtree-Medium.ttf') format('truetype');
  font-weight: 500;
  font-display: swap;
}

@font-face {
  font-family: 'Figtree';
  src: url('../assets/fonts/static/Figtree-ExtraBold.ttf') format('truetype');
  font-weight: 800;
  font-display: swap;
}
```

For optimal loading, you can also preload the variable font:

```html
<!-- Preload the variable font file -->
<link rel="preload" href="./assets/fonts/Figtree-VariableFont_wght.ttf" as="font" type="font/truetype" crossorigin>
```

## Common Implementation Pitfalls

### Avoid These Mistakes

1. **Using px for spacing**: Use rem/em for scalability
2. **Hard-coding colors**: Always use design tokens
3. **Forgetting focus states**: Essential for accessibility
4. **Over-specifying selectors**: Keep specificity low
5. **Missing semantic HTML**: Use appropriate elements

### Best Practices Reminders

1. Test early and often
2. Validate HTML and CSS
3. Check accessibility from the start
4. Use browser DevTools for debugging
5. Keep code organized and documented

## Next Steps

1. Implement the HTML structure
2. Add CSS layer by layer
3. Test interactivity and responsiveness
4. Optimize for production
5. Deploy and gather feedback