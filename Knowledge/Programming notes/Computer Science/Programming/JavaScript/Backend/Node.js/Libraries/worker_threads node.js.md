# 🧵 worker_threads

> Run JavaScript in **parallel threads** using Node.js.

Unlike the main thread, worker threads can execute JavaScript independently — useful for **CPU-intensive tasks**.

## ⚙️ 1. Create a Worker

**main.js**

```js
const { Worker } = require('node:worker_threads');

const worker = new Worker('./worker.js');
```

**worker.js**

```js
const { parentPort } = require('node:worker_threads');

console.log('Running in a worker thread!');
```

## 🔄 2. Communicate Between Threads

Use `postMessage()` to send data and listen for messages.

**main.js**

```js
const { Worker } = require('node:worker_threads');

const worker = new Worker('./worker.js');

worker.postMessage(10);

worker.on('message', (result) => {
  console.log('Result:', result);
});
```

**worker.js**

```js
const { parentPort } = require('node:worker_threads');

parentPort.on('message', (number) => {
  parentPort.postMessage(number * 2);
});
```

**Output:**

```
Result: 20
```

## 📡 3. Important Methods & Events

|Method / Event|Purpose|
|---|---|
|`new Worker()`|Creates a worker|
|`postMessage()`|Sends data|
|`parentPort`|Communicates with parent|
|`'message'`|Receives messages|
|`'error'`|Handles worker errors|
|`'exit'`|Detects worker termination|
|`worker.terminate()`|Stops a worker|

**Remember:**

- `worker_threads` → Parallel JavaScript execution.
- Main thread → Handles normal application work.
- Workers → Handle CPU-intensive tasks.

⚠️ Workers are generally not useful for simple I/O tasks, where Node.js already uses asynchronous operations.

---
