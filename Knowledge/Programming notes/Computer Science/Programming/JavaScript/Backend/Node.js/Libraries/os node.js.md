# 🟢 Node.js — JavaScript Runtime

> 🚀 Node.js allows you to run JavaScript outside the browser, using the V8 JavaScript engine.

## 📦 Import Modules

```js
// CommonJS
const os = require('os');

// ES Modules
import os from 'node:os';
```

## 💻 System Information

```js
// Operating system name
console.log(os.type());

// OS platform
console.log(os.platform());

// OS architecture
console.log(os.arch());

// OS release
console.log(os.release());

// Hostname
console.log(os.hostname());
```

## 📂 User & Directory Information

```js
// Home directory
console.log(os.homedir());

// Current username
console.log(os.userInfo().username);

// Temporary directory
console.log(os.tmpdir());

// System uptime (seconds)
console.log(os.uptime());
```

## 🧠 Memory Information

```js
// Total system memory (bytes)
console.log(os.totalmem());

// Free system memory (bytes)
console.log(os.freemem());
```

## ⚡ Useful Examples

```js
// Check the operating system
if (os.platform() === 'win32') {
    console.log('Windows');
} else if (os.platform() === 'darwin') {
    console.log('macOS');
} else if (os.platform() === 'linux') {
    console.log('Linux');
}

// Memory in GB
const memoryGB = os.totalmem() / 1024 ** 3;
console.log(memoryGB.toFixed(2), 'GB');

// CPU information
console.log(os.cpus().length, 'CPU cores');
```

## 📌 Quick Reference

|Method|Description|
|---|---|
|`os.type()`|OS name|
|`os.platform()`|OS platform|
|`os.arch()`|CPU architecture|
|`os.release()`|OS version|
|`os.hostname()`|Computer name|
|`os.homedir()`|Home directory|
|`os.userInfo()`|User information|
|`os.tmpdir()`|Temporary directory|
|`os.uptime()`|System uptime|
|`os.totalmem()`|Total RAM|
|`os.freemem()`|Available RAM|
|`os.cpus()`|CPU information|

## 💡 Remember

- `os` is a built-in Node.js module.
- No installation is required.
- Memory values are returned in bytes.
- `os.platform()` is useful for OS-specific code.

---
