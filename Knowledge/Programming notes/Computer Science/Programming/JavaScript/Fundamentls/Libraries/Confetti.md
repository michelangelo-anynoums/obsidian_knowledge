# 🎉 JavaScript Confetti in Obsidian

## ✨ What is Canvas Confetti?

**Canvas Confetti** is a lightweight JavaScript library that creates colorful bursts of confetti. You can use it to celebrate completed tasks, study sessions, or personal milestones in Obsidian.

🔗 **Official library:** [https://github.com/catdad/canvas-confetti](https://github.com/catdad/canvas-confetti)

## 1. 📦 Import the library into HTML

> [!important] The easiest way to try Canvas Confetti in a standalone HTML document is to use a CDN (Content Delivery Network). Add this script tag to your HTML file:

```html
<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.3/dist/confetti.browser.min.js"></script>
```

Place it inside the `<head>` section or before your own JavaScript code near the end of `<body>`.

**What happens here?**

- `cdn.jsdelivr.net` serves the library over the web.
- `canvas-confetti@1.9.3` specifies the library version.
- `confetti.browser.min.js` is the browser-ready, compressed JavaScript file.

Once loaded, the library provides the global `confetti()` function.

## 2. 🎈 Your first confetti burst

Here is a complete, working HTML example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>My Confetti Celebration</title>

  <!-- Import Canvas Confetti -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.3/dist/confetti.browser.min.js"></script>
</head>
<body>
  <h1>🎉 Well done!</h1>
  <button onclick="confetti()">Celebrate!</button>
</body>
</html>
```

Save it as `confetti.html` and open it in a browser with an internet connection. Click **Celebrate!** to see the effect.

## 3. 🎨 Customize your celebration

```js
confetti({
  particleCount: 100,
  spread: 70,
  origin: { y: 0.6 }
});
```

- `particleCount` — how many particles appear.
- `spread` — how widely they scatter.
- `origin.y` — the vertical starting position, expressed as a fraction of the screen height.

Try changing `100` to `30` or `250` and compare the results.

## 4. 🌈 Choose your colors

```js
confetti({
  particleCount: 80,
  colors: ["#FFD700", "#FF69B4", "#7B68EE"]
});
```

This creates a gold, pink, and purple celebration. Use hexadecimal color codes to make your own palette.

## 5. ✅ Create a reusable function

```js
function celebrate() {
  confetti({
    particleCount: 120,
    spread: 90,
    origin: { y: 0.7 }
  });
}
```

Now you can trigger the effect whenever you call:

```js
celebrate();
```

For example, connect it to a button:

```js
<button onclick="celebrate()">Task completed!</button>
```

Make sure the function is defined in a script that the button can access.

---

### 💎 The takeaway

1. **Import** the library with a `<script>` tag.
2. **Call** `confetti()` to create a burst.
3. **Customize** the colors, particle count, and spread.
4. **Connect** it to an action, such as clicking a button.

---
