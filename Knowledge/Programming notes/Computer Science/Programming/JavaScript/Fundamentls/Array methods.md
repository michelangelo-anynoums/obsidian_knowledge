# 📦 JavaScript — Array Methods

> [!summary] What is an Array?  
> An **array** is a collection of values stored in a single variable.
> 
> ```js
> const fruits = ["apple", "banana", "orange"];
> ```
> 
> Array methods help you **add, remove, search, transform, and work with elements**.

---

## ➕ `push()`

Adds an element to the **end** of an array.

```js
const fruits = ["apple", "banana"];

fruits.push("orange");

console.log(fruits);
```

Output:

```text
["apple", "banana", "orange"]
```

> 🧠 **push → add to the end**

---

## ➖ `pop()`

Removes the **last** element.

```js
const fruits = ["apple", "banana", "orange"];

fruits.pop();

console.log(fruits);
```

Output:

```text
["apple", "banana"]
```

> 🧠 **pop → remove from the end**

---

## ⬅️ `unshift()`

Adds an element to the **beginning**.

```js
const fruits = ["banana", "orange"];

fruits.unshift("apple");

console.log(fruits);
```

Output:

```text
["apple", "banana", "orange"]
```

---

## ➡️ `shift()`

Removes the **first** element.

```js
const fruits = ["apple", "banana", "orange"];

fruits.shift();

console.log(fruits);
```

Output:

```text
["banana", "orange"]
```

### 🧠 Easy to remember

```text
push()    → ➡️ add end
pop()     → ⬅️ remove end

unshift() → ⬅️ add beginning
shift()   → ➡️ remove beginning
```

---

## 🔎 `find()`

Returns the **first element** that matches a condition.

```js
const numbers = [5, 12, 8, 20];

const result = numbers.find(n => n > 10);

console.log(result);
```

Output:

```text
12
```

If nothing matches, it returns `undefined`.

> 🧠 **find → give me ONE matching item**

---

## 🔍 `filter()`

Returns **all elements** that match a condition.

```js
const numbers = [5, 12, 8, 20];

const result = numbers.filter(n => n > 10);

console.log(result);
```

Output:

```text
[12, 20]
```

> 🧠 **filter → give me ALL matching items**

---

## 🔄 `map()`

Creates a new array by **transforming every element**.

```js
const numbers = [1, 2, 3];

const doubled = numbers.map(n => n * 2);

console.log(doubled);
```

Output:

```text
[2, 4, 6]
```

> 🧠 **map → change every item**

---

## ➕ `reduce()`

Combines all elements into a **single result**.

```js
const numbers = [10, 20, 30];

const total = numbers.reduce((sum, n) => sum + n, 0);

console.log(total);
```

Output:

```text
60
```

> 🧠 **reduce → combine everything**

---

## 🔎 `includes()`

Checks whether an array contains a specific value.

```js
const fruits = ["apple", "banana", "orange"];

console.log(fruits.includes("banana"));
```

Output:

```text
true
```

---

## 📍 `indexOf()`

Returns the index of an element.

```js
const fruits = ["apple", "banana", "orange"];

console.log(fruits.indexOf("banana"));
```

Output:

```text
1
```

If it isn't found:

```js
fruits.indexOf("grape");
```

Returns:

```text
-1
```

---

## ✂️ `slice()`

Creates a **portion of an array** without changing the original.

```js
const numbers = [1, 2, 3, 4, 5];

const result = numbers.slice(1, 4);

console.log(result);
```

Output:

```text
[2, 3, 4]
```

> 🧠 **slice → take a piece**

---

## ✂️ `splice()`

Adds, removes, or replaces elements **inside the original array**.

```js
const fruits = ["apple", "banana", "orange"];

fruits.splice(1, 1);

console.log(fruits);
```

Output:

```text
["apple", "orange"]
```

The arguments mean:

```text
splice(start, deleteCount)
```

You can also insert:

```js
fruits.splice(1, 0, "banana");

console.log(fruits);
```

> [!warning] `slice()` vs `splice()`
> 
> - `slice()` → doesn't modify the original
>     
> - `splice()` → **modifies** the original
>     

---

## 🔀 `sort()`

Sorts the elements of an array.

```js
const numbers = [3, 1, 5, 2];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output:

```text
[1, 2, 3, 5]
```

For descending order:

```js
numbers.sort((a, b) => b - a);
```

> [!warning] Important  
> For numbers, use a comparison function. Without one, `sort()` sorts values as strings.

---

## 🔄 `reverse()`

Reverses the order of an array.

```js
const numbers = [1, 2, 3, 4];

numbers.reverse();

console.log(numbers);
```

Output:

```text
[4, 3, 2, 1]
```

---

## 🔗 `join()`

Converts an array into a **string**.

```js
const fruits = ["apple", "banana", "orange"];

const result = fruits.join(", ");

console.log(result);
```

Output:

```text
apple, banana, orange
```

> 🧠 **join → Array → String**

---

## 🔀 `concat()`

Combines arrays.

```js
const fruits = ["apple", "banana"];
const vegetables = ["carrot", "potato"];

const food = fruits.concat(vegetables);

console.log(food);
```

Output:

```text
["apple", "banana", "carrot", "potato"]
```

You can also use the spread operator:

```js
const food = [...fruits, ...vegetables];
```

---

## 📏 `length`

Returns the number of elements.

```js
const fruits = ["apple", "banana", "orange"];

console.log(fruits.length);
```

Output:

```text
3
```

> [!tip] Remember  
> Like strings, `length` is a **property**, not a method.

---

## 🔗 Chaining Methods

Array methods can be combined.

```js
const numbers = [1, 2, 3, 4, 5];

const result = numbers
  .filter(n => n > 2)
  .map(n => n * 10);

console.log(result);
```

Output:

```text
[30, 40, 50]
```

### What's happening?

```text
[1, 2, 3, 4, 5]
        ↓ filter
    [3, 4, 5]
        ↓ map
  [30, 40, 50]
```

---

## 🧠 Quick Reference

|Method|Purpose|
|---|---|
|`push()`|Add to the end|
|`pop()`|Remove from the end|
|`unshift()`|Add to the beginning|
|`shift()`|Remove from the beginning|
|`find()`|Find the first matching element|
|`filter()`|Find all matching elements|
|`map()`|Transform every element|
|`reduce()`|Combine elements into one result|
|`includes()`|Check if value exists|
|`indexOf()`|Find an element's position|
|`slice()`|Copy/extract part of an array|
|`splice()`|Add/remove elements|
|`sort()`|Sort elements|
|`reverse()`|Reverse elements|
|`join()`|Array → String|
|`concat()`|Combine arrays|
|`length`|Get number of elements|

---

# 🧰 JavaScript — Array Static Methods

> [!summary] What are Static Array Methods?  
> Static methods are called directly on the **Array class**, rather than on an array itself.
> 
> ```js
> Array.from(...)
> Array.isArray(...)
> Array.of(...)
> ```
> 
> They are especially useful for **converting values into arrays** and checking whether something is an array.

---

## 🔄 `Array.from()`

Converts an **iterable** or **array-like object** into a real array.

### String → Array

```js
const text = "Hello";

const letters = Array.from(text);

console.log(letters);
```

Output:

```text
["H", "e", "l", "l", "o"]
```

### Set → Array

```js
const numbers = new Set([1, 2, 3]);

const array = Array.from(numbers);

console.log(array);
```

Output:

```text
[1, 2, 3]
```

### NodeList → Array

Very useful when working with the DOM:

```js
const elements = document.querySelectorAll("p");

const paragraphs = Array.from(elements);
```

Now `paragraphs` is a regular array.

### 🧠 Think:

> **Array.from() → "Turn this into an array."**

---

## 🔢 `Array.from()` with a Transformation

`Array.from()` can also transform each element.

```js
const numbers = Array.from([1, 2, 3], n => n * 2);

console.log(numbers);
```

Output:

```text
[2, 4, 6]
```

This can sometimes be useful instead of:

```js
[1, 2, 3].map(n => n * 2);
```

---

## ❓ `Array.isArray()`

Checks whether a value is actually an array.

```js
const fruits = ["apple", "banana"];

console.log(Array.isArray(fruits));
```

Output:

```text
true
```

Another example:

```js
console.log(Array.isArray("hello"));
```

Output:

```text
false
```

### 🧠 Think:

> **"Is this an array?"**

---

## 🏗️ `Array.of()`

Creates an array from the values you provide.

```js
const numbers = Array.of(1, 2, 3);

console.log(numbers);
```

Output:

```text
[1, 2, 3]
```

This is particularly useful for understanding the difference between:

```js
Array.of(5);
```

and:

```js
new Array(5);
```

The first creates:

```text
[5]
```

The second creates an array with **5 empty slots**:

```text
[empty × 5]
```

> [!tip] Simple rule  
> For creating an array from individual values, `Array.of()` avoids the special behavior of `new Array(number)`.

---

## 🔢 `Array()`

You can also create an array directly using the `Array` constructor.

```js
const fruits = Array("apple", "banana", "orange");

console.log(fruits);
```

Output:

```text
["apple", "banana", "orange"]
```

However, for everyday code, array literals are usually clearer:

```js
const fruits = ["apple", "banana", "orange"];
```

---

## 🔗 `Array.from()` vs `Array.of()`

These two are easy to confuse.

### `Array.from()`

**Converts something into an array:**

```js
Array.from("ABC");
// ["A", "B", "C"]
```

### `Array.of()`

**Creates an array from the supplied values:**

```js
Array.of("A", "B", "C");
// ["A", "B", "C"]
```

### 🧠 Remember

```text
Array.from() → 🔄 CONVERT
Array.of()   → 🏗️ CREATE
```

---

## 🧩 Useful Example

Imagine you receive a `Set` containing unique numbers:

```js
const uniqueNumbers = new Set([10, 20, 30]);

const numbers = Array.from(uniqueNumbers);

const doubled = numbers.map(n => n * 2);

console.log(doubled);
```

Output:

```text
[20, 40, 60]
```

Here we're combining a **static method** with an **array instance method**:

```text
Set
 ↓
Array.from()
 ↓
Array
 ↓
.map()
 ↓
Transformed Array
```

---

## 🧠 Quick Reference

|Static Method|Purpose|
|---|---|
|`Array.from()`|Convert an iterable/array-like value → array|
|`Array.isArray()`|Check whether a value is an array|
|`Array.of()`|Create an array from supplied values|
|`Array()`|Create an array|

---

## 🎯 Array Methods vs Array Static Methods

This distinction is important:

### Instance methods

Called **on an array**:

```js
const numbers = [1, 2, 3];

numbers.map(...)
numbers.filter(...)
numbers.find(...)
numbers.includes(...)
```

### Static methods

Called **on `Array`**:

```js
Array.from(...)
Array.isArray(...)
Array.of(...)
```

### 🧠 Easy Way to Remember

```text
array.method()
     ↓
Works with an existing array

Array.method()
     ↓
Works with/creates/checks arrays
```

> [!important] Most Useful Conversion  
> If you're wondering **"How do I turn this thing into an array?"**, the method to remember first is:
> 
> ```js
> Array.from(value)
> ```
> 
> It is commonly used with strings, Sets, Maps, NodeLists, and other iterable or array-like values.

### 🎯 In One Sentence

**Static `Array` methods let you create arrays, convert other data into arrays, and check whether a value is an array.**


---

## 🎯 Easy Way to Remember

```text
push     → ➕ Add end
pop      → ➖ Remove end
unshift  → ➕ Add beginning
shift    → ➖ Remove beginning

find     → 🔎 ONE
filter   → 🔎 MANY
map      → 🔄 CHANGE
reduce   → ➕ COMBINE

includes → ❓ Does it exist?
indexOf  → 📍 Where is it?
slice    → ✂️ Take a piece
splice   → 🛠️ Change the array

sort     → 📊 Order
reverse  → 🔄 Reverse
join     → 🔤 Array → String
concat   → 🔗 Combine
```

> [!important] Mutation  
> Some array methods **change the original array**, while others return a new result.
> 
> **Usually mutates:** `push()`, `pop()`, `shift()`, `unshift()`, `splice()`, `sort()`, `reverse()`
> 
> **Usually returns a new result:** `map()`, `filter()`, `slice()`, `concat()`

### 🎯 In One Sentence

**Array methods give you simple tools to add, remove, search, transform, combine, and organize data in arrays.**

