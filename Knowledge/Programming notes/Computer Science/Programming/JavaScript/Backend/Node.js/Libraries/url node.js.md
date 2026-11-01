# 🔗 URL — Parse and Construct URLs

> 💡 Node.js provides the `URL` class to parse, inspect, modify and construct URLs.

## 📦 Import


```js
const { URL } = require('node:url');
```

## 1. 🔍 Parse a URL

Break a URL into its individual parts.

```js
const myURL = new URL('https://example.com:8080/users?id=10');

console.log(myURL.hostname); // example.com
console.log(myURL.port);     // 8080
console.log(myURL.pathname); // /users
console.log(myURL.search);   // ?id=10
console.log(myURL.protocol); // https:
```

## 2. 🏗️ Construct a URL

Create a URL from scratch.

```js
const myURL = new URL('https://example.com');

myURL.pathname = '/products';
myURL.searchParams.set('id', '25');

console.log(myURL.href);
// https://example.com/products?id=25
```

## 3. 🔎 Search Parameters

Use `searchParams` to read, add, update or delete query parameters.

```js
const myURL = new URL('https://example.com?name=John');

myURL.searchParams.get('name'); // John

myURL.searchParams.set('age', '30');
myURL.searchParams.delete('name');

console.log(myURL.href);
// https://example.com/?age=30
```

Useful methods:

|Method|Description|
|---|---|
|`.get()`|Get a parameter|
|`.set()`|Add or update|
|`.append()`|Add another value|
|`.delete()`|Remove a parameter|
|`.has()`|Check if it exists|

## 4. 🔗 Resolve Relative URLs

Combine a relative path with a base URL.

```js
const base = new URL('https://example.com/users/');

const result = new URL('profile', base);

console.log(result.href);
// https://example.com/users/profile
```

## 5. ⚡ Convert URL to String

```js
const myURL = new URL('https://example.com');

console.log(myURL.href);
console.log(myURL.toString());
```

Both return the complete URL as a string.

---

## 🧠 Remember

- `new URL()` → Parse or create URLs.
- `.hostname` → Get the domain.
- `.pathname` → Get the path.
- `.searchParams` → Work with query parameters.
- `.href` → Get the complete URL.
- `new URL(path, base)` → Resolve relative URLs.

📌 **Tip:** Prefer the modern `URL` class over the legacy `url.parse()` API.

---
