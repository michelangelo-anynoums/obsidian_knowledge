# 🌐 HTTP — Node.js

> [!abstract] 💡 The idea The built-in `node:http` module lets you create HTTP servers, receive requests, and send responses without Express.js.
> 
> 🔄 `Client → Request → Server → Response`

## 🚀 01 · Create a server


```js
const http = require('node:http');

const server = http.createServer((req, res) => {
  res.end('Hello, World! 👋');
});

server.listen(3000, () => {
  console.log('🚀 Server running on port 3000');
});
```

💡 `createServer()` creates the server. `req` represents the request, `res` represents the response, and `listen()` opens the port.

🌍 Visit `http://localhost:3000`.

## 🛣️ 02 · Handle routes

> [!important] Node.js HTTP has no built-in routing system. You check the method and URL yourself.

```js
const server = http.createServer((req, res) => {
  if (req.method === 'GET' && req.url === '/') {
    res.end('🏠 Home');
  } else if (req.method === 'GET' && req.url === '/about') {
    res.end('📖 About');
  } else {
    res.writeHead(404);
    res.end('❌ Not Found');
  }
});
```

💡 `req.method` identifies the HTTP method. `req.url` contains the path and query string.

## 📥 03 · Read request data

### 🔎 Query strings


```js
const url = new URL(req.url, 'http://localhost');
const search = url.searchParams.get('search');

console.log(search);
```

🌍 Request: `/tasks?search=books`

📤 Output: `books`

### 🏷️ Request headers

```js
console.log(req.headers['content-type']);
console.log(req.headers['user-agent']);
```

💡 Headers provide metadata about the request, such as its content type.

### 📦 Request body

The body arrives as a stream of chunks.

```js
const chunks = [];

req.on('data', chunk => chunks.push(chunk));

req.on('end', () => {
  const body = Buffer.concat(chunks).toString();
  console.log(body);
});
```

🧠 For JSON requests, convert the text into a JavaScript object:

```js
try {
  const data = JSON.parse(body);
  console.log(data);
} catch {
  console.log('❌ Invalid JSON');
}
```

⚠️ Parse only after the request's `end` event. Production servers should also limit body size and handle stream errors.

## 📤 04 · Send responses

A response contains a status code, headers, and a body.

```js
res.writeHead(200, {
  'Content-Type': 'text/plain; charset=utf-8'
});

res.end('✅ Success');
```

### 🧾 Send JSON

```js
const data = {
  id: 1,
  title: 'Learn Node.js'
};

res.writeHead(200, {
  'Content-Type': 'application/json'
});

res.end(JSON.stringify(data));
```

💡 `JSON.stringify()` converts a JavaScript value into JSON text.

### 🚦 Common status codes

`200` ✅ OK · `201` 🎉 Created · `204` 🔇 No Content · `400` ⚠️ Bad Request · `401` 🔐 Unauthorized · `403` 🚫 Forbidden · `404` 🔍 Not Found · `500` 💥 Server Error.

## 🔧 05 · HTTP methods

Methods describe the intended action on a resource.

```js
if (req.method === 'GET') {
  // 📖 Read
}

if (req.method === 'POST') {
  // ➕ Create
}

if (req.method === 'PUT') {
  // 🔄 Replace
}

if (req.method === 'PATCH') {
  // ✏️ Update partially
}

if (req.method === 'DELETE') {
  // 🗑️ Remove
}
```

💡 Your code must implement each operation; the method itself does not perform the action.

## 📨 06 · Headers & content types

Tell the client what kind of data you're sending.

```js
// 📝 Plain text
res.writeHead(200, {
  'Content-Type': 'text/plain; charset=utf-8'
});

// 📦 JSON
res.writeHead(200, {
  'Content-Type': 'application/json; charset=utf-8'
});

// 🌐 HTML
res.writeHead(200, {
  'Content-Type': 'text/html; charset=utf-8'
});
```

💡 Headers also control caching, cookies, and other HTTP behavior.

## 🌊 07 · Streams & buffers

Streams let Node.js process data incrementally instead of loading an entire file into memory.

```js
const fs = require('node:fs');

const stream = fs.createReadStream('large-file.txt');

stream.pipe(res);
```

💡 `pipe()` forwards file data to the response.

⚠️ Handle file errors and client disconnects in production. Never assume a file exists.

## 🛡️ 08 · Handle errors

Create a helper for consistent JSON responses.

```js
function sendJson(res, status, data) {
  res.writeHead(status, {
    'Content-Type': 'application/json'
  });

  res.end(JSON.stringify(data));
}

sendJson(res, 404, {
  error: '🔍 Resource not found'
});
```

💡 Always finish a response only once. Handle unexpected errors without exposing sensitive details.

## 🧪 09 · Build a mini API

A simple in-memory task API:

```js
const http = require('node:http');

const tasks = [
  { id: 1, title: 'Learn HTTP' }
];

const server = http.createServer((req, res) => {
  const url = new URL(req.url, 'http://localhost');

  if (req.method === 'GET' && url.pathname === '/tasks') {
    res.writeHead(200, {
      'Content-Type': 'application/json'
    });

    return res.end(JSON.stringify(tasks));
  }

  if (req.method === 'GET' && url.pathname === '/') {
    res.writeHead(200, {
      'Content-Type': 'text/plain'
    });

    return res.end('🚀 Task API');
  }

  res.writeHead(404, {
    'Content-Type': 'application/json'
  });

  res.end(JSON.stringify({
    error: '❌ Not found'
  }));
});

server.listen(3000, () => {
  console.log('🌐 http://localhost:3000');
});
```

### 🧪 Test with curl

```bash
curl http://localhost:3000/
curl http://localhost:3000/tasks
```

💡 This API supports two `GET` routes. Add `POST`, `PATCH`, and `DELETE` to practice creating and modifying tasks.

## ⚖️ 10 · HTTP vs Express

|🌐 Node.js HTTP|⚡ Express.js|
|---|---|
|Built into Node.js|Installed separately|
|Manual routing|Convenient routing|
|Manual body parsing|JSON middleware|
|More low-level control|Less repetitive code|

💡 Express builds on Node.js HTTP capabilities and simplifies common server tasks.

---

> [!tip] 🧠 Mental model **HTTP = Request + Response + Status + Headers + Body**
> 
> 📥 `req` receives information.
> 
> ⚙️ Your code decides what happens.
> 
> 📤 `res` sends the result.
> 
> 🔗 **Reference:** [Node.js HTTP documentation](https://nodejs.org/api/http.html

---
