# 🔢 JavaScript — Number & Integer Methods

> [!summary] Numbers in JavaScript  
> JavaScript uses the **Number** type for both integers and decimal numbers.
> 
> ```js
> const age = 25;
> const price = 19.99;
> ```
> 
> The methods below are useful for rounding, checking, converting, and working with numbers.

---

## 🔢 `Number.isInteger()`

Checks whether a value is an integer.

Returns `true` or `false`.

```js
Number.isInteger(10);
```

Output:

```text
true
```

```js
Number.isInteger(10.5);
```

Output:

```text
false
```

### 🧠 Think:

> **"Is this a whole number?"**

---

## 🔍 `Number.isNaN()`

Checks whether a value is `NaN` (**Not a Number**).

```js
Number.isNaN(10);
```

Output:

```text
false
```

```js
Number.isNaN(NaN);
```

Output:

```text
true
```

> [!tip] Remember  
> `NaN` means JavaScript couldn't produce a valid numeric result.

---

## 🔄 `Number()`

Converts a value into a number.

```js
const age = "25";

const number = Number(age);

console.log(number);
```

Output:

```text
25
```

This is particularly useful when getting numbers from user input, because input values are often strings.

```js
const input = "42";

console.log(typeof input);          // "string"
console.log(typeof Number(input));  // "number"
```

---

## 🔢 `parseInt()`

Converts a string into an **integer**.

```js
const value = "25px";

const number = parseInt(value);

console.log(number);
```

Output:

```text
25
```

It stops when it reaches something that isn't part of the integer.

```js
parseInt("42.9");
```

Output:

```text
42
```

### 🧠 Think:

> **parseInt() → "Give me the whole number."**

---

## 🔢 `parseFloat()`

Converts a string into a **decimal number**.

```js
const value = "19.99";

const number = parseFloat(value);

console.log(number);
```

Output:

```text
19.99
```

Compare:

```js
parseInt("19.99");   // 19
parseFloat("19.99"); // 19.99
```

---

## ⬇️ `Math.floor()`

Rounds a number **down**.

```js
Math.floor(4.9);
```

Output:

```text
4
```

```js
Math.floor(4.1);
```

Output:

```text
4
```

### 🧠 Think:

> **floor() → go down**

---

## ⬆️ `Math.ceil()`

Rounds a number **up**.

```js
Math.ceil(4.1);
```

Output:

```text
5
```

```js
Math.ceil(4.9);
```

Output:

```text
5
```

### 🧠 Think:

> **ceil() → go up**

---

## 🎯 `Math.round()`

Rounds to the **nearest integer**.

```js
Math.round(4.4);
```

Output:

```text
4
```

```js
Math.round(4.6);
```

Output:

```text
5
```

### 🧠 Quick comparison

```text
4.1 → floor → 4
4.1 → ceil  → 5
4.1 → round → 4

4.6 → floor → 4
4.6 → ceil  → 5
4.6 → round → 5
```

---

## ✂️ `Math.trunc()`

Removes the decimal part without rounding.

```js
Math.trunc(4.9);
```

Output:

```text
4
```

```js
Math.trunc(4.1);
```

Output:

```text
4
```

### 🧠 Difference from `Math.floor()`

With positive numbers they look similar:

```js
Math.floor(4.9); // 4
Math.trunc(4.9); // 4
```

But with negative numbers:

```js
Math.floor(-4.9); // -5
Math.trunc(-4.9); // -4
```

---

## 🎲 `Math.random()`

Generates a random decimal number between **0 (inclusive)** and **1 (exclusive)**.

```js
console.log(Math.random());
```

Possible output:

```text
0.738291
```

### Random integer

To generate a random integer from `1` to `10`:

```js
const randomNumber = Math.floor(Math.random() * 10) + 1;

console.log(randomNumber);
```

Possible result:

```text
7
```

---

## 📐 `Math.max()` / `Math.min()`

Find the largest or smallest number.

```js
Math.max(10, 5, 20, 8);
```

Output:

```text
20
```

```js
Math.min(10, 5, 20, 8);
```

Output:

```text
5
```

---

## 🔢 `toFixed()`

Formats a number to a specific number of decimal places.

```js
const price = 19.567;

console.log(price.toFixed(2));
```

Output:

```text
19.57
```

> [!warning] Important  
> `toFixed()` returns a **string**, not a number.

```js
const result = (19.567).toFixed(2);

console.log(typeof result);
```

Output:

```text
string
```

---

## 🧠 Quick Reference

|Method|Purpose|
|---|---|
|`Number.isInteger()`|Check if a number is an integer|
|`Number.isNaN()`|Check for `NaN`|
|`Number()`|Convert to a number|
|`parseInt()`|Convert to an integer|
|`parseFloat()`|Convert to a decimal|
|`Math.floor()`|Round down|
|`Math.ceil()`|Round up|
|`Math.round()`|Round to nearest integer|
|`Math.trunc()`|Remove decimal part|
|`Math.random()`|Generate random number|
|`Math.max()`|Find largest number|
|`Math.min()`|Find smallest number|
|`toFixed()`|Format decimal places|

---

## 🎯 Easy Way to Remember

```text
isInteger → 🔢 Is it a whole number?
Number    → 🔄 Convert to number
parseInt  → 🔢 Get integer
parseFloat → 🔢 Get decimal

floor → ⬇️ Down
ceil  → ⬆️ Up
round → 🎯 Nearest
trunc → ✂️ Remove decimal

max → 🔝 Biggest
min → 🔻 Smallest
random → 🎲 Random
toFixed → 💰 Decimal places
```

> [!important] One Important Difference  
> `parseInt()` and `parseFloat()` are useful for **parsing strings**, while `Math.floor()`, `Math.ceil()`, and `Math.round()` are used for **rounding numbers**.

### 🎯 In One Sentence

**JavaScript's number methods help you check, convert, round, format, and generate numbers.**