# 🌐 JavaScript — Fetch API

The **Fetch API** allows us to make HTTP requests to retrieve or send data to a server. It returns a `Promise` that resolves to a `Response` object.

## 1. Using `async/await`

A clean, modern way to handle requests.

```js
async function getUsers() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/users"
    );

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

getUsers();
```

- `await fetch()` → Waits for the response.
- `response.ok` → Checks whether the status is between 200 and 299.
- `response.json()` → Reads and parses the response body as JSON.
- `try...catch` → Handles network errors and errors thrown in the `try` block.

## 2. Using `.then()` and `.catch()`

The traditional Promise-chaining approach.

```js
fetch("https://jsonplaceholder.typicode.com/users")
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error(error);
  });
```

- `.then()` → Handles a fulfilled Promise and returns a new Promise.
- `.catch()` → Handles rejected Promises and errors thrown in previous handlers.
- `return response.json()` → Passes the parsed data to the next `.then()`.

**Remember:** Both approaches do essentially the same thing. Choose the one that makes your code easier to read.

## 3. Important `Response` Properties

|Property|Description|
|---|---|
|`response.ok`|`true` if the status is 200–299|
|`response.status`|HTTP status code, e.g. `200`, `404`|
|`response.statusText`|Status message, e.g. `"OK"`|
|`response.headers`|Access to response headers|
|`response.url`|Final response URL|
|`response.redirected`|Whether the response followed a redirect|
|`response.type`|Response type, e.g. `"basic"` or `"cors"`|
|`response.body`|Readable stream of the response body|
|`response.bodyUsed`|Whether the body has already been consumed|

## 4. Important `Response` Methods

Use the method that matches the data format you expect.

|Method|Purpose|
|---|---|
|`response.json()`|Parse JSON into JavaScript data|
|`response.text()`|Read the body as text|
|`response.blob()`|Read the body as a `Blob`, useful for files and images|
|`response.arrayBuffer()`|Read the body as binary data|
|`response.formData()`|Parse form data|
|`response.clone()`|Create a copy of the response|
|`response.bytes()`|Read the body as a `Uint8Array` (modern browsers)|

**Important:** These body-reading methods return Promises, and the response body can normally be consumed only once. Use `response.clone()` before reading it twice.

## 5. Sending Data with `fetch()`

Use the `method`, `headers`, and `body` options to configure a request.

```js
fetch("https://example.com/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "Alex",
    age: 25
  })
})
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

Common HTTP methods:

- `GET` → Retrieve data.
- `POST` → Send or create data.
- `PUT` → Replace a resource.
- `PATCH` → Partially update a resource.
- `DELETE` → Delete a resource.

## ⚠️ Important Things to Remember

- **HTTP errors don't automatically reject** **`fetch()`****.** A `404` or `500` usually still resolves to a `Response`; check `response.ok`.
- **Network errors reject the Promise.** For example, a connection failure can be caught with `catch` or `try...catch`.
- **Parse the body separately.** `fetch()` doesn't automatically give you JSON; use `response.json()`.
- **Use** **`JSON.stringify()`** **when sending JSON.** Set the `Content-Type` header to `application/json`.
- **Use** **`AbortController`** **to cancel requests** when necessary.
- **CORS restrictions apply in browsers.** A server must permit cross-origin access when required.

## 🧠 Quick Summary

```js
const response = await fetch(url); // Request
if (!response.ok) throw new Error("Request failed");
const data = await response.json(); // Read data
```

**The basic workflow:** `fetch()` → check the response → read the body → use the data.

---
