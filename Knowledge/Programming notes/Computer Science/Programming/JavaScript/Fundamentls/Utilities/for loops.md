# 🔁 JavaScript — `for` Loops

A `for` loop repeats a block of code while a condition is `true`.

## 1. Basic `for` Loop

Use it when you know how many times you want to repeat something.

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

**Output:** `0 1 2 3 4`

- `let i = 0` → Start
- `i < 5` → Condition
- `i++` → Increase by 1

## 2. Loop Through an Array

Use it to access array elements by index.

```js
const fruits = ["Apple", "Banana", "Orange"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

## 3. Count Backwards

Use `i--` to decrease the counter.

```js
for (let i = 5; i > 0; i--) {
  console.log(i);
}
```

**Output:** `5 4 3 2 1`

## 4. Skip Steps

Use `i += 2` to increase by 2 each time.

```js
for (let i = 0; i <= 10; i += 2) {
  console.log(i);
}
```

**Output:** `0 2 4 6 8 10`

## 5. `for...of` Loop

Use it to iterate directly over the values of an array or other iterable.

```js
const colors = ["Red", "Green", "Blue"];

for (const color of colors) {
  console.log(color);
}
```

## 6. `for...in` Loop

Use it to iterate over an object's enumerable property keys.

```js
const person = {
  name: "Alex",
  age: 25
};

for (const key in person) {
  console.log(key, person[key]);
}
```

**Output:**

```
name Alex
age 25
```

## 💡 Quick Reminder

|Loop|Best used for|
|---|---|
|`for`|Counting and working with indexes|
|`for...of`|Iterating over values|
|`for...in`|Iterating over object keys|

**Remember:** Use `break` to stop a loop early and `continue` to skip the current iteration.

---
