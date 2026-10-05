# 🟢 JAVASCRIPT — FETCH API

### 🎯 Goal

Learn how to **request data from APIs**, send data to servers, handle responses, and deal with loading and errors.

---

# 1. What is `fetch()`?

`fetch()` is a built-in JavaScript function used to make **HTTP requests**.

You can use it to:

- Get data from an API
    
- Send data to a server
    
- Update existing data
    
- Delete data
    
- Work with JSON
    
- Handle loading and errors
    

Basic example:

```js
fetch("https://api.example.com/users");
```

Think of it as:

**JavaScript → Request → Server/API → Response → JavaScript**

---

# 2. The Basic `fetch()`

```js
fetch("https://api.example.com/users")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error(error);
  });
```

There are three important parts:

```js
fetch()
.then()
.catch()
```

### What happens?

1. `fetch()` sends the request.
    
2. The server sends a response.
    
3. `response.json()` reads the response as JSON.
    
4. `.then()` receives the data.
    
5. `.catch()` handles certain errors.
    

---

# 3. `fetch()` Returns a Promise

`fetch()` is **asynchronous**.

It doesn't immediately give you the final data.

```js
const response = fetch(url);
```

`response` is a **Promise**.

Think:

```text
fetch()
   ↓
Promise
   ↓
Response
   ↓
JSON data
```

That's why we use either:

```js
.then()
```

or:

```js
async / await
```

---

# 4. Using `.then()`

The traditional approach:

```js
fetch(url)
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error(error);
  });
```

Each `.then()` receives the result from the previous step.

```text
fetch()
  ↓
response
  ↓
response.json()
  ↓
data
```

---

# 5. Using `async / await`

This is usually easier to read.

```js
async function getUsers() {
  const response = await fetch(url);
  const data = await response.json();

  console.log(data);
}
```

`await` means:

> "Wait for this Promise to finish before continuing."

---

# 6. `try / catch`

When using `async / await`, use `try / catch` for error handling.

```js
async function getUsers() {
  try {
    const response = await fetch(url);
    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

Think:

```text
try
 ↓
Request
 ↓
Response
 ↓
Data

If something fails
 ↓
catch
```

---

# 7. Checking `response.ok`

One important thing beginners often miss:

**fetch() does not automatically reject the Promise for HTTP errors such as 404 or 500.**

So check:

```js
if (!response.ok) {
  throw new Error("Request failed");
}
```

Example:

```js
async function getUsers() {
  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

---

# 8. HTTP Status Codes

You should understand the basic status codes.

### `2xx` — Success

```text
200 OK
201 Created
204 No Content
```

### `3xx` — Redirect

```text
301
302
```

### `4xx` — Client Error

```text
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
```

### `5xx` — Server Error

```text
500 Internal Server Error
502 Bad Gateway
503 Service Unavailable
```

You can check the status:

```js
console.log(response.status);
```

---

# 9. Reading JSON

A very common API response is JSON.

```js
const response = await fetch(url);
const data = await response.json();
```

Important:

```js
response
```

is **not yet your data**.

You need:

```js
response.json()
```

And because it returns a Promise:

```js
await response.json()
```

So:

```js
const response = await fetch(url);
const data = await response.json();
```

---

# 10. Other Response Methods

`response` has several methods for reading the response body.

### JSON

```js
await response.json();
```

### Text

```js
await response.text();
```

### Blob

Useful for files/images:

```js
await response.blob();
```

### ArrayBuffer

Useful for binary data:

```js
await response.arrayBuffer();
```

Most API work uses:

```js
response.json()
```

---

# 11. GET Request

`GET` means:

> "Give me some data."

```js
const response = await fetch(
  "https://api.example.com/users"
);

const users = await response.json();
```

GET is the default method:

```js
fetch(url);
```

is essentially:

```js
fetch(url, {
  method: "GET"
});
```

---

# 12. POST Request

`POST` usually means:

> "Create/send some data."

```js
const response = await fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "John",
    age: 25
  })
});

const data = await response.json();
```

Important:

```js
JSON.stringify()
```

converts a JavaScript object into a JSON string.

```js
{
  name: "John"
}
```

becomes:

```json
{"name":"John"}
```

---

# 13. Headers

Headers provide additional information about the request.

Example:

```js
headers: {
  "Content-Type": "application/json"
}
```

This tells the server:

> "I'm sending JSON."

You can send other headers too:

```js
headers: {
  "Content-Type": "application/json",
  "Authorization": "Bearer TOKEN"
}
```

---

# 14. PUT Request

`PUT` is commonly used to **replace/update** a resource.

```js
await fetch(url, {
  method: "PUT",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "John",
    age: 30
  })
});
```

---

# 15. PATCH Request

`PATCH` is commonly used to **partially update** a resource.

```js
await fetch(url, {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    age: 30
  })
});
```

Difference:

```text
PUT   → replace/update the resource
PATCH → update part of the resource
```

The exact behavior depends on the API.

---

# 16. DELETE Request

`DELETE` is used to delete a resource.

```js
const response = await fetch(url, {
  method: "DELETE"
});
```

Some APIs return no body after DELETE.

In that case, don't blindly do:

```js
await response.json();
```

If the response is `204 No Content`, there may be nothing to parse.

---

# 17. Request Options

The second argument to `fetch()` is an options object.

```js
fetch(url, {
  method: "POST",
  headers: {},
  body: "",
  credentials: "include",
  signal: controller.signal
});
```

Common options:

```text
method
headers
body
credentials
signal
mode
cache
```

You don't need all of them immediately.

Focus first on:

```text
method
headers
body
```

---

# 18. Sending Form Data

You don't always send JSON.

For HTML-style form data:

```js
const formData = new FormData();

formData.append("username", "john");
formData.append("email", "john@example.com");

await fetch(url, {
  method: "POST",
  body: formData
});
```

When using `FormData`, normally **do not manually set**:

```js
"Content-Type": "multipart/form-data"
```

The browser needs to set the correct boundary automatically.

---

# 19. URLSearchParams

Another useful format is URL-encoded data.

```js
const params = new URLSearchParams();

params.append("username", "john");
params.append("age", "25");

await fetch(url, {
  method: "POST",
  body: params
});
```

---

# 20. Query Parameters

You can add information to a URL:

```text
https://api.example.com/users?page=2&limit=10
```

Using JavaScript:

```js
const params = new URLSearchParams({
  page: 2,
  limit: 10
});

const response = await fetch(
  `https://api.example.com/users?${params}`
);
```

This is safer and cleaner than manually building complicated query strings.

---

# 21. Dynamic URLs

You can use variables:

```js
const userId = 5;

const response = await fetch(
  `https://api.example.com/users/${userId}`
);
```

---

# 22. Authentication

Some APIs require authentication.

A common pattern is a Bearer token:

```js
const response = await fetch(url, {
  headers: {
    Authorization: `Bearer ${token}`
  }
});
```

The server uses the token to identify or authorize the request.

### ⚠️ Important

Never casually put secret API keys in frontend JavaScript.

Anything shipped to a browser can potentially be inspected by users.

Secrets that must remain secret should generally be handled by a backend/server-side environment.

---

# 23. Cookies and Credentials

Sometimes authentication uses cookies.

You may need:

```js
fetch(url, {
  credentials: "include"
});
```

This tells the browser to include credentials such as cookies where permitted.

Whether this works depends on the server's cookie and CORS configuration.

---

# 24. CORS

You may eventually see an error related to:

**CORS — Cross-Origin Resource Sharing**

For example:

```text
Frontend
localhost:3000

        ↓ request

API
api.example.com
```

These are different origins.

The API must allow your frontend's origin according to its CORS policy.

### Important

CORS is primarily a **browser security mechanism**.

You generally cannot fix a server's CORS policy simply by adding random headers to your frontend request.

The server needs to be configured appropriately.

---

# 25. Loading State

When requesting data, the UI usually needs three states:

```text
Loading
Success
Error
```

Example:

```js
let loading = true;

try {
  const response = await fetch(url);
  const data = await response.json();

  loading = false;
} catch (error) {
  loading = false;
}
```

In React, this becomes especially important because you'll normally represent these states with React state.

---

# 26. A Complete Fetch Function

A good basic pattern:

```js
async function getUsers() {
  try {
    const response = await fetch(
      "https://api.example.com/users"
    );

    if (!response.ok) {
      throw new Error(
        `HTTP error: ${response.status}`
      );
    }

    const data = await response.json();

    return data;
  } catch (error) {
    console.error("Failed to fetch users:", error);
    throw error;
  }
}
```

Then:

```js
const users = await getUsers();
console.log(users);
```

---

# 27. Fetch in React

This is where `fetch()` becomes especially useful.

A common pattern is:

```jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function getUsers() {
      try {
        const response = await fetch(
          "https://api.example.com/users"
        );

        if (!response.ok) {
          throw new Error("Failed to fetch users");
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

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}
```

### The flow

```text
Component renders
      ↓
useEffect runs
      ↓
fetch()
      ↓
API responds
      ↓
response.json()
      ↓
setUsers()
      ↓
React re-renders
      ↓
Users appear
```

---

# 28. Why `useEffect()`?

If you want to fetch data when a React component loads, you commonly use:

```js
useEffect(() => {
  // fetch data
}, []);
```

The empty dependency array:

```js
[]
```

means the effect is set up to run after the initial mount.

---

# 29. Fetch Based on a Variable

For example, fetching a specific user:

```jsx
useEffect(() => {
  async function getUser() {
    const response = await fetch(
      `/api/users/${userId}`
    );

    const data = await response.json();

    setUser(data);
  }

  getUser();
}, [userId]);
```

Now when `userId` changes, the effect runs again.

---

# 30. Abort a Fetch

Sometimes a component starts a request and then the request is no longer needed.

You can use `AbortController`.

```js
const controller = new AbortController();

fetch(url, {
  signal: controller.signal
});
```

Cancel it with:

```js
controller.abort();
```

In React:

```jsx
useEffect(() => {
  const controller = new AbortController();

  async function getUsers() {
    try {
      const response = await fetch(url, {
        signal: controller.signal
      });

      const data = await response.json();

      setUsers(data);
    } catch (error) {
      if (error.name !== "AbortError") {
        setError(error.message);
      }
    }
  }

  getUsers();

  return () => {
    controller.abort();
  };
}, []);
```

This is useful for preventing unnecessary work when a request is no longer relevant.

---

# 31. Common Mistake: Forgetting `await response.json()`

❌ Wrong:

```js
const response = await fetch(url);

console.log(response);
```

This gives you the **Response object**, not the actual JSON data.

✅ Correct:

```js
const response = await fetch(url);
const data = await response.json();

console.log(data);
```

---

# 32. Common Mistake: Forgetting `response.ok`

❌ This isn't enough:

```js
const response = await fetch(url);
const data = await response.json();
```

A `404` or `500` response does not necessarily cause `fetch()` itself to throw.

Better:

```js
if (!response.ok) {
  throw new Error(`HTTP error: ${response.status}`);
}
```

---

# 33. Common Mistake: Forgetting `JSON.stringify()`

❌ Wrong:

```js
body: {
  name: "John"
}
```

For a JSON request, use:

```js
body: JSON.stringify({
  name: "John"
})
```

And usually:

```js
headers: {
  "Content-Type": "application/json"
}
```

---

# 34. Common Mistake: Calling `response.json()` Twice

❌ Don't do:

```js
const data1 = await response.json();
const data2 = await response.json();
```

The response body is generally consumed once.

Instead:

```js
const data = await response.json();
```

Then use:

```js
data
```

as much as you need.

---

# 35. Common Mistake: Not Handling Errors

❌

```js
const response = await fetch(url);
const data = await response.json();
```

Better:

```js
try {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error("Request failed");
  }

  const data = await response.json();
} catch (error) {
  console.error(error);
}
```

---

# 36. `Promise.all()`

If you need multiple requests at the same time:

```js
const [usersResponse, postsResponse] = await Promise.all([
  fetch("/api/users"),
  fetch("/api/posts")
]);
```

Then:

```js
const users = await usersResponse.json();
const posts = await postsResponse.json();
```

This is useful when requests are independent.

---

# 37. `Promise.allSettled()`

Sometimes you want **all requests to finish**, even if one fails.

```js
const results = await Promise.allSettled([
  fetch("/api/users"),
  fetch("/api/posts")
]);
```

Useful when one failed request shouldn't prevent you from seeing the results of the others.

---

# 38. Request Timeout

`fetch()` does not automatically give you a simple built-in timeout option like:

```js
timeout: 5000
```

A common approach is `AbortController`.

```js
const controller = new AbortController();

const timeout = setTimeout(() => {
  controller.abort();
}, 5000);

try {
  const response = await fetch(url, {
    signal: controller.signal
  });

  const data = await response.json();
} finally {
  clearTimeout(timeout);
}
```

Now the request is aborted after approximately 5 seconds.

---

# 39. The `Response` Object

After:

```js
const response = await fetch(url);
```

you have a `Response` object.

Useful properties include:

```js
response.ok
response.status
response.statusText
response.headers
response.url
```

And methods:

```js
response.json()
response.text()
response.blob()
```

---

# 40. Reading Response Headers

You can access headers:

```js
console.log(response.headers);
```

Or retrieve a specific header:

```js
const contentType =
  response.headers.get("content-type");
```

---

# 41. Request Headers vs Response Headers

Don't confuse these.

### Request headers

Information **you send to the server**:

```js
fetch(url, {
  headers: {
    Authorization: `Bearer ${token}`
  }
});
```

### Response headers

Information **the server sends back**:

```js
response.headers.get("content-type");
```

---

# 42. A Useful Mental Model

Think about `fetch()` as a conversation:

```text
YOU
 │
 │  fetch(url)
 ↓
SERVER
 │
 │  Response
 ↓
YOU
 │
 │  response.json()
 ↓
DATA
```

For POST:

```text
YOU
 │
 │  Request + data
 ↓
SERVER
 │
 │  Response
 ↓
YOU
 │
 │  Read response
 ↓
RESULT
```

---

# 43. CRUD + Fetch

A very useful thing to memorize:

```text
CREATE → POST
READ   → GET
UPDATE → PUT / PATCH
DELETE → DELETE
```

Example:

```js
// READ
fetch("/users");

// CREATE
fetch("/users", {
  method: "POST"
});

// UPDATE
fetch("/users/1", {
  method: "PATCH"
});

// DELETE
fetch("/users/1", {
  method: "DELETE"
});
```

---

# 44. The Fetch Pattern to Memorize

For GET requests:

```js
async function getData() {
  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    const data = await response.json();

    return data;
  } catch (error) {
    console.error(error);
  }
}
```

For POST:

```js
async function createData(data) {
  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(data)
  });

  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  return response.json();
}
```

---

# 🧠 What You Should Know

Before moving on, make sure you understand:

- `fetch()`
    
- Promises
    
- `async / await`
    
- `try / catch`
    
- `response.ok`
    
- `response.status`
    
- `response.json()`
    
- GET
    
- POST
    
- PUT
    
- PATCH
    
- DELETE
    
- Headers
    
- JSON
    
- `JSON.stringify()`
    
- Query parameters
    
- Authentication
    
- Cookies / credentials
    
- CORS
    
- Loading states
    
- Error states
    
- `AbortController`
    
- `Promise.all()`
    
- Fetching data in React with `useEffect()`
    

---

# 🎯 Final Goal

You should be able to look at an API and confidently do this:

```text
1. Send a request
       ↓
2. Wait for the response
       ↓
3. Check for errors
       ↓
4. Read the response
       ↓
5. Get the data
       ↓
6. Store/use the data
       ↓
7. Show loading/error/success states
```

### ⭐ The Core Pattern

```js
try {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  const data = await response.json();

  // Use data here
} catch (error) {
  // Handle error here
}
```

---
