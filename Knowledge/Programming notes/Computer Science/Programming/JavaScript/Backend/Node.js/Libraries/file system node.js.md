# 📁 Node.js — `fs` (File System)

> [!abstract] 🎯 Goal Learn to read, create, update, delete, and manage files using Node.js.

## 🧠 1. What is `fs`?

`fs` is a built-in Node.js module for working with files and directories.

```js
import fs from 'node:fs'
import fsPromises from 'node:fs/promises'
```

- 📖 Read files
- ✍️ Write files
- ➕ Append content
- 🗑️ Delete files
- 📂 Manage directories

## 📖 2. Read a File

js

```js
import { readFile } from 'node:fs/promises'

const data = await readFile('hello.txt', 'utf8')

console.log(data)
```

## ✍️ 3. Write a File

Creates a file or replaces its existing content.

js

```js
import { writeFile } from 'node:fs/promises'

await writeFile('hello.txt', 'Hello, Node.js! 🟢')
```

## ➕ 4. Append Content

Adds content to the end of a file.

```js
import { appendFile } from 'node:fs/promises'

await appendFile('hello.txt', '\nLearning fs 📚')
```

## 🗑️ 5. Delete a File

```js
import { unlink } from 'node:fs/promises'

await unlink('hello.txt')
```

⚠️ The file must exist, and deletion is not automatically reversible.

## 📂 6. Create a Directory

```js
import { mkdir } from 'node:fs/promises'

await mkdir('notes', { recursive: true })
```

## 📋 7. List Directory Contents


```js
import { readdir } from 'node:fs/promises'

const files = await readdir('./')

console.log(files)
```

## 🔍 8. Check File Information

```js
import { stat } from 'node:fs/promises'

const info = await stat('hello.txt')

console.log(info.isFile())
console.log(info.isDirectory())
console.log(info.size)
```

## 🛡️ 9. Handle Errors


```js
import { readFile } from 'node:fs/promises'

try {
  const data = await readFile('hello.txt', 'utf8')
  console.log(data)
} catch (error) {
  console.error('❌ Error:', error.message)
}
```

## ⚡ 10. Essential Methods

|Method|Purpose|
|---|---|
|`readFile()`|📖 Read a file|
|`writeFile()`|✍️ Write or replace|
|`appendFile()`|➕ Add content|
|`unlink()`|🗑️ Delete a file|
|`mkdir()`|📂 Create a directory|
|`readdir()`|📋 List directory contents|
|`rename()`|🔄 Rename or move a file|
|`copyFile()`|📑 Copy a file|
|`stat()`|🔍 Get file information|
|`access()`|🔐 Check accessibility|


> [!tip] ⭐ Best practice Prefer `node:fs/promises` for everyday asynchronous file operations. Use `await` inside an `async` function or at the top level of an ES module.

---
## 📁 Example: Reusable read function

```js
import { readFile } from 'node:fs/promises'

async function readTextFile(filePath) {
  try {
    const content = await readFile(filePath, 'utf8')
    return content
  } catch (error) {
    console.error('❌ Reading failed:', error.message)
    throw error
  }
}

// Usage
const text = await readTextFile('./hello.txt')
console.log(text)
```

## 🧠 How it works

- `async` — allows the function to use `await`.
    
- `await` — waits for the file-reading operation to finish without blocking the Node.js event loop.
    
- `return content` — returns the file contents to the caller.
    
- `try...catch` — handles errors, such as a missing file.
    
- `throw error` — lets the caller handle the error too.
    

### ⚡ Even simpler

If you want the caller to handle errors, you can keep the function minimal:

```js
async function readTextFile(filePath) {
  return await readFile(filePath, 'utf8')
}
```

You can even omit `await` here:

```js
function readTextFile(filePath) {
  return readFile(filePath, 'utf8')
}
```

Both return a Promise containing the file contents. The second version is simpler because it directly returns the Promise.

> [!important] ⭐ Best practice: Use the `async` version when you need additional asynchronous steps or error handling inside the function. Otherwise, returning the Promise directly is perfectly fine.

---