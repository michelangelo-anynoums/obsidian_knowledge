# 🟣 JavaScript — Set Methods

> [!abstract] Overview A **Set** is a collection of unique values. It automatically prevents duplicate values and is useful for removing duplicates or checking whether a value exists.

## 1. ✨ Creating a Set

```js
const fruits = new Set(["apple", "banana", "apple"]);

console.log(fruits);
// Set(2) { "apple", "banana" }
```

The duplicate `"apple"` is automatically removed.

## 2. 🛠️ Essential Methods

### `.add()` — Add a value

```js
fruits.add("orange");
fruits.add("banana"); // Already exists

console.log(fruits.size); // 3
```

Adds a value only if it isn't already present.

### `.has()` — Check for a value

```js
fruits.has("apple");  // true
fruits.has("grape");  // false
```

Returns `true` if the value exists, otherwise `false`.

### `.delete()` — Remove a value

```js
fruits.delete("banana");

console.log(fruits.has("banana")); // false
```

Returns `true` if the value was found and deleted.

### `.clear()` — Remove everything

```js
fruits.clear();

console.log(fruits.size); // 0
```

Empties the entire Set.

## 3. 📏 The `.size` Property

Returns the number of unique values.

```js
const numbers = new Set([1, 2, 2, 3, 3]);

console.log(numbers.size); // 3
```

Remember: `size` is a property, not a method. Use `numbers.size`, not `numbers.size()`.

## 4. 🔄 Iterating Over a Set

```js
const colors = new Set(["red", "green", "blue"]);

for (const color of colors) {
  console.log(color);
}
```

A Set preserves insertion order when iterating.

## 5. 🚀 A Common Real-World Use

### Removing duplicates from an array

```js
const numbers = [1, 2, 2, 3, 3, 4];

const uniqueNumbers = [...new Set(numbers)];

console.log(uniqueNumbers);
// [1, 2, 3, 4]
```

`Set` removes duplicates, and the spread operator (`...`) converts it back into an array.

## 📌 Quick Reference

| Method / Property | Purpose                         |
| ----------------- | ------------------------------- |
| `new Set()`       | Create a Set                    |
| `.add(value)`     | Add a value                     |
| `.has(value)`     | Check if a value exists         |
| `.delete(value)`  | Remove one value                |
| `.clear()`        | Remove all values               |
| `.size`           | Get the number of unique values |

> [!tip] Remember **Set = unique values.** Use it when duplicates are unwanted and you need a convenient way to check membership.

---
