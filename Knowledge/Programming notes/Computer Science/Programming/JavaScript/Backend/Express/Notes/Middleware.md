# 🔄 Middleware — Express.js

> Middleware functions execute during the HTTP request-response cycle. They can access requests, modify responses, end requests, or pass control to the next middleware.

## 1. 🧠 How Middleware Works

Every middleware receives three main arguments:

- `req` → Incoming request.
- `res` → Response object.
- `next` → Pass control to the next middleware.

```js
Client Request
      ↓
 Middleware 1
      ↓
 Middleware 2
      ↓
 Middleware 3
      ↓
 Controller
      ↓
 Response
```

## 2. 🔹 Built-in Middleware

Express provides middleware for common tasks.

### Parse JSON

Converts incoming JSON request bodies into JavaScript objects.

```js
app.use(express.json());
```

Now you can access:

```js
req.body
```

### Parse Form Data

Handles URL-encoded form submissions.

```js
app.use(express.urlencoded({ extended: true }));
```

Example:

```js
// name=Alex&age=25
console.log(req.body.name); // Alex
```

### Serve Static Files

Makes files publicly accessible.

```js
app.use(express.static("public"));
```

Example structure:

```js
public/
├── images/
├── styles.css
└── index.html
```

Access files through:

```js
http://localhost:3000/styles.css
```

## 3. 🛠️ Custom Middleware

Create middleware to handle application-specific logic.

### Logging Middleware

```js
const logger = (req, res, next) => {
  console.log(req.method, req.url);
  next();
};

app.use(logger);
```

### Authentication Middleware

Check whether a user is authenticated.

```js
function authMiddleware(req, res, next) {
  const token = req.headers.authorization;

  if (!token) {
    return res.status(401).json({
      message: "Unauthorized"
    });
  }

  next();
}
```

Apply it to a route:

```js
app.get("/profile", authMiddleware, (req, res) => {
  res.json({ message: "Private profile" });
});
```

## 4. 📍 Middleware Order Matters!

Express executes middleware in the order it is registered.

```js
app.use(express.json());

app.use(logger);

app.use(authMiddleware);

app.use("/api/tasks", taskRoutes);
```

**Why?** A middleware can modify the request before the next middleware receives it.

For example, `express.json()` must run before routes that need `req.body`.

## 5. ⚠️ Error-Handling Middleware

Special middleware uses four arguments:

`(err, req, res, next)`

```js
app.use((err, req, res, next) => {
  console.error(err);

  res.status(err.status || 500).json({
    message: err.message || "Internal Server Error"
  });
});
```

Pass an error to it using:

```js
next(new Error("Something went wrong"));
```

Place error-handling middleware after your routes.

## 6. 🎯 Route-Level vs Global Middleware

### Global Middleware

Runs for every request (unless its mounting path restricts it).

```js
app.use(logger);
```

### Route-Level Middleware

Runs only on specific routes.

```js
app.get("/admin", authMiddleware, adminController);
```

You can also chain multiple middleware functions:

```js
app.post(
  "/tasks",
  authMiddleware,
  validateTask,
  taskController.create
);
```

## 7. 📚 Important Express Middleware

|Middleware|Purpose|
|---|---|
|`express.json()`|Parse JSON bodies|
|`express.urlencoded()`|Parse form data|
|`express.static()`|Serve static files|
|`cors()`|Configure cross-origin access|
|`helmet()`|Set security-related HTTP headers|
|Custom middleware|Logging, authentication, validation|

## ⭐ Key Takeaway

```js
req   → Read or modify the request
res   → Send the response
next  → Continue to the next middleware
next(err) → Pass an error to error handlers

app.use() → Register global middleware
```

**Remember:**

- Middleware executes in registration order.
- Call `next()` to continue.
- Send a response to finish the request.
- Don't call `next()` after sending a response.
- Always handle errors properly.

**Middleware is the pipeline between receiving a request and sending a response.**

---

# 🧩 Essential Express.js Middlewares

Useful middlewares for almost every Node.js / Express API.

|Middleware|Purpose|
|---|---|
|`express.json()`|Parse incoming JSON requests.|
|`express.urlencoded()`|Parse form data.|
|`cors`|Control cross-origin requests.|
|`helmet`|Secure HTTP headers.|
|`express-rate-limit`|Limit incoming requests.|
|`morgan`|Log HTTP requests.|
|`cookie-parser`|Parse cookies.|
|`compression`|Compress HTTP responses.|

## 📦 Install

```bash
npm install cors helmet express-rate-limit morgan cookie-parser compression
```

## ⚡ Basic Setup


```js
const express = require("express");
const cors = require("cors");
const helmet = require("helmet");
const rateLimit = require("express-rate-limit");
const morgan = require("morgan");
const cookieParser = require("cookie-parser");
const compression = require("compression");

const app = express();

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

app.use(cors());
app.use(helmet());
app.use(rateLimit({
  windowMs: 15 * 60 * 1000,
  limit: 100
}));

app.use(morgan("dev"));
app.use(cookieParser());
app.use(compression());
```

💡 **Remember:** Middleware executes in the order it is registered. Configure CORS origins, rate limits, and proxy settings appropriately for production.

---
