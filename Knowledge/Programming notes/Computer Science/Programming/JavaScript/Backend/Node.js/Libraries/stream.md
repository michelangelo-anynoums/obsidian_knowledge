# 🌊 Streams — Process Data Incrementally

> 🎯 **Goal:** Process data piece by piece instead of loading everything into memory.

## 🧠 1. What are Streams?

A stream processes data in small chunks (pieces).

Instead of loading an entire file into memory, Node.js reads and processes it incrementally.


```
Without streams:
File → Load everything → Process

With streams:
File → Chunk → Process → Chunk → Process
```

**Why use streams?**

- 💾 Lower memory usage.
- ⚡ Efficient data processing.
- 📦 Handle large files.
- 🔄 Process data while it is arriving.

---

## 🔧 2. Four Types of Streams

|Type|Purpose|
|---|---|
|Readable|Read data|
|Writable|Write data|
|Duplex|Read and write|
|Transform|Read, modify, and write|

### 📖 Readable Stream

Read a file piece by piece.

```js
import fs from "node:fs";

const stream = fs.createReadStream("large.txt", {
  encoding: "utf8"
});

stream.on("data", chunk => {
  console.log(chunk);
});

stream.on("end", () => {
  console.log("Finished reading!");
});
```

### ✍️ Writable Stream

Write data incrementally.

```js
const stream = fs.createWriteStream("output.txt");

stream.write("Hello ");
stream.write("Node.js!");

stream.end();
```

### 🔄 Duplex Stream

Read and write data through the same stream.

Examples: TCP sockets.

```js
import net from "node:net";

const server = net.createServer(socket => {
  socket.on("data", chunk => {
    socket.write(`Received: ${chunk}`);
  });
});

server.listen(3000);
```

### ⚙️ Transform Stream

Modify data while it passes through.

```js
import { Transform } from "node:stream";

const upperCase = new Transform({
  transform(chunk, encoding, callback) {
    callback(null, chunk.toString().toUpperCase());
  }
});
```

---

## 🔗 3. Piping Streams

Connect streams together.

```js
import fs from "node:fs";

fs.createReadStream("input.txt")
  .pipe(fs.createWriteStream("output.txt"));
```

**Flow:**

```
📖 Readable
     |
     ↓
  📦 Chunks
     |
     ↓
✍️ Writable
```

`pipe()` automatically manages data flow and backpressure.

### 🛡️ Better approach: pipeline()

Handles errors and stream completion more reliably.


```js
import fs from "node:fs";
import { pipeline } from "node:stream/promises";

await pipeline(
  fs.createReadStream("input.txt"),
  fs.createWriteStream("output.txt")
);
```

---

## ⚖️ 4. Backpressure

Backpressure happens when data is produced faster than it can be consumed.

Example:

```
Producer: 100 MB/s
Consumer:  10 MB/s

Result: Data builds up in memory.
```

Streams manage this by slowing down the producer when the consumer cannot keep up.


```js
const canContinue = writable.write(chunk);

if (!canContinue) {
  writable.once("drain", () => {
    console.log("Ready for more data");
  });
}
```

---

## 🌐 5. Streams in Backend Development

Common real-world applications:

- 📁 File uploads and downloads.
- 📦 Processing large CSV or JSON files.
- 🌐 HTTP request and response bodies.
- 🎥 Audio and video streaming.
- 🔄 Data transformation.
- 🗄️ Database result processing.

### Example: Stream a file through Express


```js
import fs from "node:fs";

app.get("/download", (req, res, next) => {
  const stream = fs.createReadStream("large.pdf");

  stream.on("error", next);
  stream.pipe(res);
});
```

---

## 🧠 Key Takeaways

|Concept|Remember|
|---|---|
|Readable|Get data|
|Writable|Send data|
|Duplex|Read + write|
|Transform|Modify data|
|Pipe|Connect streams|
|Pipeline|Safely manage stream chains|
|Backpressure|Control data flow|

**🌊 Streams = Process data incrementally, efficiently, and with less memory.**

---
