# 🧩 Util — Useful Node.js Utilities

> 💡 **Goal:** Use built-in Node.js utilities to simplify debugging, asynchronous operations, data handling, and everyday development.

## 🐛 1. Debugging — `console`

Useful methods for inspecting application behavior.

```js
console.log("Server started");
console.error("Something went wrong");
console.warn("Warning!");
console.table([{ name: "John", age: 25 }]);
console.time("operation");

// Some operation...

console.timeEnd("operation");
```

- `log()` — General information.
- `error()` — Errors.
- `table()` — Display structured data.
- `time()` — Measure execution time.

## ⏳ 2. Promises — `Promise`

Handle asynchronous operations.

```js
const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) resolve("Done!");
  else reject(new Error("Failed"));
});

promise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log("Finished"));
```

**Modern approach — async/await**

```js
async function getData() {
  try {
    const result = await fetch("https://api.example.com/users");
    const data = await result.json();

    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

## 🔀 3. Promise Utilities

|Method|Purpose|
|---|---|
|`Promise.all()`|Wait for all promises|
|`Promise.allSettled()`|Wait for all, even if some fail|
|`Promise.race()`|First promise to settle|
|`Promise.any()`|First fulfilled promise|

```js
const results = await Promise.all([
  fetch("/users"),
  fetch("/products")
]);
```

⚠️ `Promise.all()` rejects if any promise rejects.

## ⏱️ 4. Timers

Execute code after a delay or repeatedly.

```js
// Run once after 2 seconds
setTimeout(() => {
  console.log("Hello!");
}, 2000);

// Repeat every second
const timer = setInterval(() => {
  console.log("Running...");
}, 1000);

// Stop interval
clearInterval(timer);
```

## 📂 5. Path — `node:path`

Work with file and directory paths.

```js
const path = require("node:path");

const file = "/app/data/users.json";

console.log(path.basename(file)); // users.json
console.log(path.dirname(file));  // /app/data
console.log(path.extname(file));  // .json

const fullPath = path.join(__dirname, "data", "users.json");
```

💡 `path.join()` handles platform-specific path separators.

## 📁 6. File System — `node:fs`

Read and write files.

```js
const fs = require("node:fs/promises");

// Read file
const data = await fs.readFile("users.json", "utf8");

// Write file
await fs.writeFile("output.txt", "Hello Node.js");

// Check if file exists
try {
  await fs.access("users.json");
  console.log("File exists");
} catch {
  console.log("File not found");
}
```

## 🆔 7. UUID — `crypto`

Generate unique identifiers.

```js
const crypto = require("node:crypto");

const id = crypto.randomUUID();

console.log(id);
// Example: 550e8400-e29b-41d4-a716-446655440000
```

Useful for:

- Database IDs.
- Request identifiers.
- Temporary resource identifiers.

## 🔐 8. Crypto — `node:crypto`

Hash data using cryptographic algorithms.

```js
const crypto = require("node:crypto");

const hash = crypto
  .createHash("sha256")
  .update("hello")
  .digest("hex");

console.log(hash);
```

⚠️ Passwords should use dedicated password-hashing algorithms such as Argon2 or bcrypt, not plain SHA-256.

## 🧹 9. Structured Data — `JSON`

Convert between JavaScript objects and JSON strings.

```js
const user = {
  name: "John",
  age: 25
};

// Object → JSON string
const json = JSON.stringify(user);

// JSON string → Object
const parsed = JSON.parse(json);

console.log(parsed.name);
```

## 🧪 10. Assert — `node:assert`

Check whether values match expectations.

```js
const assert = require("node:assert/strict");

assert.equal(2 + 2, 4);
assert.deepEqual(
  { name: "John" },
  { name: "John" }
);

console.log("All assertions passed");
```

Useful for debugging and automated tests.

## 🧵 11. Event Emitter — `node:events`

Create and listen for custom events.

```js
const EventEmitter = require("node:events");

const emitter = new EventEmitter();

emitter.on("userCreated", (user) => {
  console.log("New user:", user.name);
});

emitter.emit("userCreated", {
  name: "John"
});
```

- `on()` — Listen for an event.
- `emit()` — Trigger an event.
- `once()` — Listen only once.
- `off()` — Remove a listener.

## 📦 12. OS — `node:os`

Get information about the operating system.

```js
const os = require("node:os");

console.log(os.platform());
console.log(os.arch());
console.log(os.cpus().length);
console.log(os.totalmem());
console.log(os.freemem());
```

Useful for diagnostics and system monitoring.

---

## 🎯 Quick Reference

|Utility|Module|
|---|---|
|Debugging|`console`|
|Async operations|`Promise`|
|Timers|`setTimeout()`|
|File paths|`node:path`|
|File operations|`node:fs`|
|Unique IDs|`node:crypto`|
|Hashing|`node:crypto`|
|JSON|`JSON`|
|Assertions|`node:assert`|
|Events|`node:events`|
|System information|`node:os`|

💡 **Remember:** Node.js already provides many useful utilities. Before installing an npm package, check whether the built-in modules can solve the problem.

---
