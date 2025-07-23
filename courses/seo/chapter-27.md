---
title: Chapter 27
order: 27
---

# Optimizing Fonts


82% of web pages for desktop use web fonts. Custom fonts are important for the branding, design, and cross-browser/device consistency of your site. However, using a web font should not come at the cost of performance.

Next.js has built-in Automatic Webfont Optimization that inlines font CSS at build time, eliminating an extra round trip to fetch font declarations. This results in improvements to First Contentful Paint (FCP) and Largest Contentful Paint (LCP).

For example, here is the before and after of Next.js optimizing your font.

Before optimizing, an extra network request is needed:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter" rel="stylesheet" />
```

After optimizing, Next.js inlines the font CSS for you:

```
<style data-href="https://fonts.googleapis.com/css2?family=Inter">
  @font-face{font-family:'Inter';font-style:normal; }
</style>
```
