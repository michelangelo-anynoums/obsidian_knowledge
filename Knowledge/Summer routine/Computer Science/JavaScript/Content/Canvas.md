## 🎨 JavaScript Canvas – Essential Concepts & Methods

## 🧠 What is Canvas?

The **canvas** element lets you draw graphics via JavaScript (2D shapes, animations, images, games).

---

### Declare the CANVAS

```JavaScript
const canvas = document.getElementById("c");  
const ctx = canvas.getContext("2d");  
```

## 🏗️ Basic Setup

<canvas id="myCanvas" width="500" height="300"></canvas>

const canvas = document.getElementById("myCanvas");  
const ctx = canvas.getContext("2d");

- `ctx` → drawing context (2D API)

---

## 📏 Drawing Shapes

### Rectangle

```JavaScript
ctx.fillStyle = "blue";  
ctx.fillRect(50, 50, 150, 100);

ctx.strokeStyle = "red";  
ctx.strokeRect(50, 50, 150, 100); 
```

---

### Path (Custom Shapes)

```JavaScript
ctx.beginPath();  
ctx.moveTo(50, 50);  
ctx.lineTo(200, 50);  
ctx.lineTo(200, 150);  
ctx.closePath();  
ctx.stroke();
```

---

### Circle / Arc

```JavaScript
ctx.beginPath();  
ctx.arc(100, 100, 50, 0, Math.PI * 2);  
ctx.fill();
```

---

## 🎨 Styles & Colors

```JavaScript
ctx.fillStyle = "green";  
ctx.strokeStyle = "black";  
ctx.lineWidth = 5;
```

### Gradients

```JavaScript
const grad = ctx.createLinearGradient(0, 0, 200, 0);  
grad.addColorStop(0, "red");  
grad.addColorStop(1, "blue");  
  
ctx.fillStyle = grad;  
ctx.fillRect(10, 10, 200, 100);
```

---

## 🔤 Text Drawing

```JavaScript
ctx.font = "20px Arial";  
ctx.fillText("Hello Canvas", 50, 50);

ctx.strokeText("Outline Text", 50, 100);
```

---

## 🖼️ Images

```JavaScript
const img = new Image();  
img.src = "image.png";  
  
img.onload = () => {  
  ctx.drawImage(img, 50, 50, 200, 150);  
};
```

---

## ✏️ Lines & Curves

### Line

```JavaScript
ctx.beginPath();  
ctx.moveTo(20, 20);  
ctx.lineTo(200, 20);  
ctx.stroke();
```

### Bezier Curve

```JavaScript
ctx.beginPath();  
ctx.moveTo(20, 100);  
ctx.bezierCurveTo(100, 0, 150, 200, 200, 100);  
ctx.stroke();
```

---

## 🔄 Transformations

```JavaScript
ctx.translate(100, 100);  
ctx.rotate(Math.PI / 4);  
ctx.scale(1.5, 1.5);
```

---

## 🧹 Clearing Canvas

```JavaScript
ctx.clearRect(0, 0, canvas.width, canvas.height);
```

---

## 🎞️ Animation (Core Concept)

```JavaScript
function draw() {  
  ctx.clearRect(0, 0, canvas.width, canvas.height);  
  
  ctx.fillRect(x, 50, 50, 50);  
  x += 2;  
  
  requestAnimationFrame(draw);  
}  
  
draw();
```

- `requestAnimationFrame()` → smooth animation loop

---

## 🖱️ Mouse Interaction

```JavaScript
canvas.addEventListener("click", (e) => {  
  const x = e.offsetX;  
  const y = e.offsetY;  
  
  ctx.fillRect(x, y, 10, 10);  
});
```

---

## 🎯 State Management

```JavaScript
ctx.save();  
  
// change styles  
ctx.fillStyle = "red";  
ctx.fillRect(10, 10, 50, 50);  
  
ctx.restore(); // restore previous state
```

---

## 🌟 Global Alpha & Composition

```JavaScript
ctx.globalAlpha = 0.5;  
ctx.fillRect(20, 20, 100, 100);

ctx.globalCompositeOperation = "multiply";
```

---

## 🧩 Useful Methods Summary

- `fillRect()` / `strokeRect()`
- `clearRect()`
- `beginPath()`, `closePath()`
- `moveTo()`, `lineTo()`
- `arc()`
- `fill()` / `stroke()`
- `drawImage()`
- `fillText()` / `strokeText()`
- `save()` / `restore()`
- `translate()`, `rotate()`, `scale()`

---

## ⚡ Quick Example

```JavaScript
const canvas = document.getElementById("c");  
const ctx = canvas.getContext("2d");  
  
ctx.fillStyle = "blue";  
ctx.fillRect(10, 10, 100, 100);  
  
ctx.beginPath();  
ctx.arc(200, 60, 40, 0, Math.PI * 2);  
ctx.fillStyle = "red";  
ctx.fill();
```

---

## ⚠️ Notes

- Canvas is **pixel-based** (not vector like SVG)
- Redrawing is required for animations
- State resets unless saved/restored
- Performance matters for complex scenes

---
