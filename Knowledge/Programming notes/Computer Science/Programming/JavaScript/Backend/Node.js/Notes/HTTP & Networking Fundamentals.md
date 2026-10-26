# 🚀 04 — HTTP & Networking Fundamentals

> 💡 **Core idea:** HTTP allows clients and servers to communicate. Node.js provides the tools to build servers, while Express makes the process easier.

## 🌐 1. HTTP Request & Response


```text
Client → Request → Server
Client ← Response ← Server
```

A request contains a **method, URL, headers, and sometimes a body**.


```http
GET /users HTTP/1.1
Host: localhost:3000
```

A response contains a **status code, headers, and sometimes a body**.

```json
{
  "id": 1,
  "name": "Alex"
}
```

## 📬 2. HTTP Methods

|Method|Purpose|
|---|---|
|`GET`|Read data|
|`POST`|Create data|
|`PUT`|Replace data|
|`PATCH`|Update part of data|
|`DELETE`|Delete data|

```text
GET    /users
GET    /users/1
POST   /users
PATCH  /users/1
DELETE /users/1
```

## 🚦 3. Status Codes

|Code|Meaning|
|---|---|
|`200`|✅ Success|
|`201`|✅ Created|
|`204`|✅ Success, no body|
|`400`|❌ Bad request|
|`401`|🔑 Not authenticated|
|`403`|🚫 Forbidden|
|`404`|🔍 Not found|
|`409`|⚠️ Conflict|
|`422`|📝 Validation failed|
|`429`|⏳ Too many requests|
|`500`|💥 Server error|

```js
res.writeHead(201, {
  "Content-Type": "application/json"
});

res.end(JSON.stringify({ id: 1 }));
```

## 📦 4. Headers, JSON & Cookies

Headers describe the request or response.

```http
Content-Type: application/json
Cache-Control: no-store
```

Send JSON:

```js
res.setHeader("Content-Type", "application/json");
res.end(JSON.stringify({ name: "Alex" }));
```

🍪 **Cookies** store small pieces of data in the browser, often for sessions.

🗜️ **Compression** reduces response size using formats such as Gzip or Brotli.

## 🔗 5. URLs & Request Data


```text
/users/42?role=admin
```

- **URL parameter:** `42` — identifies a user.
- **Query parameter:** `role=admin` — filters or modifies a query.
- **Request body:** Data sent with requests such as `POST` or `PATCH`.

```js
const url = new URL(
  "/users/42?role=admin",
  "http://localhost:3000"
);

console.log(url.pathname);              // /users/42
console.log(url.searchParams.get("role")); // admin
```

## 🔒 6. Networking Basics

- 🌍 **DNS:** Converts domain names into IP addresses.
- 🔌 **TCP:** Provides reliable data transport.
- 🔐 **TLS:** Encrypts communication.
- 🔒 **HTTPS:** HTTP protected by TLS.
- 🚪 **Ports:** Identify services on a computer.

```text
DNS → TCP → TLS → HTTP
```

Common ports: `80` (HTTP), `443` (HTTPS), `3000` (development).

## 🛡️ 7. CORS & Caching

**CORS** controls which cross-origin requests browser JavaScript can access.


```text
Access-Control-Allow-Origin: http://localhost:5173
```

**Caching** stores responses to avoid unnecessary requests.

```http
Cache-Control: max-age=60
ETag: "v1"
```

An `ETag` helps a client check whether a cached response has changed.

## 🏗️ 8. REST API Basics

REST-style APIs organize data around resources.

```text
GET    /products
GET    /products/1
POST   /products
PATCH  /products/1
DELETE /products/1
```

Query parameters support filtering, sorting, and pagination.

```text
/products?category=books&sort=price&page=2
```

💡 **Idempotency:** Repeating an operation has the same intended effect on server state. `GET`, `PUT`, and `DELETE` are generally idempotent; `POST` is not necessarily.

⏱️ **Timeouts:** Prevent requests from waiting indefinitely.

🔌 **Connection handling:** Reuse connections when appropriate and handle errors or client disconnections.

## ⚙️ 9. Build a Basic Node.js Server

Before Express, understand the built-in `http` module.

```js
const http = require("node:http");

const server = http.createServer((req, res) => {
  res.setHeader("Content-Type", "application/json");

  if (req.method === "GET" && req.url === "/") {
    res.writeHead(200);
    return res.end(JSON.stringify({
      message: "Hello, Node.js!"
    }));
  }

  res.writeHead(404);
  res.end(JSON.stringify({
    error: "Not found"
  }));
});

server.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

Run it:

```bash
node server.js
```

Test it:

```bash
curl -i http://localhost:3000/
```

## 🎯 Remember

```text
HTTP       → Communication
Methods    → Actions
Status     → Results
Headers    → Metadata
Body       → Data
DNS/TCP/TLS → Networking
REST       → API structure
Node.js    → Build the server
Express    → Simplify the server
```

> 🧠 **Key takeaway:** Learn how HTTP works and build one small server with `node:http` before moving to Express.js.

---
