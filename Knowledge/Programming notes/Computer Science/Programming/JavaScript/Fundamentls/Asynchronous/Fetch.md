# 🌐 JavaScript Fetch API — Complete Beginner's Guide

> [!abstract] Goal Learn how to request data from an API, understand HTTP headers and `Content-Type`, handle responses and errors, and use `fetch()` correctly in React.

## 1. What Is `fetch()`?

`fetch()` is a built-in JavaScript function that allows your application to communicate with a server or API.

You can use it to:

- **GET** — Retrieve data.
- **POST** — Send or create data.
- **PUT** — Replace existing data.
- **PATCH** — Partially update data.
- **DELETE** — Delete data.

Example:

```js
fetch("https://jsonplaceholder.typicode.com/users");
```

This sends a request to an API that provides user data.

**Important:** `fetch()` is asynchronous. It returns a Promise rather than the actual data immediately.

---

## 2. Basic Fetch Example — Explained Line by Line

This is one of the most important patterns to learn.

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
    console.error("Request failed:", error);
  }
}

getUsers();
```

### Understanding Every Line

**Line 1 — Create an asynchronous function**

```js
async function getUsers() {
```

- `async` allows the function to use `await`.
- `function` declares a function.
- `getUsers` is the function's name.
- `{` starts the function body.

**Line 2 — Start error handling**

```js
try {
```

The `try` block contains code that might throw an error, including a rejected Promise when awaited.

**Line 3 — Send the request**

```js
const response = await fetch(
  "https://jsonplaceholder.typicode.com/users"
);
```

- `fetch()` sends an HTTP request.
- The URL identifies the API endpoint.
- `await` waits for the Promise to settle.
- `const response` stores the resulting `Response` object.

The response contains information such as the HTTP status, headers, and body.

**Line 4 — Check the HTTP status**

```js
if (!response.ok) {
```

- `response.ok` is `true` when the HTTP status is between `200` and `299`.
- `!` means NOT.
- Therefore, this condition runs when the HTTP response is not successful.

**Line 5 — Throw an error**

```js
throw new Error(`HTTP error: ${response.status}`);
```

If the server returns an unsuccessful status, this creates an error containing the status code, such as `404` or `500`.

Throwing the error transfers control to the `catch` block.

**Line 6 — Read the response body**

```js
const data = await response.json();
```

- `response.json()` reads the response body and parses it as JSON.
- It returns a Promise.
- `await` waits for the parsed data.
- `data` stores the resulting JavaScript value, such as an array or object.

**Line 7 — Use the data**

```js
console.log(data);
```

This prints the data to the console. In React, you would usually store it in state using `setUsers(data)`.

**Line 8 — Catch errors**

```js
} catch (error) {
  console.error("Request failed:", error);
}
```

This catches errors from the awaited fetch, the explicit `throw`, and JSON parsing.

**Final line — Call the function**

```js
getUsers();
```

Defining a function does not run it. This line executes it.

> [!tip] Remember `fetch()` gets the response. `response.json()` reads and parses the body. React state stores the data you want to display.

---

## 3. What Does `fetch()` Return?

`fetch()` returns a **Promise that normally resolves to a** **`Response`** **object**.

```js
const response = await fetch("/api/users");
```

It does not return the actual users directly.

The process looks like this:

```js
fetch(url)
    |
    v
Promise<Response>
    |
    v
Response object
    |
    v
response.json()
    |
    v
Promise containing parsed data
    |
    v
JavaScript array or object
```

### What Happens When Something Fails?

|Situation|Result|
|---|---|
|HTTP `200`|Usually resolves with a `Response`|
|HTTP `404`|Usually resolves with a `Response`|
|HTTP `500`|Usually resolves with a `Response`|
|Network failure|Fetch Promise rejects|
|CORS failure|Fetch Promise usually rejects|
|Aborted request|Fetch Promise rejects|
|Invalid JSON|`response.json()` rejects|

> [!warning] Important `fetch()` does **not** automatically reject for HTTP errors such as `404` or `500`. Check `response.ok` yourself.

---

## 4. The Most Important HTTP Headers

Headers provide extra information about a request or response.

### Request Headers

|Header|Purpose|
|---|---|
|`Accept`|Specifies the response formats the client accepts|
|`Content-Type`|Describes the format of the request body|
|`Authorization`|Sends authentication credentials, often a bearer token|
|`Cache-Control`|Gives caching instructions|
|`Accept-Language`|Indicates preferred languages|
|`If-None-Match`|Makes a conditional request using an ETag|

### Response Headers

|Header|Purpose|
|---|---|
|`Content-Type`|Describes the response body's format|
|`Cache-Control`|Provides caching instructions|
|`Content-Length`|Indicates the content size, when provided|
|`ETag`|Identifies a particular version of a resource|
|`Location`|Indicates a resource location or redirect destination|
|`Retry-After`|Indicates when a request may be retried|
|`Access-Control-Allow-Origin`|Indicates which origin is allowed by CORS|

Some headers are controlled by the browser or server and cannot be set freely from frontend JavaScript.

### `Accept` vs. `Content-Type`

```js
headers: {
  Accept: "application/json",
  "Content-Type": "application/json",
}
```

- `Accept` — The format you want to receive.
- `Content-Type` — The format of the body you are sending.

For example, a request may send JSON and expect JSON back.

---

## 5. Content-Type — The Most Important Types

The `Content-Type` header tells the recipient how to interpret the body.

There is no finite list of every possible media type, because custom and application-specific types can exist. These are the most useful ones to recognize.

### A. JSON

**MIME type:** `application/json`

Used to send and receive JSON data.

```js
fetch("/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Accept: "application/json",
  },
  body: JSON.stringify({
    name: "Alex",
    age: 25,
  }),
});
```

- `JSON.stringify()` converts a JavaScript value into a JSON string.
- `Content-Type` tells the server that the request body is JSON.

Common JSON-related media types include:

- `application/json` — Standard JSON.
- `application/problem+json` — Structured error information using the Problem Details format.
- `application/ld+json` — JSON-LD linked data.

### B. Plain Text

**MIME type:** `text/plain`

Used for ordinary text.

```js
fetch("/api/message", {
  method: "POST",
  headers: {
    "Content-Type": "text/plain",
  },
  body: "Hello, server!",
});
```

### C. HTML

**MIME type:** `text/html`

Used for HTML documents.

```js
const response = await fetch("/page.html");
const html = await response.text();

console.log(html);
```

`response.text()` reads text. It does not automatically render the returned HTML as a webpage.

### D. CSS

**MIME type:** `text/css`

Used for CSS stylesheet content.

### E. JavaScript

Common MIME types include:

- `text/javascript`
- `application/javascript` — An older, commonly encountered value.

These identify JavaScript content. They are not typical request-body types for JSON APIs.

### F. URL-Encoded Form Data

**MIME type:** `application/x-www-form-urlencoded`

Used for form fields encoded as key-value pairs.

```js
const body = new URLSearchParams({
  username: "alex",
  email: "alex@example.com",
});

fetch("/api/login", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded",
  },
  body,
});
```

The encoded body looks like:

```js
username=alex&email=alex%40example.com
```

This format is common in traditional web forms and some authentication endpoints.

### G. Multipart Form Data

**MIME type:** `multipart/form-data`

Used for forms containing multiple fields, especially file uploads.

```js
const formData = new FormData();

formData.append("username", "alex");
formData.append("avatar", fileInput.files[0]);

fetch("/api/upload", {
  method: "POST",
  body: formData,
});
```

> [!warning] Do not set the multipart header manually When using browser `FormData`, let the browser set `Content-Type` and its required boundary automatically.

### H. XML

**MIME type:** `application/xml` or `text/xml`

Used for XML documents, including some older APIs and integrations.

```js
const response = await fetch("/api/data.xml");
const xml = await response.text();
```

Reading XML as text does not parse it into an XML document. Use `DOMParser` if you need to process it as XML.

### I. Binary Data and Files

|MIME type|Typical content|
|---|---|
|`application/octet-stream`|Generic binary data|
|`application/pdf`|PDF documents|
|`application/zip`|ZIP archives|
|`application/gzip`|Gzip-compressed files|
|`image/jpeg`|JPEG images|
|`image/png`|PNG images|
|`image/gif`|GIF images|
|`image/webp`|WebP images|
|`image/svg+xml`|SVG images|
|`audio/mpeg`|MP3 audio|
|`audio/ogg`|Ogg audio|
|`video/mp4`|MP4 video|

For binary response data, use methods such as `response.blob()` or `response.arrayBuffer()` rather than `response.json()`.

### J. Other Common Media Types

|MIME type|Purpose|
|---|---|
|`application/pdf`|PDF files|
|`application/zip`|ZIP files|
|`application/octet-stream`|Generic binary data|
|`application/wasm`|WebAssembly modules|
|`application/graphql-response+json`|GraphQL response data|
|`application/manifest+json`|Web app manifest|
|`application/rss+xml`|RSS feeds|
|`application/atom+xml`|Atom feeds|
|`application/x-ndjson`|Newline-delimited JSON in some APIs|
|`text/csv`|Comma-separated values|
|`text/event-stream`|Server-Sent Events streams|

> [!note] Important distinction `Content-Type` describes the body format. It does not determine which HTTP method to use or whether the request will succeed.

---

## 6. Reading Different Response Types

Choose the body-reading method based on the response format.

```js
const response = await fetch("/api/data");
```

|Method|What it returns|
|---|---|
|`response.json()`|Promise resolving to parsed JSON|
|`response.text()`|Promise resolving to a string|
|`response.blob()`|Promise resolving to a `Blob`|
|`response.arrayBuffer()`|Promise resolving to an `ArrayBuffer`|
|`response.formData()`|Promise resolving to `FormData`|
|`response.bytes()`|Promise resolving to a byte array in supporting runtimes|

Example with text:

```js
const response = await fetch("/api/message");
const message = await response.text();

console.log(message);
```

Example with JSON:

```js
const response = await fetch("/api/users");
const users = await response.json();

console.log(users);
```

> [!warning] Read the body once Response bodies are streams. Once consumed, the same body cannot normally be read again. Use `response.clone()` before reading if you genuinely need two copies.

---

## 7. HTTP Methods and Request Bodies

|Method|Common purpose|Usually has a body?|
|---|---|---|
|`GET`|Retrieve data|No|
|`POST`|Create data or submit an operation|Yes|
|`PUT`|Replace a resource|Yes|
|`PATCH`|Partially update a resource|Yes|
|`DELETE`|Request deletion|Usually no, but some APIs support one|

Example `GET`:

```js
const response = await fetch("/api/users");
```

Example `POST`:

```js
const response = await fetch("/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Alex",
  }),
});
```

The API determines which methods and body formats it accepts.

---

## 8. Handling Errors Correctly

A robust fetch pattern handles HTTP errors, network errors, and parsing errors.

```js
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const users = await response.json();

    return users;
  } catch (error) {
    console.error("Failed to get users:", error);
    throw error;
  }
}
```

### Three Things Can Go Wrong

1. **Request failure:** `fetch()` rejects.
2. **HTTP failure:** `fetch()` resolves, but `response.ok` is `false`.
3. **Body parsing failure:** The response exists, but `response.json()` or another body reader rejects.

These are different situations, even though they can all end up in the same `catch` block.

---

## 9. Important `fetch()` Options

```js
fetch("/api/users", {
  method: "GET",
  headers: {
    Accept: "application/json",
  },
  credentials: "same-origin",
  mode: "cors",
  cache: "default",
  redirect: "follow",
});
```

|Option|Purpose|
|---|---|
|`method`|HTTP request method|
|`headers`|Request headers|
|`body`|Data sent in the request|
|`credentials`|Controls sending credentials such as cookies|
|`mode`|Controls request mode and cross-origin behavior|
|`cache`|Controls cache behavior|
|`redirect`|Controls redirect handling|
|`signal`|Supports cancellation|
|`referrer`|Sets the referrer, subject to browser restrictions|
|`referrerPolicy`|Controls referrer information|
|`integrity`|Enables supported integrity checks|
|`keepalive`|Allows certain requests to continue during page unloading|
|`priority`|Provides a priority hint where supported|

You do not need to memorize every option at the beginning. Focus on `method`, `headers`, `body`, `credentials`, and `signal`.

---

## 10. Using Fetch in React

In React, API data is usually stored in state and fetched in an effect when needed.

```js
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function getUsers() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );

        if (!response.ok) {
          throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();
        setUsers(data);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    }

    getUsers();
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  if (users.length === 0) return <p>No users found.</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default Users;
```

### What This Example Teaches

- `useState()` stores data and request status.
- `useEffect()` starts the request after rendering.
- `fetch()` communicates with the API.
- `response.ok` checks HTTP success.
- `response.json()` parses the data.
- `setUsers(data)` updates React state.
- `.map()` renders the list.
- `loading` handles the waiting state.
- `error` handles failure.
- An empty array produces an empty state.
- `finally` runs whether the request succeeds or fails.

For production applications, consider cancellation or stale-response handling if the component unmounts or the requested data changes.

---

## 11. Quick Reference

> [!success] The essential pattern

```js
async function getData() {
  try {
    const response = await fetch("/api/data");

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const data = await response.json();

    return data;
  } catch (error) {
    console.error(error);
    throw error;
  }
}
```

### Remember These Five Rules

1. `fetch()` returns a Promise resolving to a `Response` when the HTTP response is received.
2. Check `response.ok` because HTTP errors do not automatically reject the fetch Promise.
3. Use the correct body reader: `json()`, `text()`, `blob()`, or another suitable method.
4. Match `Content-Type` to the format of the request body.
5. Use `try/catch` to handle rejected requests and body-reading errors.

### Final Mental Model

```js
Request
  |
  v
fetch(url, options)
  |
  v
Response received?
  |
  +--- No ---> Promise rejects ---> catch
  |
  +--- Yes
         |
         v
     Check response.ok
         |
         +--- false ---> Handle HTTP error
         |
         +--- true
                |
                v
           Read the body
                |
                +--- JSON ---> response.json()
                +--- Text ---> response.text()
                +--- File ---> response.blob()
                |
                v
           Use the data
```

**Final takeaway:** `fetch()` handles the HTTP request. The `Response` object describes the server's reply. The body-reading method converts the response body into usable data. Your code must handle HTTP errors, rejected requests, and parsing failures appropriately.

---
