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
    

```js
const promise = new Promise((resolve, reject) => {
  // Do something...

  resolve("Success!");
  // reject("Something went wrong!");
});
```

## `.then()` and `.catch()`

Use `.then()` when the Promise succeeds and `.catch()` when it fails.

```js
promise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error);
  });
```

Output:

```text
Success!
```

### 🧩 A Simple Example

```js
function getUser() {
  return new Promise((resolve, reject) => {
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

---

## 🔗 Chaining Promises

You can run asynchronous operations one after another:

```js
getUser()
  .then(user => getProfile(user))
  .then(profile => console.log(profile))
  .catch(error => console.error(error));
```

Each `.then()` can return another Promise.

---

## 🚀 Running Promises Together

Use `Promise.all()` when multiple Promises can run at the same time.

```js
const user = getUser();
const posts = getPosts();

Promise.all([user, posts])
  .then(([userData, postData]) => {
    console.log(userData);
    console.log(postData);
  })
  .catch(error => console.error(error));
```

> [!important] Key idea  
> **Promises are mainly used to handle asynchronous work**, such as API requests, timers, reading files, or database operations.

## 🧠 Quick Reference

|Method|Purpose|
|---|---|
|`new Promise()`|Create a Promise|
|`resolve()`|Mark it as successful|
|`reject()`|Mark it as failed|
|`.then()`|Handle success|
|`.catch()`|Handle errors|
|`.finally()`|Run code after completion|
|`async`|Make a function return a Promise|
|`await`|Wait for a Promise's result|
|`Promise.all()`|Wait for multiple Promises|

### 🎯 In One Sentence

**A Promise represents a value that will be available now, later, or never.**