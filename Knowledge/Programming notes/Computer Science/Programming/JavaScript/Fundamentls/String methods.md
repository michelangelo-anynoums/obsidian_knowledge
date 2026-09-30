# 🔤 JavaScript String Methods

> [!summary] What are String Methods?  
> String methods are built-in tools that let you **work with text** in JavaScript.
> 
> ```js
> const name = "Alice";
> ```

---

## 📏 `length`

Returns the number of characters in a string.

```js
const text = "Hello";

console.log(text.length);
```

Output:

```text
5
```

> [!tip] Remember  
> `length` is a **property**, not a method — so don't use `()`.

---

## 🔠 `toUpperCase()` / `toLowerCase()`

Change the capitalization.

```js
const text = "Hello World";

console.log(text.toUpperCase());
console.log(text.toLowerCase());
```

Output:

```text
HELLO WORLD
hello world
```

---

## ✂️ `trim()`

Removes whitespace from the **beginning and end** of a string.

```js
const username = "   Alice   ";

console.log(username.trim());
```

Output:

```text
Alice
```

Very useful when handling user input.

---

## 🔎 `includes()`

Checks whether a string contains some text.

Returns `true` or `false`.

```js
const text = "I love JavaScript";

console.log(text.includes("JavaScript"));
```

Output:

```text
true
```

```js
console.log(text.includes("Python"));
```

Output:

```text
false
```

### 🧠 Think:

> **"Does this string contain this?"**

---

## 🎯 `startsWith()` / `endsWith()`

Check whether a string starts or ends with specific text.

```js
const file = "photo.jpg";

console.log(file.startsWith("photo"));
console.log(file.endsWith(".jpg"));
```

Output:

```text
true
true
```

---

## 🔍 `indexOf()`

Returns the position of the first occurrence of some text.

```js
const text = "Hello World";

console.log(text.indexOf("World"));
```

Output:

```text
6
```

If the text isn't found:

```js
console.log(text.indexOf("JavaScript"));
```

Output:

```text
-1
```

> [!tip] Remember  
> JavaScript indexes start at **0**.

```text
H e l l o
0 1 2 3 4
```

---

## ✂️ `slice()`

Extracts part of a string.

```js
const text = "JavaScript";

console.log(text.slice(0, 4));
```

Output:

```text
Java
```

You can also omit the ending position:

```js
console.log(text.slice(4));
```

Output:

```text
Script
```

### 🧠 Think:

> **"Give me a piece of this string."**

---

## 🔀 `split()`

Splits a string into an **array**.

```js
const fruits = "apple,banana,orange";

const result = fruits.split(",");

console.log(result);
```

Output:

```js
["apple", "banana", "orange"]
```

This is especially useful when combined with array methods:

```js
const names = "Alice,Bob,Charlie";

const result = names
  .split(",")
  .map(name => name.toUpperCase());

console.log(result);
```

Output:

```js
["ALICE", "BOB", "CHARLIE"]
```

---

## 🔗 `replace()` / `replaceAll()`

Replace text inside a string.

```js
const text = "I like cats";

console.log(text.replace("cats", "dogs"));
```

Output:

```text
I like dogs
```

`replace()` normally replaces the **first match**.

To replace all matches:

```js
const text = "cat cat cat";

console.log(text.replaceAll("cat", "dog"));
```

Output:

```text
dog dog dog
```

---

## 🔤 `charAt()`

Returns the character at a specific position.

```js
const text = "Hello";

console.log(text.charAt(1));
```

Output:

```text
e
```

You can also use bracket notation:

```js
console.log(text[1]);
```

Output:

```text
e
```

---

## ➕ `concat()`

Combines strings.

```js
const firstName = "John";
const lastName = "Smith";

const fullName = firstName.concat(" ", lastName);

console.log(fullName);
```

Output:

```text
John Smith
```

> [!tip] Modern JavaScript  
> Template literals are usually easier to read:

```js
const fullName = `${firstName} ${lastName}`;
```

---

## 🔢 `includes()` vs `indexOf()`

Both can check whether text exists:

```js
const text = "Hello World";

text.includes("World"); // true
text.indexOf("World");  // 6
```

### 🧠 Difference

- `includes()` → tells you **if it's there**
    
- `indexOf()` → tells you **where it is**
    

---

## 🧠 Quick Reference

|Method|Purpose|
|---|---|
|`length`|Get string length|
|`toUpperCase()`|Convert to uppercase|
|`toLowerCase()`|Convert to lowercase|
|`trim()`|Remove surrounding whitespace|
|`includes()`|Check if text exists|
|`startsWith()`|Check beginning|
|`endsWith()`|Check ending|
|`indexOf()`|Find position|
|`slice()`|Extract part of a string|
|`split()`|Convert string → array|
|`replace()`|Replace text|
|`replaceAll()`|Replace all occurrences|
|`charAt()`|Get a character|
|`concat()`|Combine strings|

---

## 🎯 Easy Way to Remember

```text
length       → 📏 How long?
toUpperCase  → 🔠 UPPERCASE
toLowerCase  → 🔡 lowercase
trim         → ✂️ Remove spaces
includes     → 🔎 Is it there?
startsWith   → ⬅️ Does it start with?
endsWith     → ➡️ Does it end with?
indexOf      → 📍 Where is it?
slice        → ✂️ Give me a piece
split        → 🔀 String → Array
replace      → 🔄 Change text
```

> [!important] One Important Thing  
> JavaScript strings are **immutable**. String methods don't change the original string; they return a new string.

```js
const text = "hello";

text.toUpperCase();

console.log(text);
```

Still:

```text
hello
```

To keep the changed version:

```js
const text = "hello";

const upperText = text.toUpperCase();

console.log(upperText);
```

Output:

```text
HELLO
```

### 🎯 In One Sentence

**String methods let you inspect, search, extract, modify, and transform text in JavaScript.**