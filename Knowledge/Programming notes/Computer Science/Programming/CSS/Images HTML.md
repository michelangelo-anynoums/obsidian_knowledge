# 🖼️ HTML Image Attributes

> [!info] 💡 What are image attributes? Attributes define how an image is displayed, loaded, identified, and handled by the browser.

## 1. 📌 Basic attributes


```html
<img src="photo.jpg" alt="Mountain landscape">
```

|Attribute|Purpose|
|---|---|
|`src`|Image file path or URL.|
|`alt`|Alternative text if the image cannot load.|
|`width`|Image width in pixels.|
|`height`|Image height in pixels.|
|`title`|Tooltip displayed on hover.|

```html
<img
  src="photo.jpg"
  alt="Mountain"
  width="600"
  height="400"
  title="Mountain view"
>
```

## 2. ⚡ Loading attributes

Control how and when images are loaded.

|Attribute|Purpose|
|---|---|
|`loading="lazy"`|Loads image when approaching the viewport.|
|`loading="eager"`|Loads image immediately.|
|`decoding="async"`|Decodes without blocking other content.|
|`decoding="sync"`|Requests synchronous decoding.|
|`decoding="auto"`|Lets the browser decide.|
|`fetchpriority="high"`|Gives the image higher loading priority.|
|`fetchpriority="low"`|Gives the image lower loading priority.|

**Example:**

```html
<img
  src="gallery.jpg"
  alt="Gallery"
  loading="lazy"
  decoding="async"
>
```

⭐ For images visible immediately, avoid lazy loading. Use it for images further down the page.

## 3. 🔐 Security & privacy attributes

|Attribute|Purpose|
|---|---|
|`crossorigin`|Controls cross-origin image requests.|
|`referrerpolicy`|Controls referrer information sent with the request.|

**Examples:**

```html
<img
  src="https://example.com/image.jpg"
  crossorigin="anonymous"
  alt="Example"
>
```


```html
<img
  src="image.jpg"
  referrerpolicy="no-referrer"
  alt="Private image"
>
```

### 🔒 What about encryption?

HTML has **no** **encryption** **image attribute**.

- HTTPS encrypts image data during transmission.
- Encrypted storage protects image files at rest.
- `crossorigin` is not encryption.
- `referrerpolicy` controls privacy, not encryption.

```html
<img src="https://example.com/secure-image.jpg" alt="Secure image">
```

HTTPS protects the connection, not necessarily the image file itself.

## 4. 🎯 Other useful attributes

|Attribute|Purpose|
|---|---|
|`usemap`|Connects an image to a clickable image map.|
|`ismap`|Makes an image a server-side image map.|
|`sizes`|Defines image display sizes for responsive loading.|
|`srcset`|Provides multiple image resolutions.|

**Responsive image example:**

```html
<img
  src="small.jpg"
  srcset="small.jpg 480w, large.jpg 1200w"
  sizes="(max-width: 600px) 100vw, 600px"
  alt="Landscape"
>
```

The browser chooses the appropriate image based on screen size and resolution.
## 🧠 Quick reference

- `src` → Where is the image?
- `alt` → What does it represent?
- `width / height` → How big is it?
- `loading` → When should it load?
- `decoding` → How should it be decoded?
- `fetchpriority` → How important is loading it?
- `crossorigin` → How is cross-origin access handled?
- `referrerpolicy` → What referrer information is shared?
- `HTTPS` → Is the connection encrypted?

✨ **Remember:** Attributes control image behaviour; CSS controls image appearance.