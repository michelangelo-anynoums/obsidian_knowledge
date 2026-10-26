# ⚡ JavaScript Promises

> [!summary] What is a Promise?  
> A **Promise** is an object that represents the eventual result of an **asynchronous operation**.
> 
> Think of it as: **“I’ll give you the result later.”**

## 🔄 Promise States

A Promise can be in one of three states:

- 🟡 **Pending** — still waiting
- 🟢 **Fulfilled** — operation completed successfully
- 🔴 **Rejected** — operation failed

Once a Promise is fulfilled or rejected, it is **settled**. A settled Promise cannot change its state again.

```js
const promise = new Promise((resolve, reject) => {
  // Do something...

  resolve("Success!");
  // reject(new Error("Something went wrong!"));
});
```

## `.then()`, `.catch()` and `.finally()`

Use `.then()` to handle a successful result, `.catch()` to handle an error, and `.finally()` to run cleanup code regardless of the outcome.

```js
promise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error);
  })
  .finally(() => {
    console.log("Operation finished.");
  });
```

Output:

```js
Success!
Operation finished.
```

- `.then(onFulfilled, onRejected)` — handles fulfillment and optionally rejection.
- `.catch(onRejected)` — handles rejection.
- `.finally(onFinally)` — runs after settlement, usually for cleanup. It normally passes through the original result or error.

### 🧩 A Simple Example

```js
function getUser() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("User found!");
    }, 1000);
  });
}

getUser()
  .then(message => console.log(message))
  .catch(error => console.error(error));
```

The Promise waits **1 second**, then resolves with `"User found!"`.

---

## ✨ `async` / `await`

`async` and `await` make Promise-based code easier to read.

```js
async function showUser() {
  try {
    const message = await getUser();
    console.log(message);
  } catch (error) {
    console.error(error);
  }
}

showUser();
```

> [!tip] Remember  
> `await` pauses the **async function** until the Promise settles. It doesn't block the entire JavaScript program.

An `async` function always returns a Promise. If it returns a regular value, that value becomes the fulfillment value of the returned Promise.

---

## 🔗 Chaining Promises

You can run asynchronous operations one after another:

```js
getUser()
  .then(user => getProfile(user))
  .then(profile => console.log(profile))
  .catch(error => console.error(error));
```

Each `.then()` returns a new Promise. Returning a value fulfills the next Promise with that value; returning another Promise makes the chain wait for it.

---

# 🚀 Static Methods of the `Promise` Class

Static methods are called directly on `Promise`, not on an individual Promise instance.

For example:

```js
Promise.all([promise1, promise2]);
```

The four most important methods for combining multiple Promises are:

- `Promise.all()`
- `Promise.allSettled()`
- `Promise.race()`
- `Promise.any()`

## 1. `Promise.all()` — All Must Succeed

**Purpose:** Wait for all Promises to fulfill. If any Promise rejects, the returned Promise rejects immediately with that reason.

```js
const p1 = Promise.resolve("User");
const p2 = Promise.resolve("Posts");
const p3 = Promise.resolve("Comments");

Promise.all([p1, p2, p3])
  .then(results => {
    console.log(results);
  })
  .catch(error => {
    console.error(error);
  });
```

Output:

```js
["User", "Posts", "Comments"]
```

Example with an error:

```js
Promise.all([
  Promise.resolve("Success"),
  Promise.reject(new Error("Request failed")),
  Promise.resolve("Another success")
])
  .then(results => console.log(results))
  .catch(error => console.error(error.message));
```

Output:

```js
Request failed
```

**Important:**

- All Promises must fulfill for the combined Promise to fulfill.
- Results preserve the **input order**, not completion order.
- A rejection does not automatically cancel the other operations.

**Use it when:** You need every result, such as fetching a user, their posts, and their settings.

## 2. `Promise.allSettled()` — Wait for Everything

**Purpose:** Wait until every Promise settles, whether fulfilled or rejected.

```js
const p1 = Promise.resolve("User");
const p2 = Promise.reject(new Error("Posts failed"));
const p3 = Promise.resolve("Settings");

Promise.allSettled([p1, p2, p3])
  .then(results => {
    console.log(results);
  });
```

Output:

```js
[
  { status: "fulfilled", value: "User" },
  { status: "rejected", reason: Error("Posts failed") },
  { status: "fulfilled", value: "Settings" }
]
```

Each result has one of two shapes:

```js
{ status: "fulfilled", value: result }
```

or

```js
{ status: "rejected", reason: error }
```

You can process the results individually:

```js
Promise.allSettled([p1, p2, p3])
  .then(results => {
    results.forEach(result => {
      if (result.status === "fulfilled") {
        console.log("Success:", result.value);
      } else {
        console.error("Error:", result.reason);
      }
    });
  });
```

**Important:** Unlike `Promise.all()`, one rejection does not cause the combined Promise to reject. It waits for every input to settle.

**Use it when:** You want to collect all outcomes, even if some requests fail.

## 3. `Promise.race()` — First to Settle Wins

**Purpose:** Settle with the outcome of the first input Promise to settle, whether fulfilled or rejected.

```js
const p1 = new Promise(resolve => {
  setTimeout(() => resolve("First result"), 1000);
});

const p2 = new Promise(resolve => {
  setTimeout(() => resolve("Second result"), 500);
});

Promise.race([p1, p2])
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

Output:

```js
Second result
```

The second Promise settles first, so its result wins.

If the first Promise to settle rejects, the returned Promise rejects too.

**Use it when:** You need a timeout or want whichever operation settles first.

### Example: Request Timeout

```js
function timeout(ms) {
  return new Promise((_, reject) => {
    setTimeout(() => {
      reject(new Error("Request timed out"));
    }, ms);
  });
}

Promise.race([
  fetch("/api/users"),
  timeout(3000)
])
  .then(response => console.log(response))
  .catch(error => console.error(error.message));
```

> [!warning] Important  
> `Promise.race()` does not cancel the losing operation. The request may continue after the timeout wins.

## 4. `Promise.any()` — First Successful Result Wins

**Purpose:** Fulfill with the first input Promise that fulfills. Rejections are ignored as long as another Promise fulfills.

```js
const p1 = Promise.reject(new Error("Server 1 failed"));
const p2 = Promise.resolve("Server 2 succeeded");
const p3 = Promise.resolve("Server 3 succeeded");

Promise.any([p1, p2, p3])
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

Output:

```js
Server 2 succeeded
```

The first fulfilled Promise wins, even if other Promises reject.

If **every input Promise rejects**, `Promise.any()` rejects with an `AggregateError` containing the individual errors.

```js
Promise.any([
  Promise.reject(new Error("Error A")),
  Promise.reject(new Error("Error B"))
])
  .catch(error => {
    console.log(error instanceof AggregateError); // true
    console.log(error.errors); // [Error A, Error B]
  });
```

**Use it when:** You have multiple servers, mirrors, or alternative sources and only need one successful response.

---

## 🆕 Other Static Promise Methods

### 5. `Promise.resolve()` — Create a Fulfilled Promise

Creates a Promise fulfilled with the supplied value, or adopts the state of a supplied Promise or thenable.

```js
const promise = Promise.resolve("Hello!");

promise.then(value => console.log(value));
```

Output:

```js
Hello!
```

This is useful when you want to convert a regular value into a Promise-compatible value.

```js
function getData() {
  return Promise.resolve({ name: "Alice" });
}

getData().then(data => console.log(data.name));
```

### 6. `Promise.reject()` — Create a Rejected Promise

Creates a Promise rejected with the supplied reason.

```js
const promise = Promise.reject(new Error("Something went wrong"));

promise.catch(error => console.error(error.message));
```

Output:

```js
Something went wrong
```

**Tip:** Prefer `Error` objects over plain strings for rejection reasons because they provide useful debugging information and stack traces.

### 7. `Promise.withResolvers()` — Get a Promise and Its Controls

Available in modern JavaScript environments, this method returns an object containing a Promise and its `resolve` and `reject` functions.

```js
const { promise, resolve, reject } = Promise.withResolvers();

setTimeout(() => {
  resolve("Finished!");
}, 1000);

promise.then(value => console.log(value));
```

Output after one second:

```js
Finished!
```

It is useful when the code that creates a Promise and the code that resolves or rejects it need to be separated.

The traditional alternative is the Promise constructor:

```js
let resolvePromise;

const promise = new Promise(resolve => {
  resolvePromise = resolve;
});

resolvePromise("Finished!");
```

### 8. `Promise.try()` — Start a Function in a Promise Chain

`Promise.try()` is a newer static method, available in modern JavaScript environments. It calls a function and returns a Promise that adopts its result, turning a synchronous throw into a rejection.

```js
Promise.try(() => {
  if (Math.random() > 0.5) {
    throw new Error("Something went wrong");
  }

  return "Success!";
})
  .then(result => console.log(result))
  .catch(error => console.error(error.message));
```

This is useful when a function might either return a value, return a Promise, or throw synchronously, and you want to handle all three cases in the same chain.

---

## 🧠 Quick Reference

### Instance Methods and Language Keywords

|Method / keyword|Purpose|
|---|---|
|`new Promise()`|Create a Promise using an executor function|
|`.then()`|Handle fulfillment and optionally rejection|
|`.catch()`|Handle rejection|
|`.finally()`|Run cleanup after settlement|
|`async`|Declare a function that returns a Promise|
|`await`|Wait for a Promise's result inside an async function|

### Static Methods

|Method|Purpose|Rejects when...|
|---|---|---|
|`Promise.all()`|Wait for all results|Any input rejects|
|`Promise.allSettled()`|Collect every outcome|Normally only if iteration itself fails, not because an input rejects|
|`Promise.race()`|Take the first settled outcome|The first settled input rejects|
|`Promise.any()`|Take the first successful result|All inputs reject|
|`Promise.resolve()`|Fulfill with or adopt a value|The adopted Promise rejects|
|`Promise.reject()`|Create a rejected Promise|It is rejected by design|
|`Promise.withResolvers()`|Return a Promise and its controls|Depends on how it is settled|
|`Promise.try()`|Call a function and normalize its result into a Promise|The function throws or returns a rejected Promise|

> [!note] Compatibility  
> `Promise.all()`, `Promise.race()`, `Promise.resolve()`, and `Promise.reject()` are long-established methods. `Promise.allSettled()` and `Promise.any()` arrived later, while `Promise.withResolvers()` and `Promise.try()` require newer runtimes. Check your target browser or Node.js version when using newer methods.

---

## 🎯 Which Method Should You Choose?

|Situation|Method|
|---|---|
|Every operation must succeed|`Promise.all()`|
|You need every success and failure|`Promise.allSettled()`|
|You want the first operation to finish, even if it fails|`Promise.race()`|
|You want the first successful operation|`Promise.any()`|
|You need a fulfilled Promise from a value|`Promise.resolve()`|
|You need a rejected Promise|`Promise.reject()`|
|You need to settle a Promise from separate code|`Promise.withResolvers()`|
|You want to start a possibly throwing function in a Promise chain|`Promise.try()`|

### 🎯 In One Sentence

**A Promise represents the eventual outcome of an operation, while Promise methods help you handle results, errors, and multiple asynchronous operations in a predictable way.**

---
