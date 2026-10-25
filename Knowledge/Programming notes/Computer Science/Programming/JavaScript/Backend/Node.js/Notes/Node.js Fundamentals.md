# 🟢 02 — Node.js Fundamentals

> [!abstract] The Big Picture **Node.js** runs JavaScript outside the browser. Build APIs, servers, CLI tools, and background jobs with it.

```js
JavaScript → Node.js → Operating System
                ├── Files
                ├── Network
                ├── Processes
                └── Servers
```

---

## 01 — Runtime Architecture

Node.js combines the V8 JavaScript engine with native system APIs and `libuv`.

|Component|Purpose|
|---|---|
|**V8**|Executes JavaScript|
|**libuv**|Async I/O, event loop, thread pool|
|**Event Loop**|Coordinates callbacks and async work|
|**Node APIs**|Files, network, processes, etc.|

### Event Loop

```js
console.log("1. Start");

setTimeout(() => console.log("3. Timer"), 0);

console.log("2. End");
```

**Output:**

```
1. Start
2. End
3. Timer
```

> [!tip] Remember Asynchronous operations let Node.js handle other work while waiting for I/O. CPU-heavy JavaScript can still block the event loop.

---

## 02 — Modules

### CommonJS (CJS)

```js
// math.js
function add(a, b) {
  return a + b;
}

module.exports = { add };
```

```js
// app.js
const { add } = require("./math");

console.log(add(2, 3)); // 5
```

### ES Modules (ESM)

```js
// math.js
export function add(a, b) {
  return a + b;
}
```

```js
// app.js
import { add } from "./math.js";

console.log(add(2, 3)); // 5
```

|CommonJS|ES Modules|
|---|---|
|`require()`|`import`|
|`module.exports`|`export`|
|Traditional Node.js format|Modern JavaScript module format|

For ESM, use `"type": "module"` in `package.json` or the `.mjs` extension.

---

## 03 — npm & package.json

**npm** manages packages, dependencies, and scripts.

```bash
npm init -y
npm install express
npm install -D nodemon
npm uninstall express
```

### package.json

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  }
}
```

Run scripts:

```bash
npm start
npm run dev
```

### Versioning

```bash
^1.2.3  → compatible minor/patch updates
~1.2.3  → compatible patch updates
1.2.3   → exact version
```

- `package.json` — project metadata and dependency ranges.
- `package-lock.json` — records the resolved dependency tree.
- `dependencies` — packages needed at runtime.
- `devDependencies` — tools used during development.

---

## 04 — Core Modules

Node.js includes useful modules without extra installation.

### `path` — File paths

```js
import path from "node:path";

const file = path.join("data", "notes.json");

console.log(file);
console.log(path.extname(file)); // .json
```

### `fs` — File system

```js
import { readFile, writeFile } from "node:fs/promises";

await writeFile("note.txt", "Learn Node.js");

const text = await readFile("note.txt", "utf8");

console.log(text);
```

### `os` — Operating system

```js
import os from "node:os";

console.log(os.platform());
console.log(os.cpus().length);
console.log(os.freemem());
```

### `url` — URL parsing

```js
const url = new URL(
  "https://example.com/notes?id=10"
);

console.log(url.pathname); // /notes
console.log(url.searchParams.get("id")); // 10
```

### `crypto` — Secure randomness

```js
import { randomUUID } from "node:crypto";

console.log(randomUUID());
```

### `events` — Event-driven code

```js
import { EventEmitter } from "node:events";

const emitter = new EventEmitter();

emitter.on("message", (text) => {
  console.log(text);
});

emitter.emit("message", "Hello!");
```

### `http` — Basic server

```js
import { createServer } from "node:http";

const server = createServer((req, res) => {
  res.end("Hello from Node.js!");
});

server.listen(3000);
```

Visit `http://localhost:3000`.

### `stream` — Process data in chunks

```js
import { createReadStream } from "node:fs";

const stream = createReadStream("large.txt", "utf8");

stream.on("data", (chunk) => {
  console.log(chunk);
});
```

**Why streams?** Process large files without loading the entire file into memory.

---

## 05 — Environment & CLI Arguments

### Environment variables

```js
const port = process.env.PORT || 3000;

console.log(`Server port: ${port}`);
```

Run:

```js
PORT=4000 node app.js
```

Keep secrets out of source code. Use environment variables for configuration.

### Command-line arguments

```js
const args = process.argv.slice(2);

console.log(args);
```

```js
node app.js add "Learn Node.js"
```

Output:

```js
["add", "Learn Node.js"]
```

---

## 06 — File System: Async vs Sync

### Synchronous

```js
import { readFileSync } from "node:fs";

const data = readFileSync("notes.txt", "utf8");
```

Execution waits until the file operation finishes.

### Asynchronous

```js
import { readFile } from "node:fs/promises";

const data = await readFile("notes.txt", "utf8");
```

Execution can continue while Node.js waits for the file operation.

> [!warning] Best Practice Prefer asynchronous I/O in servers and request handlers. Synchronous operations block the JavaScript thread.

### Safe file handling

```js
import { mkdir, writeFile } from "node:fs/promises";

await mkdir("data", { recursive: true });
await writeFile("data/notes.json", "[]", "utf8");
```

Use controlled paths, validate input, and handle file errors.

---

## 07 — Event-Driven Design

An **event** announces that something happened. A listener reacts to it.

```js
import { EventEmitter } from "node:events";

class Notes extends EventEmitter {
  add(note) {
    console.log("Saved:", note);
    this.emit("noteAdded", note);
  }
}

const notes = new Notes();

notes.on("noteAdded", (note) => {
  console.log("Event received:", note);
});

notes.add("Study Node.js");
```

**Useful for:** notifications, logging, background tasks, and decoupled components.

---

## 08 — Debugging

### Logging

```js
console.log("Value:", value);
console.error("Something went wrong");
console.table([{ name: "Node.js", level: "beginner" }]);
```

### Stack traces

```js
function first() {
  second();
}

function second() {
  throw new Error("Something failed");
}

first();
```

The stack trace shows where the error occurred and how execution reached it.

### Inspector

```js
node --inspect app.js
node --inspect-brk app.js
```

- `--inspect` — enables the debugger.
- `--inspect-brk` — pauses at the start for debugging.

Use breakpoints to inspect variables and step through execution.

---

## 09 — Important Concepts

> [!important] Understand These Deeply
> 
> - Node.js is a runtime, not just JavaScript on a server.
> - Async I/O improves concurrency; it does not make CPU-heavy JavaScript non-blocking.
> - Avoid synchronous file operations in request handlers.
> - Handle errors from promises, streams, and network requests.
> - Separate configuration and secrets from application code.

### Quick comparison

|Task|Preferred approach|
|---|---|
|Read a file in a server|`node:fs/promises`|
|Handle HTTP requests|`node:http` or a framework|
|Process large files|Streams|
|Generate unique IDs|`node:crypto`|
|Read environment settings|`process.env`|
|React to custom events|`EventEmitter`|

---


## 🧠 Final Mental Model

```node
Node.js
  ├── Runtime       → V8 + native APIs + libuv
  ├── Modules       → import / export
  ├── Packages      → npm
  ├── System        → fs, path, os, crypto
  ├── Communication → http, events, streams
  ├── Configuration → process.env, process.argv
  └── Debugging     → inspector, logs, stack traces
```

> [!quote] Core Principle **Master asynchronous I/O, modules, and error handling first.** These ideas appear throughout real-world Node.js applications.