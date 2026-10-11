# 🌐 BOM — Browser Object Model

> [!abstract] Overview The **Browser Object Model (BOM)** allows JavaScript to interact with the web browser outside the webpage itself.

## 🧩 1. What is the BOM?

The BOM provides objects that let JavaScript control or access browser features, such as:

- 🌍 The browser window
- 📍 The current URL
- 🕒 Timers and delays
- 🧭 Browser history
- 💻 Information about the user's browser

The main object is `window`.

## 🪟 2. The `window` Object

The `window` object represents the browser window and provides access to many browser features.

```js
console.log(window);
console.log(window.innerWidth);
console.log(window.innerHeight);
```

- `window.innerWidth` → Browser viewport width.
- `window.innerHeight` → Browser viewport height.
- `window.alert()` → Displays an alert message.

Example:

```js
window.alert("Hello, world!");
```

**Note:** In a browser's classic script, many `window` properties and methods can be accessed without writing `window.` explicitly.

```js
alert("Hello!");
console.log(innerWidth);
```

## 🧭 3. Important BOM Objects

|Object|Purpose|
|---|---|
|`window`|Represents the browser window|
|`location`|Gets or changes the current URL|
|`history`|Navigates through session history|
|`navigator`|Provides browser and device information|
|`screen`|Provides information about the screen|

### 📍 Location

Access information about the current URL.

```js
console.log(location.href);
console.log(location.hostname);
```

- `location.href` → The complete URL.
- `location.hostname` → The hostname.

To navigate to another page:

```js
location.href = "https://example.com";
```

### ⏳ Timers

Execute code after a delay or repeatedly.

```js
setTimeout(() => {
  console.log("Hello after 2 seconds!");
}, 2000);
```

Repeat an action every second:

```js
const timer = setInterval(() => {
  console.log("One second passed");
}, 1000);
```

Stop the interval:

```js
clearInterval(timer);
```

### 🕰️ History

Access the browser's session history.

```js
history.back();
history.forward();
```

- `history.back()` → Goes back one history entry.
- `history.forward()` → Goes forward one history entry.

### 🧑‍💻 Navigator

Access information about the browser.

```js
console.log(navigator.language);
console.log(navigator.onLine);
```

- `navigator.language` → The browser's preferred language.
- `navigator.onLine` → Indicates the browser's current online-status estimate.

### 🖥️ Screen

Access information about the user's screen.

```js
console.log(screen.width);
console.log(screen.height);
```

These properties report the screen's width and height in pixels.

---
## 🔍 Browser Detection with JavaScript

### Method 1 — Using `navigator.userAgent`

```js
function detectBrowser() {
  const ua = navigator.userAgent;

  if (/Edg\//i.test(ua)) {
    return "Microsoft Edge";
  }

  if (/OPR\//i.test(ua)) {
    return "Opera";
  }

  if (/Firefox\//i.test(ua)) {
    return "Mozilla Firefox";
  }

  if (/Chrome\//i.test(ua) && !/Edg\//i.test(ua)) {
    return "Google Chrome or Chromium-based browser";
  }

  if (/Safari\//i.test(ua) && !/Chrome\//i.test(ua)) {
    return "Safari or another WebKit-based browser";
  }

  return "Unknown browser";
}

console.log(detectBrowser());
```

**Important:** User-agent strings can be modified, reduced or shared by multiple browsers. This example is useful for learning, but it cannot identify every browser perfectly.

### Method 2 — Using `navigator.userAgentData`

Modern Chromium-based browsers may support the User-Agent Client Hints API.

```js
if (navigator.userAgentData) {
  console.log(navigator.userAgentData.brands);
  console.log(navigator.userAgentData.mobile);
  console.log(navigator.userAgentData.platform);
} else {
  console.log("User-Agent Client Hints not supported");
}
```

To request more detailed information:

```js
async function getBrowserDetails() {
  if (!navigator.userAgentData) {
    console.log("API not supported");
    return;
  }

  const details =
    await navigator.userAgentData.getHighEntropyValues([
      "architecture",
      "bitness",
      "fullVersionList",
      "model",
      "platformVersion"
    ]);

  console.log(details);
}

getBrowserDetails();
```

This API is not available in every browser and generally requires a secure context. Avoid relying on it as your only detection method.

### Method 3 — Detect a feature instead of a browser

Often, the better solution is to check whether the feature you need exists.

```js
if ("geolocation" in navigator) {
  console.log("Geolocation API is available");
}

if ("serviceWorker" in navigator) {
  console.log("Service workers are supported");
}

if ("clipboard" in navigator) {
  console.log("Clipboard API is available");
}
```

**Best practice:** Prefer feature detection over browser detection whenever possible.

---
