# 📂 Node.js — Path Module

> 💡 **Core idea:** The `path` module helps you work with file and directory paths safely across different operating systems.

## 📦 1. Import the Module

> [!important] Node.js includes `path` by default. No installation needed.


```js
const path = require("node:path");
```

## 🧩 2. Essential Methods

### 📍 `path.join()`

Combines path segments into one normalized path.

```js
const filePath = path.join("users", "alex", "data.json");

console.log(filePath);
// users/alex/data.json (on Unix-like systems)
```

Useful for building paths without manually adding slashes.

### 🏠 `path.resolve()`

Creates an absolute path from path segments.

```js
const filePath = path.resolve("files", "data.json");

console.log(filePath);
// /your/current/directory/files/data.json
```

An absolute segment resets the earlier path:

```js
path.resolve("/app", "files", "data.json");
// /app/files/data.json (on Unix-like systems)
```

### 📄 `path.basename()`

Returns the final part of a path, usually the filename.

```js
path.basename("/app/files/data.json");
// data.json
```

Remove the extension:

```js
path.basename("/app/files/data.json", ".json");
// data
```

### 📁 `path.dirname()`

Returns the directory containing the path.

```js
path.dirname("/app/files/data.json");
// /app/files
```

### 🔤 `path.extname()`

Returns the file extension, including the dot.

```js
path.extname("photo.png");
// .png

path.extname("document.pdf");
// .pdf
```

### 🧱 `path.parse()`

Breaks a path into its components.

```js
path.parse("/app/files/data.json");
```

Result:

```js
{
  root: "/",
  dir: "/app/files",
  base: "data.json",
  ext: ".json",
  name: "data"
}
```

### 🔗 `path.isAbsolute()`

Checks whether a path is absolute.

```js
path.isAbsolute("/app/data.json"); // true
path.isAbsolute("app/data.json");  // false
```

## 🛠️ 3. Practical Example — Build a File Path

Use `__dirname` to refer to the directory containing the current CommonJS file.

```js
const path = require("node:path");

const filePath = path.join(
  __dirname,
  "data",
  "users.json"
);

console.log(filePath);
```

This builds a path to `data/users.json` relative to the current file, regardless of the process's working directory.

> 📌 `__dirname` is available in CommonJS files. In ES modules, use `import.meta.url` with `fileURLToPath()` when you need the current file's directory.

## ⚖️ 4. `join()` vs `resolve()`

|Method|Purpose|
|---|---|
|`path.join()`|Combines path segments|
|`path.resolve()`|Produces an absolute path|

```js
path.join("app", "files", "data.json");
// app/files/data.json

path.resolve("app", "files", "data.json");
// Absolute path from the current working directory
```

Remember: `process.cwd()` returns the directory from which the Node.js process was started. It may differ from `__dirname`.

## 🔐 5. Important Security Note

Never assume that joining a user-provided filename makes it safe.


```js
const path = require("node:path");

const baseDir = path.resolve("uploads");
const target = path.resolve(baseDir, userInput);

if (
  target !== baseDir &&
  !target.startsWith(baseDir + path.sep)
) {
  throw new Error("Invalid file path");
}
```

This illustrates a basic traversal check for a directory that is not itself an allowed target. Real applications should also consider symlinks and filesystem access permissions.

## 🧠 Remember

- 📂 `join()` → Combine paths.
- 🏠 `resolve()` → Create an absolute path.
- 📄 `basename()` → Get the filename.
- 📁 `dirname()` → Get the directory.
- 🔤 `extname()` → Get the extension.
- 🧩 `parse()` → Split a path into components.
- 🔍 `isAbsolute()` → Check whether a path is absolute.

> 🎯 **Key takeaway:** Use `node:path` instead of manually concatenating strings when working with file paths in Node.js.

---
