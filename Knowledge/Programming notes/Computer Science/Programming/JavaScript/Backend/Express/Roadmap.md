# 🚀 Express.js — Server-Side Roadmap

> Build server-side applications and REST APIs with Node.js and Express.

## 1. 📦 Setup & Installation

Install Express:

```bash
npm init -y
npm install express
npm install -D nodemon
```

Basic server:

```js
const express = require("express");
const app = express();

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

## 2. 🛣️ Routing

Define endpoints and handle HTTP requests.

```js
app.get("/", (req, res) => {
  res.send("Home");
});

app.post("/users", (req, res) => {
  res.send("Create user");
});

app.put("/users/:id", (req, res) => {
  res.send("Update user");
});

app.delete("/users/:id", (req, res) => {
  res.send("Delete user");
});
```

## 3. 📩 Request & Response [[Request & Response]]

Receive data and send responses.

```js
req.params   // URL parameters
req.query    // Query string
req.body     // Request body

res.send()   // Send response
res.json()   // Send JSON
res.status() // Set HTTP status
```

Example:

```js
app.get("/users/:id", (req, res) => {
  res.status(200).json({
    id: req.params.id
  });
});
```

## 4. 🔄 Middleware

Functions executed during the request-response cycle.

```js
// Parse JSON
app.use(express.json());

// Custom middleware
app.use((req, res, next) => {
  console.log(req.method, req.url);
  next();
});
```

Important middleware:

- `express.json()` — Parse JSON.
- `express.urlencoded()` — Parse form data.
- `express.static()` — Serve static files.
- Custom middleware — Authentication, logging, etc.

## 5. 📂 Routers

Organize endpoints into separate files.

**routes/users.js**

```js
const router = require("express").Router();

router.get("/", (req, res) => {
  res.json({ users: [] });
});

module.exports = router;
```

**app.js**

```js
const usersRouter = require("./routes/users");

app.use("/users", usersRouter);
```

## 6. ⚠️ Error Handling

Handle errors centrally.

```js
app.get("/error", (req, res, next) => {
  next(new Error("Something went wrong"));
});

// Error-handling middleware
app.use((err, req, res, next) => {
  console.error(err.message);

  res.status(500).json({
    error: "Internal Server Error"
  });
});
```

## 7. 🔐 Environment Variables

Keep configuration and secrets outside your code.

```bash
npm install dotenv
```

**.env**

```env
PORT=3000
DATABASE_URL=mongodb://localhost/mydb
```

**app.js**

```js
require("dotenv").config();

const port = process.env.PORT || 3000;
```

Never commit `.env` to Git.

## 8. 🗄️ Database Integration

Connect Express to a database.

Main concepts:

- MongoDB + Mongoose
- PostgreSQL + Prisma
- MySQL
- CRUD operations

Example CRUD operations:

```js
// Create
// Read
// Update
// Delete
```

## 9. 🔑 Authentication & Authorization

Protect routes and manage users.

Essential concepts:

- Password hashing (`bcrypt`)
- Authentication
- Authorization / roles
- Sessions and cookies
- JWT (JSON Web Tokens)

Example:

```js
const auth = (req, res, next) => {
  // Verify user credentials
  next();
};

app.get("/profile", auth, (req, res) => {
  res.json({ message: "Private profile" });
});
```

## 10. 🌐 REST API & HTTP

Understand the main HTTP methods and status codes.

|Method|Purpose|
|---|---|
|GET|Retrieve data|
|POST|Create data|
|PUT|Replace data|
|PATCH|Update data|
|DELETE|Remove data|

Common status codes:

|Code|Meaning|
|---|---|
|200|OK|
|201|Created|
|204|No Content|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|500|Server Error|

## 11. 🛡️ Security & CORS

Protect your server and API.

```bash
npm install helmet cors express-rate-limit
```

```js
const helmet = require("helmet");
const cors = require("cors");

app.use(helmet());
app.use(cors());
```

Essential concepts:

- CORS policies
- Rate limiting
- Input validation
- Secure HTTP headers
- Password protection
- SQL/NoSQL injection prevention

## 12. 🧪 Testing & Development

Test endpoints and debug your application.

Useful tools:

- Postman / Insomnia — API testing.
- Jest / Vitest — Automated tests.
- Supertest — HTTP endpoint testing.
- Nodemon — Automatic server restart.

```bash
npm run dev
```

## 13. 🚀 Deployment

Make your server available online.

Essential concepts:

- Production environment
- Environment variables
- Logging
- Error monitoring
- HTTPS
- Cloud hosting

Useful platforms:

- Render
- Railway
- Fly.io
- AWS

---

## 🧠 Express.js — Quick Reference

|Concept|Purpose|
|---|---|
|`express()`|Create application|
|`app.listen()`|Start server|
|`app.use()`|Register middleware|
|`app.get()`|Handle GET|
|`app.post()`|Handle POST|
|`req.params`|URL parameters|
|`req.query`|Query parameters|
|`req.body`|Request data|
|`res.json()`|Send JSON|
|`res.status()`|Set status code|
|`express.Router()`|Modular routes|
|`next()`|Pass control onward|

---
