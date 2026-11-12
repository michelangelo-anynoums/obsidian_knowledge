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
    - 🔗 Reference: [[url node.js]]
- 📡 **events** — Create and handle event-driven communication.
    - 🔗 Reference: [[events node.js]]
- 🌊 **stream** — Process data incrementally and efficiently.
    - 🔗 Reference: [[stream]]
- 🧩 **util** — Useful utilities for debugging, promises, and more.
    - 🔗 Reference: [[util node.js]]
- 📦 **buffer** — Handle binary data.
    - 🔗 Reference: [[buffer node.js]]
- ⏱️ **timers** — Schedule delayed and repeated callbacks.
    - 🔗 Reference: [[timers node.js]]
- 🧵 **worker_threads** — Run JavaScript in parallel threads.
    - 🔗 Reference: [[worker_threads node.js]]
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

---

## ⚡ Essential Node.js Libraries

- ⚙️ **dotenv** — Loads environment variables from `.env` files to manage configuration, credentials, and API keys.
    - 🔗 Reference: 
- 🛡️ **helmet** — Adds security HTTP headers to protect your backend against common web vulnerabilities.
    - 🔗 Reference: 
- 📡 **express-rate-limit** — Limits incoming requests to prevent brute-force attacks and API abuse.
    - 🔗 Reference: 
- 🌐 **cors** — Controls which external origins are allowed to access your backend.
    - 🔗 Reference: 
- 📁 **multer** — Handles file uploads through `multipart/form-data`, with file size and storage configuration.
    - 🔗 Reference: 
- 🗄️ **better-sqlite3** — Provides fast and simple SQLite database operations, including queries and transactions.
    - 🔗 Reference: 
- 💾 **connect-sqlite3** — Stores Express sessions in an SQLite database, allowing sessions to persist after server restarts.
    - 🔗 Reference: 
- 🔑 **express-session** — Manages user sessions and authentication state using session cookies.
    - 🔗 Reference: 
- 🔐 **bcrypt** — Securely hashes passwords before storing them in the database and verifies passwords during login.
    - 🔗 Reference: 
- ✅ **zod** — Validates and checks incoming data, such as request bodies, parameters, and query strings.
    - 🔗 Reference:

---

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