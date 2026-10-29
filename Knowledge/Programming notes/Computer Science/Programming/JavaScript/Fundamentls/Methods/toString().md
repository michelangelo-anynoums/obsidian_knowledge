# 🔤 `toString()` in JavaScript & Node.js

> [!abstract] 💡 What is it? `toString()` converts a value into a **string**. Its behavior depends on the object that calls it.

## 🧩 Buffer

Converts binary bytes into readable text.

```js
const buf = Buffer.from("Hello");

buf.toString();      // "Hello"
buf.toString("hex"); // "48656c6c6f"
buf.toString("base64"); // "SGVsbG8="
```

## 📦 Common objects

### 📝 String

```js
const text = "Hello";

text.toString(); // "Hello"
```

### 🔢 Number

```js
(42).toString();    // "42"
(255).toString(16); // "ff" (hexadecimal)
```

### ✅ Boolean

```js
true.toString();  // "true"
false.toString(); // "false"
```

### 📚 Array

```js
[1, 2, 3].toString(); // "1,2,3"
["a", "b"].toString(); // "a,b"
```

### 🗓️ Date


```js
const date = new Date("2026-01-01");

date.toString();
// Human-readable date and time
```

### 🧱 Plain object

```js
const user = { name: "Alex" };

user.toString(); // "[object Object]"
```

For JSON, use `JSON.stringify()` instead.

```js
JSON.stringify(user);
// '{"name":"Alex"}'
```

## ⚙️ Where does `toString()` come from?

Most JavaScript objects inherit `toString()` from `Object.prototype`. Some types override it with their own behavior.

|Type|Typical result|
|---|---|
|`Buffer`|Decoded text|
|`Number`|Numeric text|
|`Boolean`|`"true"` / `"false"`|
|`Array`|Comma-separated values|
|`Date`|Date and time text|
|Plain object|`"[object Object]"`|

---
