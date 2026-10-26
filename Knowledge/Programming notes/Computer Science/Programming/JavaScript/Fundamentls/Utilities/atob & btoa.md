# 🔐 JavaScript — `btoa()` & `atob()`

> [!abstract] Overview `btoa()` and `atob()` are built-in JavaScript functions used to **encode and decode Base64 strings**.

## 🧩 1. `btoa()` — Encode

`btoa()` converts a string into a **Base64-encoded string**.

**Syntax**

```js
btoa(string);
```

**Example**

```js
const text = "Hello World";
const encoded = btoa(text);

console.log(encoded);
// SGVsbG8gV29ybGQ=
```

💡 Think of `btoa()` as turning text into a Base64 representation.

## 🔓 2. `atob()` — Decode

`atob()` converts a Base64-encoded string back into its original binary string representation.

**Syntax**

```js
atob(string);
```

**Example**

```js
const encoded = "SGVsbG8gV29ybGQ=";
const decoded = atob(encoded);

console.log(decoded);
// Hello World
```

💡 Think of `atob()` as reversing the Base64 encoding performed by `btoa()`.

## 🔄 3. How They Work Together

```js
const original = "Hello World";

// Encode
const encoded = btoa(original);

// Decode
const decoded = atob(encoded);

console.log(encoded); // SGVsbG8gV29ybGQ=
console.log(decoded); // Hello World
```

**The process:**

`Original Text` → `btoa()` → `Base64` → `atob()` → `Original Text`

## 📌 4. Important Things to Remember

- **Base64 is not encryption.** It does not protect secrets or passwords.
- **ASCII-compatible characters:** `btoa()` works directly with strings whose characters fit within the Latin-1 byte range (code points 0–255).
- **Unicode characters:** Emojis and many other characters require UTF-8 conversion before encoding.
- **Browser support:** Both functions are widely available in web browsers and Web Workers.
- **Node.js:** Use `Buffer` for Base64 conversion when working in Node.js.

### 🌍 Handling Unicode

For text containing emojis or other Unicode characters, convert the text to UTF-8 bytes first:

```js
const text = "Hello 🌍";

// Encode Unicode text
const encoded = btoa(
  String.fromCharCode(...new TextEncoder().encode(text))
);

// Decode Unicode text
const bytes = Uint8Array.from(
  atob(encoded),
  char => char.charCodeAt(0)
);

const decoded = new TextDecoder().decode(bytes);

console.log(decoded); // Hello 🌍
```

## 🧠 Quick Summary

|Function|Purpose|Example|
|---|---|---|
|`btoa()`|Encode to Base64|`btoa("Hi")` → `"SGk="`|
|`atob()`|Decode from Base64|`atob("SGk=")` → `"Hi"`|

> [!tip] Easy way to remember - **B** in `btoa` → **Binary to ASCII** (Base64 encoding). - **A** in `atob` → **ASCII to Binary** (Base64 decoding).

> [!warning] Security reminder Base64 is an encoding format, not a security mechanism. Never rely on it to hide sensitive information.

---

**Tags:** #JavaScript #Base64 #WebDevelopment #Encoding #Decoding