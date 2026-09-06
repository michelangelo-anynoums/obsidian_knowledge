## 🧮 JavaScript Math – Essential Concepts & Methods

## 🧠 The **Math** Object

- Built-in object for mathematical operations
- No constructor → use directly: `Math.method()`

---

## 🔢 Important Constants

```JavaScript
Math.PI        // 3.141592653589793  
Math.E         // Euler's number (~2.718)  
Math.SQRT2     // √2  
Math.SQRT1_2   // √1/2  
Math.LN2       // ln(2)  
Math.LN10      // ln(10)
```

---

## ➕ Basic Operations

```JavaScript
Math.abs(-10)     // 10  
Math.sign(-5)     // -1  
Math.pow(2, 3)    // 8  
Math.sqrt(16)     // 4  
Math.cbrt(27)     // 3
```

---

## 🔄 Rounding Methods

```JavaScript
Math.round(4.6)   // 5  
Math.floor(4.9)   // 4  
Math.ceil(4.1)    // 5  
Math.trunc(4.9)   // 4
```

---

## 📊 Min / Max

```JavaScript
Math.max(1, 5, 3)   // 5  
Math.min(1, 5, 3)   // 1
```

---

## 🎲 Random Numbers

```JavaScript
Math.random()   // 0 → 1 (not inclusive of 1)
```

### Random integer in range

```JavaScript
function randomInt(min, max) {  
  return Math.floor(Math.random() * (max - min + 1)) + min;  
}
```

---

## 📐 Trigonometry

```JavaScript
Math.sin(Math.PI / 2)   // 1  
Math.cos(0)             // 1  
Math.tan(Math.PI / 4)   // 1
```

### Inverse trig

```JavaScript
Math.asin(1)  
Math.acos(1)  
Math.atan(1)
```

---

## 📏 Logarithms & Exponents

```JavaScript
Math.log(Math.E)     // 1 (natural log)  
Math.log10(100)      // 2  
Math.log2(8)         // 3  
Math.exp(1)          // e^1
```

---

## ⚖️ Number Checks

```JavaScript
Number.isNaN(NaN)        // true  
Number.isFinite(10)      // true  
Number.isInteger(5.0)    // true
```

---

## 🔢 Parsing Numbers

```JavaScript
parseInt("42")       // 42  
parseFloat("3.14")   // 3.14
```

---

## 🎯 Useful Patterns

### Clamp a value

```JavaScript
function clamp(val, min, max) {  
  return Math.min(Math.max(val, min), max);  
}
```

---

### Linear interpolation (lerp)

```JavaScript
function lerp(a, b, t) {  
  return a + (b - a) * t;  
}
```

---

### Distance between two points

```JavaScript
function distance(x1, y1, x2, y2) {  
  return Math.hypot(x2 - x1, y2 - y1);  
}
```

---

### Degrees ↔ Radians

```JavaScript
const degToRad = (deg) => deg * (Math.PI / 180);  
const radToDeg = (rad) => rad * (180 / Math.PI);
```

---

## 🧮 BigInt (Large Integers)

```JavaScript
const big = 12345678901234567890n;
```

- Use for very large integers
- Cannot mix directly with regular numbers

---

## ⚡ Quick Example

```JavaScript
const x = 5.7;  
  
console.log(Math.floor(x));   // 5  
console.log(Math.random());   // random number  
console.log(Math.sqrt(25));   // 5
```

---

## 🧩 Most Used Methods Summary

- `Math.random()`
- `Math.floor()`, `Math.ceil()`, `Math.round()`
- `Math.max()`, `Math.min()`
- `Math.sqrt()`, `Math.pow()`
- `Math.sin()`, `Math.cos()`
- `Math.log()`, `Math.exp()`

---

## ⚠️ Notes

- `Math.random()` is **not cryptographically secure**
- Trigonometry uses **radians, not degrees**
- Floating-point math can cause precision issues (`0.1 + 0.2 !== 0.3`)

---
