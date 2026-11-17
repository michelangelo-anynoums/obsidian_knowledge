# 🖼️ HTML Images Optimization + React

> [!abstract] Goal Load images faster, reduce file size, improve performance and avoid layout shifts.

## 1. 📐 HTML Image Rules

**Always define dimensions** to prevent layout shifts.

```html
<img
  src="/images/photo.webp"
  alt="Mountain landscape"
  width="800"
  height="600"
/>
```

**Use modern formats:**

- `WebP` → good compression and quality.
- `AVIF` → often smaller files.
- `SVG` → icons and vector graphics.

## 2. ⚡ Lazy Loading

Load images only when they approach the viewport.


```html
<img
  src="/images/photo.webp"
  alt="Nature"
  loading="lazy"
  width="800"
  height="600"
/>
```

**Important:**

- `loading="lazy"` → below-the-fold images.
- `loading="eager"` → load immediately.
- Avoid lazy loading the main hero/LCP image.

## 3. 🚀 Priority Loading

Prioritize important images, especially the hero image.

```html
<img
  src="/images/hero.webp"
  alt="Homepage hero"
  fetchpriority="high"
  loading="eager"
  width="1600"
  height="900"
/>
```

**Rule:** High priority for the main visual, not every image.

## 4. 📱 Responsive Images

Serve different image sizes depending on the screen.


```html
<img
  src="/images/photo-800.webp"
  srcset="
    /images/photo-400.webp 400w,
    /images/photo-800.webp 800w,
    /images/photo-1200.webp 1200w
  "
  sizes="(max-width: 600px) 100vw, 800px"
  alt="Landscape"
/>
```

- `srcset` → available image sizes.
- `sizes` → expected display width.
- Browser selects the appropriate source.

## 6. 🎯 Quick Rules

| Rule                   | Benefit                     |
| ---------------------- | --------------------------- |
| WebP / AVIF            | Smaller files               |
| `width` + `height`     | Prevent layout shifts       |
| `loading="lazy"`       | Reduce initial loading      |
| `fetchpriority="high"` | Prioritize important images |
| `srcset` + `sizes`     | Responsive images           |
| `decoding="async"`     | Asynchronous decoding       |
| Descriptive `alt`      | Accessibility + SEO         |

---

## 💡 Golden Rule

**Optimize before rendering.**

- Compress images.
- Choose the correct format.
- Serve the correct dimensions.
- Lazy-load offscreen images.
- Prioritize the main visual.
- Never sacrifice accessibility (`alt`).

---
