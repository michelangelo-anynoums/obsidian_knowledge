# 🗺️ 01 — JavaScript Foundations

> [!abstract] 🎯 Learning Goal Understand JavaScript well enough to build backend applications with Node.js.
> 
> **Rule:** Learn a concept → read the example → run it → modify it yourself.

---

## 🧱 1. Variables & Data Types

Variables store information. Prefer `const` by default and use `let` when reassignment is needed.

```js
const name = "Alex";       // String
let age = 25;              // Number
const isDev = true;        // Boolean
const nothing = null;      // Intentional absence
let value;                 // undefined

const user = { name, age }; // Object
const skills = ["JS", "Node"]; // Array
```

### 🔍 Types, coercion & truthy values

JavaScript sometimes converts values automatically. This is called **type coercion**.

```js
console.log("5" + 2); // "52" — string concatenation
console.log("5" - 2); // 3 — numeric conversion

console.log(Boolean("hello")); // true
console.log(Boolean(""));      // false
console.log(Boolean(0));       // false
console.log(Boolean([]));      // true!
```

💡 **Remember:** `0`, `""`, `null`, `undefined`, `false` and `NaN` are falsy. Empty arrays and objects are truthy.

---

## ⚙️ 2. Functions

Functions package reusable logic.

```js
// Declaration
function add(a, b) {
  return a + b;
}

// Function expression
const multiply = function (a, b) {
  return a * b;
};

// Arrow function
const square = n => n * n;

console.log(add(2, 3));      // 5
console.log(multiply(2, 3)); // 6
console.log(square(4));      // 16
```

### 🔁 Callbacks & higher-order functions

A **callback** is a function passed to another function. A **higher-order function** accepts or returns a function.

```js
function processNumber(n, callback) {
  return callback(n);
}

console.log(processNumber(5, n => n * 2)); // 10
```

### 🔒 Closures

A closure remembers variables from the scope where a function was created.

```js
function createCounter() {
  let count = 0;

  return () => ++count;
}

const counter = createCounter();

console.log(counter()); // 1
console.log(counter()); // 2
```

💡 Useful for private state and functions that remember previous values.

---

## 🌍 3. Scope & Hoisting

**Scope** determines where a variable can be accessed.

```js
const globalName = "Alex";

function greet() {
  const message = "Hello";
  console.log(globalName); // Works
}

greet();
// console.log(message); // ReferenceError
```

### 📦 Block scope

```js
if (true) {
  let x = 10;
  const y = 20;
}

// x and y are unavailable here
```

### ⬆️ Hoisting

JavaScript processes declarations before executing code, but different declarations behave differently.

```js
sayHi(); // Works

function sayHi() {
  console.log("Hi!");
}
```

```js
console.log(name); // ReferenceError
const name = "Alex";
```

💡 `let` and `const` exist in a temporal dead zone until their declaration is reached. Avoid relying on hoisting.

---

## 🧰 4. Objects & Arrays

### 🧩 Destructuring

Extract values into variables.

```js
const user = { name: "Alex", age: 25 };
const { name, age } = user;

const colors = ["red", "blue"];
const [first, second] = colors;
```

### 📤 Spread & rest

Spread expands values. Rest collects remaining values.

```js
const original = [1, 2];
const copy = [...original, 3];

function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}

console.log(copy);       // [1, 2, 3]
console.log(sum(1, 2, 3)); // 6
```

### 🛡️ Optional chaining

Safely access nested properties that might not exist.

```js
const user = {};

console.log(user.profile?.email); // undefined
```

### 🔄 Essential array methods

```js
const numbers = [1, 2, 3, 4, 5];

numbers.map(n => n * 2);
// [2, 4, 6, 8, 10]

numbers.filter(n => n > 3);
// [4, 5]

numbers.find(n => n > 3);
// 4

numbers.reduce((sum, n) => sum + n, 0);
// 15
```

|Method|Purpose|
|---|---|
|`map()`|Transform every element|
|`filter()`|Keep matching elements|
|`find()`|Return the first match|
|`reduce()`|Combine elements into one result|

💡 These methods usually leave the original array unchanged. Prefer them when transforming data.

---

## ✨ 5. Modern JavaScript

### 📝 Template literals

```js
const name = "Alex";
console.log(`Hello, ${name}!`);
```

### 📦 Modules

Modules let you split code across files.

**math.js**

```js
export const add = (a, b) => a + b;
```

**app.js**

```js
import { add } from "./math.js";

console.log(add(2, 3)); // 5
```

For Node.js, use `.mjs` files or configure `"type": "module"` in `package.json` for this ES module syntax.

### 🏗️ Classes

Classes provide syntax for creating objects with shared behavior.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hi, ${this.name}!`;
  }
}

const user = new User("Alex");
console.log(user.greet()); // Hi, Alex!
```

### 🤝 Promises

A Promise represents a value that may become available later.

```js
const task = Promise.resolve("Done!");

task.then(result => console.log(result));
```

### 🔁 Iterators

Iterators produce values one at a time. Generators make them easy to create.

```js
function* ids() {
  yield 1;
  yield 2;
  yield 3;
}

console.log([...ids()]); // [1, 2, 3]
```

---

## 🚨 6. Error Handling

Errors happen. Handle expected failures and report useful messages.

### 🧯 try...catch

```js
try {
  JSON.parse("{invalid}");
} catch (error) {
  console.error("Could not parse JSON:", error.message);
}
```

### 💥 Throwing errors

```js
function withdraw(balance, amount) {
  if (amount > balance) {
    throw new Error("Insufficient funds");
  }

  return balance - amount;
}
```

### 🏷️ Custom errors

```js
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}

throw new ValidationError("Email is required");
```

💡 Throw errors when an operation cannot proceed. Catch them where you can handle them meaningfully.

---

# ⚡ 7. Asynchronous JavaScript

Asynchronous code lets your application wait for slow operations—such as network requests or file access—without blocking the entire program.

## 📞 Callbacks

A callback runs when an operation completes.

```js
import { readFile } from "node:fs";

readFile("notes.txt", "utf8", (error, data) => {
  if (error) {
    console.error(error.message);
    return;
  }

  console.log(data);
});
```

💡 Node.js APIs often use error-first callbacks: `(error, result)`.

## 🤝 Promises & chaining

```js
fetch("https://jsonplaceholder.typicode.com/todos/1")
  .then(response => {
    if (!response.ok) throw new Error("Request failed");
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error(error.message));
```

Each `.then()` can transform a result or return another Promise. `.catch()` handles failures in the chain.

### 🧠 Promise combinators

```js
const tasks = [
  Promise.resolve("A"),
  Promise.resolve("B")
];

await Promise.all(tasks);        // ["A", "B"]
await Promise.allSettled(tasks); // Status of every task
await Promise.race(tasks);       // First settled result
await Promise.any(tasks);        // First fulfilled result
```

|Method|Behavior|
|---|---|
|`Promise.all()`|All must fulfill; rejects if one rejects|
|`Promise.allSettled()`|Waits for every outcome|
|`Promise.race()`|First settled Promise wins|
|`Promise.any()`|First fulfilled Promise wins|

⚠️ The examples use top-level `await`, which works in ES modules. `Promise.any()` rejects if every input rejects.

## ⏳ async / await

Makes Promise-based code easier to read.

```js
async function getTodo() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/todos/1"
    );

    if (!response.ok) throw new Error("HTTP error");

    return await response.json();
  } catch (error) {
    console.error("Failed:", error.message);
    throw error;
  }
}

getTodo().then(console.log).catch(() => {});
```

💡 `await` pauses the surrounding async function until a Promise settles. It does not block the entire JavaScript thread.

## 🔄 The event loop

JavaScript runs synchronous code on the call stack. Asynchronous work schedules callbacks or Promise reactions for later execution.

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

**Output:**

```js
1
4
3
2
```

Why?

1. `1` and `4` run synchronously.
2. Promise reactions run as microtasks.
3. The timer callback runs in a later event-loop task.

### 🧠 Key terms

- **Call stack:** Executes the current functions.
- **Microtasks:** Promise reactions and similar queued work.
- **Macrotasks / tasks:** Timer callbacks and other event-loop tasks.
- **Event loop:** Coordinates execution and queued work.

## ⚖️ Concurrency vs. parallelism

- **Concurrency:** Multiple tasks make progress over overlapping periods.
- **Parallelism:** Multiple tasks execute at the same time.

Node.js can handle many I/O operations concurrently. CPU-intensive JavaScript generally runs on the main thread unless you use tools such as worker threads or other processes.

---

**Learning tip:** Don't memorize every method. Learn the idea, run the code, break it intentionally, and fix it. That's how you build real backend skills.

