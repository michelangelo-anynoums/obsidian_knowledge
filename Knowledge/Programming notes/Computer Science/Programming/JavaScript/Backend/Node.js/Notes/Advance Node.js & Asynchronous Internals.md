# ⚡ 03 — Advanced Node.js & Asynchronous Internals

> 🧠 **Learning goal:** Understand how Node.js executes asynchronous code, manages data streams, handles concurrency, and uses system resources efficiently.

## 🗺️ What You Will Learn

- 🔄 How the event loop schedules asynchronous work.
- 🌊 How streams process large amounts of data without loading everything into memory.
- ⚙️ How processes and worker threads handle concurrent tasks.
- 🛡️ How to manage cancellation, errors, and resource cleanup.
- 🔬 How to measure performance and diagnose memory problems.

---

## 🔄 1. Event Loop & Performance

### 1.1 — How Node.js Executes JavaScript

> [!important] Node.js runs JavaScript on a main thread by default. It uses the **event loop** to coordinate callbacks and asynchronous operations, allowing it to handle I/O without blocking JavaScript while waiting for results.

For example, when Node.js reads a file asynchronously, it can continue executing other JavaScript while the file operation completes.


```js
const fs = require('node:fs');

console.log('1. Start');

fs.readFile('data.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log('3. File read:', data);
});

console.log('2. Continue');
```

**Expected order:**

text

```
1. Start
2. Continue
3. File read: ...
```

The file-reading callback runs later because the asynchronous operation does not block the main JavaScript thread.

💡 **Remember:** Asynchronous does not mean that JavaScript executes everything in parallel. The main thread can still be blocked by long-running synchronous code.

### 1.2 — Event Loop Phases

The event loop coordinates different types of callbacks through phases.

|Phase|Purpose|
|---|---|
|⏱️ Timers|Run eligible `setTimeout()` and `setInterval()` callbacks.|
|📥 Pending callbacks|Handle certain deferred system-operation callbacks.|
|🔌 Poll|Retrieve I/O events and execute relevant callbacks.|
|🧹 Check|Run `setImmediate()` callbacks.|
|🔒 Close callbacks|Handle events such as socket closure.|

Node.js also performs other internal work between phases. Promise microtasks and `process.nextTick()` callbacks have their own scheduling rules and are not simply additional event loop phases.

**Example:**

```js
const fs = require('node:fs');

fs.readFile(__filename, () => {
  setTimeout(() => console.log('Timer'), 0);
  setImmediate(() => console.log('Immediate'));
});
```

> [!important] Inside an I/O callback, `setImmediate()` generally runs before the zero-delay timer.

⚠️ A timer specifies a minimum delay, not an exact execution time. Actual timing depends on the event loop and other work.

### 1.3 — Microtasks, Promises & `process.nextTick()`

JavaScript uses queues to schedule callbacks that run after the current synchronous execution finishes.

- ⚡ `process.nextTick()` schedules a callback in Node.js's next-tick queue.
- 🤝 `Promise.then()` and `await` continuations use the microtask queue.
- ⏱️ `setTimeout()` schedules a timer callback.
- 🔄 `setImmediate()` schedules a callback for the check phase.

Consider this example:

```js
console.log('A');

setTimeout(() => console.log('B'), 0);

Promise.resolve().then(() => console.log('C'));

process.nextTick(() => console.log('D'));

console.log('E');
```

In a standard CommonJS execution, the output is:

text

```js
A
E
D
C
B
```

**Why?**

1. `A` and `E` run synchronously.
2. The next-tick callback runs before Promise microtasks in this context.
3. The Promise callback runs next.
4. The timer runs when its callback becomes eligible.

⚠️ Do not assume every ordering is universal. ES modules, nested scheduling, and the execution context can affect the order.

Excessive recursive `process.nextTick()` calls or continuously replenished microtasks can starve I/O by preventing the event loop from making progress.

### 1.4 — Backpressure: Controlling Data Flow

**Backpressure** occurs when a producer generates data faster than a consumer can process it.

Imagine downloading a large file while writing it to a slow disk. If data is produced faster than it can be written, queued data can consume increasing amounts of memory.

The solution is to regulate the flow of data instead of allowing unlimited buffering.

Node.js streams support backpressure. For example:

```js
const fs = require('node:fs');

const source = fs.createReadStream('large-file.bin');
const destination = fs.createWriteStream('copy.bin');

source.pipe(destination);
```

The `.pipe()` method coordinates flow so that a writable stream can signal when it needs the readable stream to slow down.

For more robust pipelines, use `stream.pipeline()` because it also coordinates error propagation and stream cleanup.

### 1.5 — Measuring Performance

Fast code is not necessarily efficient code. Measure the problem before trying to optimize it.

|Metric|What it tells you|
|---|---|
|⏱️ Latency|How long an operation takes.|
|🧮 CPU usage|How much processing time is being consumed.|
|🧠 Memory usage|How much memory the application occupies.|
|🔄 Event-loop delay|How long the event loop is delayed beyond its expected scheduling.|
|📦 Allocation rate|How frequently the application creates new objects and buffers.|

Example: measuring event-loop delay with Node.js's `perf_hooks` module.


```js
const {
  monitorEventLoopDelay
} = require('node:perf_hooks');

const histogram = monitorEventLoopDelay({
  resolution: 20
});

histogram.enable();

setTimeout(() => {
  console.log(
    'Mean delay (ms):',
    histogram.mean / 1e6
  );

  console.log(
    '99th percentile (ms):',
    histogram.percentile(99) / 1e6
  );

  histogram.disable();
}, 5000);
```

The delay measurements are reported in nanoseconds, so dividing by one million converts them to milliseconds.

---

## 🌊 2. Streams & Binary Data

### 2.1 — Why Streams Matter

Reading a complete file into memory is straightforward:

js

```js
const fs = require('node:fs/promises');

async function readWholeFile() {
  const data = await fs.readFile('large-file.bin');
  console.log(data.length);
}
```

However, this loads the entire file into memory.

For a very large file, that can create unnecessary memory pressure.

A **stream** processes data incrementally, usually in chunks.

Instead of holding the entire file in memory, the program can read a chunk, process it, and continue.

### 2.2 — The Four Main Stream Types

|Stream|Purpose|Example|
|---|---|---|
|📥 Readable|Produces data for consumers.|Reading a file.|
|📤 Writable|Receives data from producers.|Writing a file.|
|🔀 Duplex|Supports both reading and writing.|A network socket.|
|🛠️ Transform|Reads data, transforms it, and produces output.|Compression or encryption.|

A transform stream is a special kind of duplex stream.

### 2.3 — Buffers and Binary Data

A `Buffer` represents a sequence of bytes. It is useful when working with files, network packets, images, compressed data, and other binary formats.

js

```js
const buffer = Buffer.from('Hello', 'utf8');

console.log(buffer);
console.log(buffer.length);
console.log(buffer.toString('utf8'));
```

The buffer contains the UTF-8 encoded bytes for `Hello`.

Important distinction:

- **Bytes** represent raw binary data.
- **Encoding** determines how bytes are interpreted as text.
- **Characters** and bytes do not always have a one-to-one relationship.

> [!question] For example, some Unicode characters require multiple UTF-8 bytes. Splitting a text stream at an arbitrary byte boundary can split a character, so text processing must account for encoding boundaries.

### 2.4 — Connecting Streams with `pipeline()`

Consider copying a large file.

js

```js
const fs = require('node:fs');
const { pipeline } = require('node:stream/promises');

async function copyFile() {
  await pipeline(
    fs.createReadStream('source.bin'),
    fs.createWriteStream('destination.bin')
  );

  console.log('Copy complete');
}

copyFile().catch(console.error);
```

`pipeline()` connects the streams and returns a Promise that resolves when the pipeline completes successfully.

It also propagates errors and coordinates stream destruction when a pipeline fails.

This is generally safer than manually wiring multiple streams together.

### 2.5 — Processing Data with a Transform Stream

A transform stream can modify each chunk as data passes through it.

js

```js
const { Transform } = require('node:stream');

const uppercase = new Transform({
  transform(chunk, encoding, callback) {
    callback(null, chunk.toString().toUpperCase());
  }
});

uppercase.on('data', chunk => {
  console.log(chunk.toString());
});

uppercase.write('hello ');
uppercase.write('world');
uppercase.end();
```

Output:

text

```js
HELLO
 WORLD
```

The example illustrates chunk transformation. In production, transforming arbitrary text chunks requires care because a multibyte character may span chunk boundaries.

---

## ⚙️ 3. Processes & Concurrency

### 3.1 — Concurrency vs. Parallelism

These concepts are related but different.

- **Concurrency:** Multiple tasks make progress during overlapping periods.
- **Parallelism:** Multiple tasks execute at the same time on separate execution resources.

Node.js can handle many concurrent I/O operations without creating one JavaScript thread per operation. CPU-intensive JavaScript, however, can block the main thread unless it is moved elsewhere.

### 3.2 — Child Processes

Child processes let Node.js run external programs or separate Node.js processes.

The main APIs are:

- `spawn()` — starts a process and exposes its input, output, and error streams.
- `exec()` — runs a command through a shell and buffers its output.
- `fork()` — starts another Node.js process with an IPC communication channel.

Example using `spawn()`:

```js
const { spawn } = require('node:child_process');

const child = spawn('node', ['--version']);

child.stdout.on('data', data => {
  console.log(data.toString());
});

child.on('error', error => {
  console.error('Failed to start:', error);
});

child.on('close', code => {
  console.log('Exit code:', code);
});
```

Use `spawn()` when you need streaming output or want to process output incrementally.

⚠️ Never pass untrusted input into shell commands without appropriate safeguards. When possible, pass executable arguments directly instead of constructing shell command strings.

### 3.3 — Worker Threads

Worker threads allow JavaScript to execute on separate threads.

They are particularly useful for CPU-intensive tasks such as:

- Processing large datasets.
- Calculating hashes over substantial inputs.
- Parsing or transforming complex data.
- Performing expensive mathematical calculations.

Example:

```js
// main.js
const { Worker } = require('node:worker_threads');

const worker = new Worker('./worker.js', {
  workerData: 40
});

worker.on('message', result => {
  console.log('Result:', result);
});

worker.on('error', console.error);

worker.on('exit', code => {
  if (code !== 0) {
    console.error('Worker stopped:', code);
  }
});
```

js

```js
// worker.js
const {
  parentPort,
  workerData
} = require('node:worker_threads');

function factorial(n) {
  let result = 1;

  for (let i = 2; i <= n; i++) {
    result *= i;
  }

  return result;
}

parentPort.postMessage(factorial(workerData));
```

The worker performs the calculation separately and sends the result back to the main thread.

This example uses a small calculation for simplicity. Real CPU-intensive jobs should be selected and benchmarked carefully.

💡 **Remember:** Worker threads are not automatically faster for every task. Creating workers has overhead, so a worker pool is often preferable when processing many jobs.

### 3.5 — Graceful Shutdown

A graceful shutdown gives an application time to finish ongoing work before exiting.

Typical steps:

1. Stop accepting new requests.
2. Stop scheduling new background jobs.
3. Finish or safely cancel active work.
4. Close database connections and other resources.
5. Exit before the deployment system's shutdown deadline.

Example:

```js
const server = require('node:http').createServer(
  (req, res) => {
    res.end('Hello');
  }
);

server.listen(3000);

process.on('SIGTERM', () => {
  server.close(error => {
    if (error) {
      console.error(error);
      process.exitCode = 1;
    }
  });
});
```

`server.close()` stops accepting new connections and waits for connections to close, subject to the behavior of the Node.js version and connection types involved.

A production application should also implement a shutdown timeout and close its database pools, workers, and other resources.

---

## 🧠 4. Advanced Language & Runtime Features

### 4.1 — Async Iterators and Generators

An asynchronous iterator lets you consume values that become available over time.

An asynchronous generator uses `async function*` and can yield values incrementally.

```js
async function* countToThree() {
  for (let i = 1; i <= 3; i++) {
    await new Promise(resolve => setTimeout(resolve, 100));
    yield i;
  }
}

async function main() {
  for await (const number of countToThree()) {
    console.log(number);
  }
}

main();
```

```js
1
2
3
```

`for await...of` requests each value from the iterator and awaits its availability.

This pattern is useful for paginated APIs, asynchronous data sources, and stream processing.

### 4.2 — Cancellation with `AbortController`

Some operations should stop when they are no longer needed.

Examples include:

- A client disconnecting.
- A request exceeding its deadline.
- A user cancelling a search.
- A background task becoming irrelevant.

`AbortController` provides an `AbortSignal` that supported APIs can observe.

js

```js
const controller = new AbortController();

const timeout = setTimeout(() => {
  controller.abort();
}, 2000);

async function fetchData() {
  try {
    const response = await fetch(
      'https://example.com',
      { signal: controller.signal }
    );

    console.log(await response.text());
  } catch (error) {
    if (error.name === 'AbortError') {
      console.log('Request cancelled');
    } else {
      console.error(error);
    }
  } finally {
    clearTimeout(timeout);
  }
}

fetchData();
```

The request is aborted if it has not completed before the timeout.

⚠️ Cancellation is cooperative: an API or task must support or explicitly check the signal. Aborting a request does not automatically cancel unrelated work started elsewhere.

### 4.3 — Custom Errors and Error Causes

Custom error classes help distinguish different failure types.

```js
class AppError extends Error {
  constructor(message, options) {
    super(message, options);
    this.name = 'AppError';
  }
}

class DatabaseError extends AppError {
  constructor(message, options) {
    super(message, options);
    this.name = 'DatabaseError';
  }
}

try {
  throw new Error('Connection refused');
} catch (cause) {
  throw new DatabaseError(
    'Unable to load user data',
    { cause }
  );
}
```

The `cause` property preserves the original error, making debugging easier while allowing the application to report a meaningful higher-level failure.
### 4.4 — Resource Cleanup with `try...finally`

Resources such as files, connections, locks, and temporary directories may need cleanup even when an operation fails.

js

```js
async function processResource(resource) {
  try {
    await resource.open();
    await resource.process();
  } finally {
    await resource.close();
  }
}
```

The `finally` block executes whether the `try` block succeeds or throws.


---

