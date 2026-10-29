# 🧩 Buffer in Node.js

> [!abstract] 💡 What is a Buffer? A `Buffer` stores **raw binary data** as bytes. Useful for files, streams, network packets, and binary data.

## ⚡ Create a Buffer

```js
// From text
const buf = Buffer.from("Hello");

// From an array of bytes
const bytes = Buffer.from([65, 66, 67]);

// Allocate 10 bytes (initialized to zero)
const empty = Buffer.alloc(10);
```

## 🔤 Convert to text

```js
const buf = Buffer.from("Hello, Node.js!");

console.log(buf.toString());
// "Hello, Node.js!"

console.log(buf.toString("hex"));
// "48656c6c6f2c204e6f64652e6a7321"
```

## 🔢 Read bytes


```js
const buf = Buffer.from("ABC");

console.log(buf.length); // 3 bytes
console.log(buf[0]);     // 65 (A)
console.log(buf[1]);     // 66 (B)
```

> [!improtant] Each character here uses one byte in UTF-8.

## ✏️ Modify a Buffer

```js
const buf = Buffer.from("ABC");

buf[0] = 88;

console.log(buf.toString());
// "XBC"
```

> [!fire] Buffers are **mutable**.

## ✂️ Slice a Buffer

```js
const buf = Buffer.from("Hello");

const part = buf.subarray(0, 2);

console.log(part.toString());
// "He"
```

> [!question] ⚠️ `subarray()` shares the original memory. Changing `part` can change `buf`.

## 📁 Read a file

```js
import { readFile } from "node:fs/promises";

const data = await readFile("image.png");

console.log(Buffer.isBuffer(data)); // true
console.log(data.length);           // Size in bytes
```

Node.js returns file contents as a `Buffer` when no encoding is specified.

## 🔄 Buffer ↔ JSON


```js
const buf = Buffer.from("Hi");

const json = buf.toJSON();

console.log(json);
// { type: "Buffer", data: [72, 105] }

const restored = Buffer.from(json.data);

console.log(restored.toString());
// "Hi"
```

## 🛡️ Important

- `Buffer.from(text)` — create from existing data.
- `Buffer.alloc(size)` — allocate zero-filled memory.
- `buf.length` — number of bytes, not necessarily characters.
- `buf.toString()` — decode bytes into text.
- `Buffer` is a subclass of `Uint8Array`.

**🧠 Remember:** Strings represent text; Buffers represent bytes.

---
