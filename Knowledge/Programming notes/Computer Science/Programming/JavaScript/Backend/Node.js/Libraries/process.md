# ⚙️ Node.js — `process`

> Access environment variables, process information, and runtime controls.

## 📌 1. Environment Variables

Read environment variables using `process.env`.

```js
// Access an environment variable
console.log(process.env.NODE_ENV);

// Custom environment variable
console.log(process.env.PORT);
```

Set a default value:

```js
const port = process.env.PORT || 3000;
```

## 🖥️ 2. Process Information

Get information about the running Node.js process.

```js
// Node.js version
console.log(process.version);

// Operating system platform
console.log(process.platform);

// Process ID
console.log(process.pid);

// Current working directory
console.log(process.cwd());
```

## 📂 3. Command-Line Arguments

Access arguments passed when running a script.

```js
// All arguments
console.log(process.argv);

// Custom argument
const name = process.argv[2];

console.log(`Hello, ${name}!`);
```

Run:

```bash
node app.js Alex
```

## 🚪 4. Exit the Process

Stop the Node.js process.

```js
// Successful exit
process.exit(0);

// Error exit
process.exit(1);
```

## ⏱️ 5. Process Events

Listen for important process events.

```js
process.on("exit", (code) => {
  console.log(`Process finished: ${code}`);
});
```

## 🧠 Quick Reference

|Property / Method|Purpose|
|---|---|
|`process.env`|Environment variables|
|`process.argv`|Command-line arguments|
|`process.version`|Node.js version|
|`process.platform`|Operating system|
|`process.pid`|Process ID|
|`process.cwd()`|Current directory|
|`process.exit()`|Exit process|
|`process.on()`|Listen for events|

---
