# 🔎 JavaScript — `find()`

> [!summary] What is `find()`?  
> `find()` searches an array and returns the **first element** that matches a condition.

### 🧠 Think of it as:

> **"Find me the first item that matches."**

---

## 🔍 Basic Example

```js
const numbers = [1, 2, 3, 4, 5];

const result = numbers.find(number => number > 3);

console.log(result);
```

Output:

```text
4
```

`find()` stops as soon as it finds the **first match**.

---

## 👤 Example with Objects

```js
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
  { id: 3, name: "Charlie" }
];

const user = users.find(user => user.id === 2);

console.log(user);
```

Output:

```js
{ id: 2, name: "Bob" }
```

You can then access its properties:

```js
console.log(user.name);
```

Output:

```text
Bob
```

---

## ❌ What if Nothing Matches?

If `find()` can't find a matching element, it returns:

```js
undefined
```

Example:

```js
const numbers = [1, 2, 3];

const result = numbers.find(number => number > 10);

console.log(result);
```

Output:

```text
undefined
```

---

## ⚖️ `find()` vs `filter()`

This is an important difference:

```js
const numbers = [1, 2, 3, 4, 5];

const first = numbers.find(n => n > 2);
const all = numbers.filter(n => n > 2);
```

Results:

```js
first // 3

all // [3, 4, 5]
```

### 🧠 Easy Way to Remember

|Method|Returns|
|---|---|
|`find()`|**First matching element**|
|`filter()`|**All matching elements**|

```text
find   → 🔎 ONE
filter → 🔎🔎🔎 MANY
```

---

## 🎯 Common Use Case

`find()` is particularly useful when looking for an object by an ID:

```js
const products = [
  { id: 101, name: "Laptop" },
  { id: 102, name: "Phone" },
  { id: 103, name: "Tablet" }
];

const product = products.find(product => product.id === 102);

console.log(product.name);
```

Output:

```text
Phone
```

> [!tip] Remember  
> `find()` returns the **element itself**, not its index.
> 
> If you need the position/index of the matching element, use **findIndex()**.

### 🧩 Quick Reference

```js
array.find(item => condition);
```

**Returns:**

- ✅ First matching element
    
- ❌ `undefined` if no match
    

### 🎯 In One Sentence

**find() searches an array and gives you the first element that satisfies your condition.**