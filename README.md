# Vanilla View Transitions

A comprehensive demonstration of the CSS View Transitions API for multi-page applications, showcasing multiple real-world use cases with smooth cross-document animations using pure CSS.

## Overview

This project demonstrates cross-document view transitions using pure CSS, leveraging the native View Transitions API available in modern browsers. It showcases three key use cases recommended by Chrome's documentation: image expansion, product catalogs with filtering, and navigation persistence - all without JavaScript framework overhead.

## Features

- **Zero JavaScript for Transitions**: All animations powered entirely by CSS
- **Cross-Document Transitions**: Smooth animations between separate HTML pages
- **Named View Transitions**: Elements with matching `view-transition-name` properties morph seamlessly between pages
- **Multiple Real-World Examples**: Gallery, product catalog, and detail views
- **Dynamic Filtering**: Product catalog with category-based filtering
- **Custom Animations**: Slide and blur effects for page transitions
- **Accessibility Conscious**: Respects `prefers-reduced-motion` user preferences
- **Modern CSS**: Built with Open Props for consistent design tokens
- **Responsive Design**: Works seamlessly across different screen sizes

## Live Examples

### 1. Image Gallery

Demonstrates the **thumbnail-to-detail expansion** pattern. Click any image thumbnail to see it smoothly morph into a full-size detail view. Each image maintains visual continuity using unique `view-transition-name` properties.

**Key Concept**: Individual element tracking across navigation

### 2. Product Catalog

Showcases **dynamic content filtering** with smooth transitions. Filter products by category and watch cards reposition smoothly. Click any product to see it expand into a detailed view with multiple transitioning elements (image, title, price).

**Key Concepts**:

- Multiple simultaneous transitions
- Content reordering with maintained identity
- Nested transitions (grid to detail)

### 3. About Page

Illustrates **navigation persistence** where header and footer elements maintain their position across page changes, while main content slides in from the side.

**Key Concept**: Fixed element continuity during navigation

## How It Works

The View Transitions API operates in three phases:

1. **Capture**: Browser takes snapshots of the old and new page states
2. **Update**: DOM updates occur while rendering is suppressed
3. **Animate**: CSS animations create smooth visual transitions between states

Elements sharing the same `view-transition-name` automatically morph between pages, maintaining visual continuity. Elements without named transitions use the default root transition animation.

## Browser Support

This project requires browsers with View Transitions API support:

- Chrome 126+
- Edge 126+
- Opera 112+

For unsupported browsers, the site functions normally with instant page navigation.

## Implementation Guide

### 1. Enabling Cross-Document Transitions

Add this CSS rule to opt-in to automatic transitions. The `prefers-reduced-motion` check ensures accessibility:

```css
@media (prefers-reduced-motion: no-preference) {
  @view-transition {
    navigation: auto;
  }
}
```

### 2. Creating Named Transitions

Apply matching `view-transition-name` values to elements that should morph between pages. Each name must be unique per page:

```css
/* In CSS */
.profile {
  view-transition-name: profile;
}

/* Or inline in HTML */
<img style="view-transition-name: gallery-img-1" src="..." />
```

**Important**: The same `view-transition-name` on both pages creates the morphing effect.

### 3. Maintaining Fixed Elements

Elements like navigation and footers can persist visually across transitions:

```css
nav {
  view-transition-name: nav;
}

footer {
  view-transition-name: footer;
}
```

### 4. Customizing Animations

Override default transition animations using pseudo-elements:

```css
::view-transition-old(root) {
  animation: fade-out-left 300ms ease-in forwards;
}

::view-transition-new(root) {
  animation: fade-in-right 300ms ease-out forwards;
}
```

### 5. Dynamic Transitions with JavaScript

For dynamic content, set `view-transition-name` programmatically:

```javascript
document
  .getElementById("product-image")
  .style.setProperty("view-transition-name", `product-img-${id}`);
```

## Local Development

1. Clone the repository
2. Serve the files using any static web server
3. Navigate to the demo in a supported browser

Example using Node.js:

```bash
npx serve
```

## Project Structure

```
.
├── index.html              # Home page with example showcase
├── gallery.html            # Image gallery grid
├── image-detail.html       # Expanded image detail view
├── products.html           # Product catalog with filtering
├── product-detail.html     # Individual product details
├── about.html              # How it works explanation
├── index.css               # Styles and transition definitions
└── README.md               # Documentation
```

## Technical Highlights

### Unique View Transition Names

Each transitioning element requires a unique name. This project demonstrates:

- Gallery images: `gallery-img-1`, `gallery-img-2`, etc.
- Product cards: `product-img-1`, `product-title-1`, etc.
- Persistent elements: `nav`, `footer`

### Accessibility

The demo respects user motion preferences:

```css
@media (prefers-reduced-motion: no-preference) {
  /* Transitions only enabled when user allows motion */
}
```

### Progressive Enhancement

Works in all browsers - unsupported browsers simply navigate instantly without transitions.

## Resources

- [Open Props Design System](https://open-props.style/)
- [View Transitions API Documentation](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API)
- [Smooth transitions with the View Transition API](https://developer.chrome.com/docs/web-platform/view-transitions)

## License

This project is open source and available for educational purposes.
