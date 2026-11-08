# 📂 Express.js Routers

> 🎯 **Goal:** Organize API endpoints into separate files to keep your application clean, modular, and easy to maintain.

## 🧠 1. What is a Router?

> [!abstract] A Router is a mini Express application that handles routes for a specific resource or feature.
Instead of putting every endpoint inside `app.js`, separate them into individual files.

```
📁 project/
 ├── 📁 routes/
 │    ├── users.js
 │    ├── products.js
 │    └── orders.js
 │
 ├── app.js
 └── server.js
```

## 🔧 2. Create a Router

**📄 routes/users.js**

```js
const router = require("express").Router();

// GET /users
router.get("/", (req, res) => {
  res.json({ users: [] });
});

// GET /users/:id
router.get("/:id", (req, res) => {
  res.json({ userId: req.params.id });
});

// POST /users
router.post("/", (req, res) => {
  res.status(201).json({ message: "User created" });
});

module.exports = router;
```

- `express.Router()` → Creates a router.
- `router.get()` → Defines a GET endpoint.
- `router.post()` → Defines a POST endpoint.
- `module.exports` → Exports the router.

## 🔗 3. Connect Router to Express

**📄 app.js**


```js
const express = require("express");
const app = express();

const usersRouter = require("./routes/users");

app.use(express.json());

// Mount router
app.use("/users", usersRouter);

module.exports = app;
```

## 🌐 4. Understand Route Paths

When you mount a router, Express combines its base path with the router's endpoint.


```js
app.use("/users", usersRouter);
```

Inside `users.js`:


```js
router.get("/", ...);
router.get("/:id", ...);
router.post("/", ...);
```

Final endpoints:

|Method|Endpoint|Purpose|
|---|---|---|
|GET|`/users`|Get all users|
|GET|`/users/:id`|Get one user|
|POST|`/users`|Create user|

## 🛡️ 5. Router Middleware

You can apply middleware to an entire router.

```js
const auth = require("../middleware/auth");

// Protect all user routes
router.use(auth);

router.get("/", (req, res) => {
  res.json({ users: [] });
});
```

Now every route handled by this router passes through `auth`.

## 🧠 Key Takeaways

- 📂 **Router:** Groups related endpoints.
- 🔗 **app.use():** Mounts a router at a base URL.
- 🧩 **Middleware:** Adds authentication, validation, etc.
- 📦 **module.exports:** Makes the router reusable.

**Remember:** `app.js` connects everything. Routers organize the endpoints.

---
