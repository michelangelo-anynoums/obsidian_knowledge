# ⚡ JavaScript — `filter()`, `map()` & `reduce()`

> [!summary] The Big Idea  
> These three methods are commonly used to work with **arrays**:
> 
> - `filter()` → **keep** certain items
>     
> - `map()` → **transform** every item
>     
> - `reduce()` → **combine** items into one result
>     

---

## 🔎 `filter()`

`filter()` creates a **new array** containing only the elements that pass a condition.

### Example

```js
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

### 🧠 Think of it as:

> **"Which items should I keep?"**

```js
array.filter(item => condition);
```

### Example with objects

```js
const users = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 17 },
  { name: "Charlie", age: 30 }
];

const adults = users.filter(user => user.age >= 18);

console.log(adults);
```

Result:

```text
Alice
Charlie
```

---

## 🔄 `map()`

`map()` creates a **new array** by transforming every element.

### Example

```js
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

### 🧠 Think of it as:

> **"Change every item into something else."**

```js
array.map(item => transformation);
```

### Example with objects

```js
const users = [
  { name: "Alice" },
  { name: "Bob" },
  { name: "Charlie" }
];

const names = users.map(user => user.name);

console.log(names);
```

Output:

```text
["Alice", "Bob", "Charlie"]
```

---

## ➕ `reduce()`

`reduce()` processes all elements and **reduces them to a single value**.

### Example

```js
const numbers = [1, 2, 3, 4];

const total = numbers.reduce(
  (sum, number) => sum + number,
  0
);

console.log(total);
```

Output:

```text
10
```

### 🧠 Think of it as:

> **"Combine everything into one result."**

```js
array.reduce((accumulator, item) => {
  return accumulator + item;
}, initialValue);
```

The `0` is the **initial value**.

### Another example

Find the total price:

```js
const prices = [10, 20, 30];

const total = prices.reduce(
  (sum, price) => sum + price,
  0
);

console.log(total);
```

Output:

```text
60
```

---

## 🔗 Using Them Together

You can combine these methods.

For example, get the total price of products that cost more than €10:

```js
const prices = [5, 15, 20, 8, 30];

const total = prices
  .filter(price => price > 10)
  .reduce((sum, price) => sum + price, 0);

console.log(total);
```

Output:

```text
65
```

### What's happening?

```text
[5, 15, 20, 8, 30]
        ↓
      filter
        ↓
  [15, 20, 30]
        ↓
     reduce
        ↓
       65
```

---

## 🧠 Quick Reference

|Method|What it does|Returns|
|---|---|---|
|`filter()`|Keeps elements that pass a condition|New array|
|`map()`|Transforms every element|New array|
|`reduce()`|Combines elements|Usually one value|

### 🎯 Easy Way to Remember

```text
filter → KEEP
map    → CHANGE
reduce → COMBINE
```

> [!tip] Important  
> All three methods **return a new result** and normally don't modify the original array.

### 🧩 Mini Challenge

Try to predict the result:

```js
const numbers = [1, 2, 3, 4, 5];

const result = numbers
  .filter(n => n > 2)
  .map(n => n * 10)
  .reduce((sum, n) => sum + n, 0);

console.log(result);
```

**Answer:** `120`

Because:

```text
[1, 2, 3, 4, 5]
       ↓ filter
   [3, 4, 5]
       ↓ map
 [30, 40, 50]
       ↓ reduce
      120
```