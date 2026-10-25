# 🟢 Node.js — Essential Built-in Modules

> [!abstract] 🎯 Goal Master the essential modules included with Node.js. No npm installation required.

## 📦 Core Modules

- 📁 **fs** — Read, write, and manage files.
    - 🔗 Reference: [[file system node.js]]
- 🧭 **path** — Work with file and directory paths.
    - 🔗 Reference:
- 🌐 **http** — Create HTTP servers and handle requests.
    - 🔗 Reference:
- 🔒 **crypto** — Hashing, encryption, and secure random values.
    - 🔗 Reference:
- ⚙️ **process** — Access environment variables and process information.
    - 🔗 Reference:
- 🖥️ **os** — Get operating system information.
    - 🔗 Reference:
- 📍 **url** — Parse and construct URLs.
    - 🔗 Reference:
- 📡 **events** — Create and handle event-driven communication.
    - 🔗 Reference:
- 🌊 **stream** — Process data incrementally and efficiently.
    - 🔗 Reference:
- 🧩 **util** — Useful utilities for debugging, promises, and more.
    - 🔗 Reference:
- 📦 **buffer** — Handle binary data.
    - 🔗 Reference:
- ⏱️ **timers** — Schedule delayed and repeated callbacks.
    - 🔗 Reference:
- 🧵 **worker_threads** — Run JavaScript in parallel threads.
    - 🔗 Reference:
- 🧒 **child_process** — Launch external processes and commands.
    - 🔗 Reference:
- 🗂️ **readline** — Read input line by line, including terminal input.
    - 🔗 Reference:
- 🧪 **assert** — Check conditions in tests and debugging.
    - 🔗 Reference:
- 🧰 **module** — Understand and work with Node.js modules.
    - 🔗 Reference:
- 📂 **node:fs/promises** — Use promise-based filesystem operations.
    - 🔗 Reference:

## 💻 Import Examples


```js
import fs from 'node:fs'
import path from 'node:path'
import os from 'node:os'
import crypto from 'node:crypto'
import { EventEmitter } from 'node:events'
import { Readable } from 'node:stream'
import { fileURLToPath } from 'node:url'
```

## ⭐ Learning Priority

1. 📁 `fs`
2. 🧭 `path`
3. ⚙️ `process`
4. 📍 `url`
5. 🌐 `http`
6. 📦 `buffer`
7. 🌊 `stream`
8. 📡 `events`
9. 🔒 `crypto`
10. 🖥️ `os`

> [!tip] 📚 Official documentation [https://nodejs.org/api/](https://nodejs.org/api/)
> 
> **Note:** These are built-in Node.js modules, not third-party npm packages. Some are namespaces with submodules, such as `node:fs/promises`.


---