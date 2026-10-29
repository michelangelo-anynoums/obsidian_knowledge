# 📄 Embed a PDF in HTML

> [!abstract] 💡 The idea Use `<iframe>` to display a PDF directly inside an HTML page.

## ⚡ Basic example


```html
<iframe
  src="document.pdf"
  width="100%"
  height="600">
</iframe>
```

- `src` → path or URL of the PDF.
- `width` → viewer width.
- `height` → viewer height.

## 📍 Open a specific page


```html
<iframe
  src="document.pdf#page=3"
  width="100%"
  height="600">
</iframe>
```

Opens the PDF at page 3 in compatible PDF viewers.

## 🎨 Add styling

```html
<iframe
  src="document.pdf"
  style="width: 100%; height: 80vh; border: none;">
</iframe>
```

- `100%` → fills the container width.
- `80vh` → uses 80% of the viewport height.
- `border: none` → removes the frame border.

## 🔄 Alternative: `<object>`

```html
<object
  data="document.pdf"
  type="application/pdf"
  width="100%"
  height="600">

  <a href="document.pdf">📥 Download PDF</a>

</object>
```

Displays the PDF when supported, with a download link as fallback content.

## 🔗 Just link to the PDF

```html
<a href="document.pdf" target="_blank">
  📄 Open PDF
</a>
```

Opens the PDF separately in the browser.

## 🧠 Remember

- `<iframe>` → embed a PDF viewer.
- `<object>` → embed with fallback content.
- `<a>` → link to the PDF.
- `#page=3` → request page 3 in supported PDF viewers.

---
