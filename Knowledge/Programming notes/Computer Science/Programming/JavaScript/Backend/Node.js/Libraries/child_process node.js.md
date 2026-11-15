# 🧒 Node.js — `child_process`

> **Run external programs and system commands from Node.js.**

The `child_process` module allows Node.js to execute commands, launch applications, and communicate with external processes.

## 📦 Import

```js
const { exec, spawn, fork } = require('node:child_process');
```

## ⚡ 1. `exec()` — Run a command

Executes a command and returns its output as a buffer/string.

```js
const { exec } = require('node:child_process');

exec('node --version', (error, stdout, stderr) => {
  if (error) return console.error(error);

  console.log(stdout);
});
```

- Best for short commands.
- Buffers the output in memory.

## 🚀 2. `spawn()` — Run a process

Starts a process and streams its output.

```js
const { spawn } = require('node:child_process');

const child = spawn('node', ['--version']);

child.stdout.on('data', (data) => {
  console.log(data.toString());
});

child.on('close', (code) => {
  console.log('Exit code:', code);
});
```

- Best for long-running processes.
- Handles large or continuous output.
- Supports streaming.

## 🧩 3. `fork()` — Run another Node.js process

> Creates a separate Node.js process with built-in communication.

**parent.js**

```js
const { fork } = require('node:child_process');

const child = fork('./child.js');

child.send({ message: 'Hello!' });

child.on('message', (data) => {
  console.log(data);
});
```

**child.js**

```js
process.on('message', (data) => {
  console.log(data.message);

  process.send({ status: 'Done!' });
});
```

- Designed for Node.js scripts.
- Allows communication using `send()` and `message` events.

## ⚖️ Quick comparison

|Method|Purpose|
|---|---|
|`exec()`|Execute a command|
|`spawn()`|Stream process output|
|`fork()`|Launch another Node.js process|

## ⚠️ Security

Avoid passing unsanitized user input to shell commands.

```js
// ❌ Dangerous
exec(`echo ${userInput}`);

// ✅ Safer: no shell interpretation
spawn('echo', [userInput]);
```

---

💡 **Remember:**

- `exec` → Simple command.
- `spawn` → Streaming process.
- `fork` → Node.js child process.

---
