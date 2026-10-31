# 📩 Request & Response — Express.js

> 🔄 `req` (Request) receives data from the client. `res` (Response) sends data back to the client.

## 📥 1. Request (`req`)

Get information sent by the client.

### 🔗 URL Parameters

```js
// GET /users/42
req.params.id;       // "42"
```

### 🔍 Query Parameters

```js
// GET /users?name=John&age=25
req.query.name;      // "John"
req.query.age;       // "25"
```

### 📦 Request Body

```js
// POST /users
req.body;            // Request data
req.body.name;       // Access a property
```

### 🍪 Cookies

```js
req.cookies;         // Parsed cookies
req.signedCookies;   // Signed cookies
```

Requires `cookie-parser` middleware.

### 📋 Request Information

```js
req.method;          // HTTP method
req.url;             // Request URL
req.originalUrl;     // Original URL
req.path;            // URL path
req.hostname;        // Hostname
req.ip;              // Client IP
req.protocol;        // http or https
req.headers;         // Request headers
req.get("User-Agent");// Get a specific header
req.baseUrl;         // Mounted router path
```

### 🔐 Authentication & Other Data


```js
req.secure;          // Is HTTPS?
req.xhr;             // Is AJAX request?
req.subdomains;      // Request subdomains
req.route;           // Matched route information
req.fresh;           // Is response fresh?
req.stale;           // Is response stale?
```

## 📤 2. Response (`res`)

Send information back to the client.

### 📦 Send Data

```js
res.send("Hello!");          // Send text or data
res.json({ name: "John" });  // Send JSON
res.sendStatus(404);         // Send status and message
```

### 🔢 HTTP Status

```js
res.status(200);     // Set status code
res.status(404);     // Not found
res.status(500);     // Server error
```

### 🍪 Cookies

```js
res.cookie("token", "abc123", {
  httpOnly: true,
  secure: true,
  sameSite: "strict",
  maxAge: 3600000
});

// Remove a cookie
res.clearCookie("token");
```

### 📋 Headers

```js
res.set("Content-Type", "application/json");
res.get("Content-Type");       // Read response header
res.append("X-App", "MyApp");
res.removeHeader("X-App");     // Node response method
```

### 🔀 Redirect & Routing


```js
res.redirect("/login");        // Redirect
res.redirect(301, "/home");    // Permanent redirect
res.location("/profile");      // Set Location header
res.links({ next: "/users" }); // Set Link header
```

### 📁 Files & Downloads

```js
res.sendFile("/path/file.pdf");          // Send file
res.download("/path/file.pdf");          // Download file
res.attachment("report.pdf");            // Set download header
```

### ⚙️ Response Control

```js
res.end();             // End response
res.type("json");      // Set content type
res.format({           // Content negotiation
  json: () => res.json({ ok: true }),
  html: () => res.send("<h1>Hello</h1>")
});

res.vary("Accept");    // Add Vary header
res.render("index");   // Render a template
res.locals.user = "John"; // Data for templates
```

## 🚀 3. Complete Example

```js
const express = require("express");
const cookieParser = require("cookie-parser");

const app = express();

app.use(express.json());
app.use(cookieParser());

app.get("/users/:id", (req, res) => {
  const { id } = req.params;
  const { name } = req.query;

  res.status(200).json({
    id,
    name,
    method: req.method
  });
});

app.post("/login", (req, res) => {
  const { username } = req.body;

  res.cookie("user", username, {
    httpOnly: true,
    secure: true,
    sameSite: "strict"
  });

  res.status(200).json({
    message: "Login successful"
  });
});

app.listen(3000);
```

## 📌 Quick Reference

|Object|Method / Property|Purpose|
|---|---|---|
|`req`|`.params`|URL parameters|
|`req`|`.query`|Query strings|
|`req`|`.body`|Request body|
|`req`|`.cookies`|Parsed cookies|
|`req`|`.headers`|Request headers|
|`req`|`.get()`|Read a header|
|`req`|`.method`|HTTP method|
|`req`|`.path`|URL path|
|`req`|`.ip`|Client IP|
|`res`|`.send()`|Send data|
|`res`|`.json()`|Send JSON|
|`res`|`.status()`|Set status|
|`res`|`.cookie()`|Set cookie|
|`res`|`.clearCookie()`|Remove cookie|
|`res`|`.redirect()`|Redirect client|
|`res`|`.sendFile()`|Send file|
|`res`|`.download()`|Download file|
|`res`|`.set()`|Set headers|
|`res`|`.get()`|Read response header|
|`res`|`.end()`|End response|
|`res`|`.render()`|Render template|

## ⚡ Remember

- 📥 `req` = Data coming in.
- 📤 `res` = Data going out.
- 🔗 `req.params` = URL parameters.
- 🔍 `req.query` = Query string.
- 📦 `req.body` = Request payload.
- 🍪 `req.cookies` = Read cookies.
- 🍪 `res.cookie()` = Set cookies.
- 📤 `res.json()` = Return JSON.

💡 **Tip:** A request should receive exactly one final response. Avoid sending multiple responses for the same request.

🔗 **Reference:** https://expressjs.com/en/5x/api.html