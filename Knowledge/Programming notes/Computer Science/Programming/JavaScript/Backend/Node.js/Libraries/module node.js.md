# 🧰 Node.js Modules

> [!abstract] 🎯 What are modules? Modules let you **split your code into separate files** and reuse functionality across your application.

## 📦 1. Export a module

Use `module.exports` to make code available to other files.

**math.js**

```js
const add = (a, b) => a + b;

module.exports = { add };
```

## 📥 2. Import a module

Use `require()` to load another module.

**app.js**

```js
const math = require('./math');

console.log(math.add(5, 3)); // 8
```

## 🔄 3. Export multiple values

```js
// utils.js
const name = 'Node.js';
const version = 22;

module.exports = { name, version };
```

```js

// app.js
const { name, version } = require('./utils');

console.log(name, version);
```

## ⚙️ 4. Built-in modules

Node.js includes modules ready to use. No installation required.

```js
const fs = require('node:fs');
const path = require('node:path');
const os = require('node:os');
```

|Module|Purpose|
|---|---|
|`fs` 📁|Work with files|
|`path` 🛣️|Handle file paths|
|`os` 💻|Get system information|
|`http` 🌐|Create HTTP servers|
|`events` ⚡|Handle events|

**Example — Read a file:**

```js
const fs = require('node:fs');

const data = fs.readFileSync('hello.txt', 'utf8');

console.log(data);
```

## 🆕 5. ES Modules (import / export)

Modern alternative to `require()`.

```js
// math.js
export const add = (a, b) => a + b;
```

```js
// app.js
import { add } from './math.js';

console.log(add(2, 3)); // 5
```

Enable ES Modules using `"type": "module"` in `package.json`.

---

## 🔗 References

- [Node.js — Modules](https://nodejs.org/api/modules.html)
- [Node.js — ECMAScript Modules](https://nodejs.org/api/esm.html) 

---
