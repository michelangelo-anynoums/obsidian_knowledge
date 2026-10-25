# 🛡️ Error Handling in JavaScript

> [!abstract] 💡 What is error handling? It allows us to catch errors and prevent our program from crashing unexpectedly.

## ⚠️ 1. `try...catch`

Use `try` to run code and `catch` to handle errors.

```js
try {
  console.log(unknownVariable);
} catch (error) {
  console.log("Something went wrong!");
  console.log(error.message);
}
```

- `try` → executes code.
- `catch` → handles an error.
- `error.message` → describes the error.

## 🧹 2. `finally`

Runs whether an error occurs or not.

```js
try {
  console.log("Working...");
} catch (error) {
  console.log("Error occurred!");
} finally {
  console.log("Always executed");
}
```

💡 Useful for cleanup tasks.

## 🚨 3. Throw Your Own Errors

Use `throw` to create an error when something is invalid.

```js
function divide(a, b) {
  if (b === 0) {
    throw new Error("Cannot divide by zero!");
  }

  return a / b;
}

try {
  console.log(divide(10, 0));
} catch (error) {
  console.log(error.message);
}
```

## 🔍 4. Validate Input

Check data before processing it.

```js
function greet(name) {
  if (!name) {
    throw new Error("Name is required!");
  }

  return `Hello, ${name}!`;
}

console.log(greet("Alex"));
// Hello, Alex!

// greet(""); → throws an error
```

## 🔗 5. Promise Error Handling

Use `.catch()` with promises.

```js
fetch("/api/users")
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error(error.message));
```

💡 `fetch()` does not automatically reject for HTTP errors like `404`.

## ⚡ 6. Async/Await + Try/Catch

A clean way to handle asynchronous errors.

```js
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const users = await response.json();
    console.log(users);

  } catch (error) {
    console.error("Failed:", error.message);
  }
}

getUsers();
```

## 🧠 7. Common Error Types

|Error|Meaning|
|---|---|
|`SyntaxError`|Invalid syntax or JSON|
|`ReferenceError`|Variable doesn't exist|
|`TypeError`|Invalid operation on a value|
|`RangeError`|Value outside an allowed range|
|`Error`|General-purpose error|

Example:

```js
try {
  JSON.parse("{invalid JSON}");
} catch (error) {
  console.log(error.name); // SyntaxError
}
```

## ✅ 8. Best Practices

- 🎯 Catch errors you can actually handle.
- 📝 Use clear, descriptive error messages.
- 🛡️ Validate input before using it.
- 🔄 Use `try...catch` with `await`.
- 🚫 Don't silently ignore errors.
- 🔐 Never expose passwords, tokens, or sensitive data in error messages.

---

> [!success] 🎯 Key takeaway
> 
> - `try...catch` → handle errors.
> - `throw new Error()` → create errors.
> - `finally` → run cleanup code.
> - `.catch()` → handle promise rejections.
> - `async/await` + `try...catch` → handle asynchronous errors.

