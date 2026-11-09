# 📦 Buffer — Handle Binary Data

> `Buffer` is a Node.js built-in class for working with raw binary data (bytes).

Useful for files, images, network streams, and encoding/decoding data.

## 1. Create a Buffer

```js
// From a string
const buf = Buffer.from("Hello");

// Allocate empty memory
const buf2 = Buffer.alloc(10);

// From an array of bytes
const buf3 = Buffer.from([72, 105]);

console.log(buf.toString()); // Hello
console.log(buf3.toString()); // Hi
```

## 2. Convert Between Encodings


```js
const buf = Buffer.from("Hello");

console.log(buf.toString("utf8")); // Hello
console.log(buf.toString("hex"));  // 48656c6c6f
console.log(buf.toString("base64")); // SGVsbG8=
```

Common encodings:

- `utf8` — text.
- `hex` — hexadecimal.
- `base64` — binary data represented as text.

## 3. Read & Write Bytes

```js
const buf = Buffer.alloc(4);

// Write values
buf.writeUInt8(65, 0);
buf.writeUInt8(66, 1);

// Read values
console.log(buf.readUInt8(0)); // 65
console.log(buf.readUInt8(1)); // 66
```

Each byte holds a value from `0` to `255`.

## 4. Buffer Properties & Methods

```js
const buf = Buffer.from("Node.js");

console.log(buf.length);        // 7
console.log(buf[0]);            // 78
console.log(buf.includes("Node")); // true
console.log(buf.subarray(0, 4).toString()); // Node
```

|Method|Purpose|
|---|---|
|`Buffer.from()`|Create from existing data|
|`Buffer.alloc()`|Create zero-filled buffer|
|`toString()`|Convert buffer to text|
|`write()`|Write text into buffer|
|`subarray()`|Get a portion of a buffer|
|`concat()`|Combine buffers|
|`byteLength()`|Get byte size of a value|

## 5. Combine Buffers


```js
const first = Buffer.from("Hello ");
const second = Buffer.from("World");

const combined = Buffer.concat([first, second]);

console.log(combined.toString()); // Hello World
```

## 6. Buffer vs String


```js
const text = "Hello";
const buffer = Buffer.from(text);

console.log(typeof text);     // string
console.log(Buffer.isBuffer(buffer)); // true
console.log(buffer.length);   // 5 bytes
```

- `String` → handles text.
- `Buffer` → handles raw bytes.

## 🧠 Remember

- Buffer is built into Node.js. No installation required.
- Binary data is stored as bytes.
- Commonly used with files, streams, images and network communication.
- Prefer `Buffer.alloc()` when allocating memory that should be initialized to zero.
- Avoid `Buffer.allocUnsafe()` unless you understand its security implications.

**Buffer = Working with raw bytes in Node.js.**

---
