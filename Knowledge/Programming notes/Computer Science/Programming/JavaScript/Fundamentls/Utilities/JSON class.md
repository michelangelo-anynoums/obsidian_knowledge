# 🧩 JSON in JavaScript

> [!abstract] 💡 What is JSON? **JSON** (JavaScript Object Notation) is a text format for storing and exchanging data.

## 📦 1. JSON Example

```json
{
  "name": "Alex",
  "age": 25,
  "isStudent": true,
  "skills": ["JavaScript", "HTML"],
  "address": {
    "city": "Madrid"
  }
}
```

- Keys must use **double quotes**.
- Values can be strings, numbers, booleans, `null`, arrays, or objects.
- JSON does not support functions or comments.

## 🔄 2. JavaScript Object ↔ JSON

### Object → JSON string

Use `JSON.stringify()`.

```js
const user = {
  name: "Alex",
  age: 25
};

const json = JSON.stringify(user);

console.log(json);
// '{"name":"Alex","age":25}'
```

### JSON string → Object

Use `JSON.parse()`.

```js
const json = '{"name":"Alex","age":25}';

const user = JSON.parse(json);

console.log(user.name); // "Alex"
console.log(user.age);  // 25
```

> [!tip] 🧠 Remember `stringify()` = Object ➡️ String
> 
> `parse()` = String ➡️ Object

## 🎨 3. Pretty-Print JSON

Add indentation with the third argument.

```js
const user = {
  name: "Alex",
  age: 25
};

console.log(JSON.stringify(user, null, 2));
```

Output:

```json
{
  "name": "Alex",
  "age": 25
}
```

## 🛡️ 4. Handle Invalid JSON

`JSON.parse()` throws an error if the string is invalid.

```js
try {
  const data = JSON.parse('{"name": "Alex"}');
  console.log(data);
} catch (error) {
  console.error("Invalid JSON:", error.message);
}
```

## 🧹 5. Select Properties

Use a replacer array to keep only specific properties.

```js
const user = {
  name: "Alex",
  age: 25,
  password: "12345"
};

const json = JSON.stringify(user, ["name", "age"]);

console.log(json);
// '{"name":"Alex","age":25}'
```

⚠️ For real applications, never rely on this alone to protect sensitive data.

## 💾 6. Save JSON in Local Storage

```js
const user = { name: "Alex", age: 25 };

// Save
localStorage.setItem("user", JSON.stringify(user));

// Load
const savedUser = JSON.parse(
  localStorage.getItem("user")
);

console.log(savedUser.name); // "Alex"
```

⚠️ `localStorage` stores strings, so objects need `JSON.stringify()` first.

## ⚡ 7. Quick Cheat Sheet

|Method|Purpose|
|---|---|
|`JSON.stringify(obj)`|Object → JSON string|
|`JSON.parse(str)`|JSON string → Object|
|`JSON.stringify(obj, null, 2)`|Format JSON|
|`localStorage.setItem()`|Save a string|
|`localStorage.getItem()`|Read a string|


---

> [!success] 🎯 Key takeaway JSON is a **data format**, not a JavaScript class.
> 
> The built-in `JSON` object provides methods to convert between JavaScript values and JSON text.


