# 🟢 Node.js — Essential Built-in Modules

> [!abstract] 🎯 Goal Master the essential modules included with Node.js. No npm installation required.

## 📦 Core Modules

- 📁 **fs** — Read, write, and manage files.
    - 🔗 Reference: [[file system node.js]]
- 🧭 **path** — Work with file and directory paths.
    - 🔗 Reference: [[path node.js]]
- 🌐 **http** — Create HTTP servers and handle requests.
    - 🔗 Reference: [[http node.js]]
- 🔒 **crypto** — Hashing, encryption, and secure random values.
    - 🔗 Reference: [[crypto node.js]]
- ⚙️ **process** — Access environment variables and process information.
    - 🔗 Reference: [[process]]
- 🖥️ **os** — Get operating system information.
    - 🔗 Reference: [[os node.js]]
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
- ⚙️ **dotenv** — Not preinstalled library for environment management.
    - 🔗 Reference:
- 📡 **helmet** — Not preinstalled library for controlling traffic (rate limiting).
    - 🔗 Reference:
- 📁 **fileupload** — secure way to handle file uploads.
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


---