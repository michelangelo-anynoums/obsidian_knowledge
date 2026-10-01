# 🔁 JavaScript `forEach()`

> **forEach()** runs a function once for **each item** in an array.

## Syntax

```js
array.forEach((item, index) => {
  // code
});
```

## Simple Example

```js
const fruits = ["🍎 Apple", "🍌 Banana", "🍊 Orange"];

fruits.forEach((fruit) => {
  console.log(fruit);
});
```

**Output:**

```text
🍎 Apple
🍌 Banana
🍊 Orange
```

## Using the Index

```js
fruits.forEach((fruit, index) => {
  console.log(index, fruit);
});
```

```text
0 🍎 Apple
1 🍌 Banana
2 🍊 Orange
```

## ⭐ Remember

- `forEach()` works with **arrays**
    
- It runs **once per item**
    
- It doesn't create a new array
    
- You **can't break** out of a forEach() loop
    
- Use `map()` when you want to **create a new array**
    

### 🧠 Easy way to remember

> **forEach = "Do this for every item."**

---
