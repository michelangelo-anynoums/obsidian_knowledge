# 🔑 9 — Authentication & Authorization (Express.js)

> Authentication = **Who are you?**
> 
> Authorization = **What are you allowed to do?**

> [!question] Authentication verifies a user's identity. Authorization controls access to resources and actions.

## 1. Password Hashing — bcrypt

Never store plain-text passwords. Hash them before saving to the database.

```bash
npm install bcrypt
```

```js
const bcrypt = require("bcrypt");

// Hash password
const hashedPassword = await bcrypt.hash(password, 12);

// Verify password
const isValid = await bcrypt.compare(
  password,
  hashedPassword
);
```

💡 Hashing is one-way. You compare passwords instead of decrypting them.

## 2. Authentication Middleware

> [!important] Middleware checks whether a user is authenticated before accessing a protected route.

```js
const auth = (req, res, next) => {
  const isAuthenticated = true; // Example only

  if (!isAuthenticated) {
    return res.status(401).json({
      message: "Not authenticated"
    });
  }

  next();
};

app.get("/profile", auth, (req, res) => {
  res.json({ message: "Private profile" });
});
```

- `401` — Not authenticated.
- `next()` — Continue to the next middleware or route.

## 3. Authorization — Roles & Permissions

Authentication identifies the user. Authorization checks their permissions.

Example: Admin-only route.

```js
const authorizeAdmin = (req, res, next) => {
  if (req.user.role !== "admin") {
    return res.status(403).json({
      message: "Access denied"
    });
  }

  next();
};

app.delete("/users/:id", auth, authorizeAdmin, (req, res) => {
  res.json({ message: "User deleted" });
});
```

- `req.user` — Authenticated user's information.
- `403` — Authenticated, but not allowed.

## 4. Sessions & Cookies

A session stores authentication state on the server. A cookie holds the session identifier in the browser.


```bash
npm install express-session
```


```js
const session = require("express-session");

app.use(session({
  secret: process.env.SESSION_SECRET,
  resave: false,
  saveUninitialized: false,
  cookie: {
    httpOnly: true,
    secure: true,
    sameSite: "lax"
  }
}));
```

Example:

```js
// Save user ID in session
req.session.userId = user.id;

// Check session
if (req.session.userId) {
  console.log("Logged in");
}

// Destroy session (logout)
req.session.destroy(() => {
  res.clearCookie("connect.sid");
  res.json({ message: "Logged out" });
});
```

💡 Use a persistent session store in production, not the default MemoryStore.

## 5. JWT — JSON Web Tokens

JWT allows a server to issue a signed token after successful authentication.

```bash
npm install jsonwebtoken
```

**Create a token:**

```js
const jwt = require("jsonwebtoken");

const token = jwt.sign(
  { userId: user.id, role: user.role },
  process.env.JWT_SECRET,
  { expiresIn: "15m" }
);
```

**Verify a token:**

```js
const auth = (req, res, next) => {
  const token = req.headers.authorization?.split(" ")[1];

  if (!token) {
    return res.status(401).json({
      message: "Missing token"
    });
  }

  try {
    req.user = jwt.verify(
      token,
      process.env.JWT_SECRET
    );

    next();
  } catch {
    return res.status(401).json({
      message: "Invalid or expired token"
    });
  }
};
```

Send the token in the request header:

```http
Authorization: Bearer YOUR_TOKEN
```

**JWT structure:**

```
HEADER.PAYLOAD.SIGNATURE
```

- Header → Algorithm and token type.
- Payload → Claims (user ID, role, expiration).
- Signature → Verifies token integrity.

⚠️ JWT payloads are encoded, not encrypted. Never put passwords or secrets inside them.

## 6. Authentication vs Sessions vs JWT

| Concept        | Purpose                            |
| -------------- | ---------------------------------- |
| Authentication | Verify identity                    |
| Authorization  | Check permissions                  |
| bcrypt         | Hash passwords                     |
| Sessions       | Store login state on server        |
| Cookies        | Store data in the browser          |
| JWT            | Carry signed authentication claims |

## 🧩 Typical Authentication Flow


```
USER REGISTERS
      ↓
Hash Password (bcrypt)
      ↓
Save User in Database
      ↓
USER LOGS IN
      ↓
Compare Password
      ↓
Create Session or JWT
      ↓
Send Authentication Credential
      ↓
User Requests Protected Route
      ↓
Verify Identity
      ↓
Check Permissions
      ↓
Allow or Deny Access
```

## 🛡️ Important Security Rules

- Never store plain-text passwords.
- Keep secrets in environment variables.
- Use HTTPS in production.
- Set secure cookie options.
- Validate incoming data.
- Set token expiration and handle revocation where needed.
- Never trust a role or user ID supplied directly by the client.

**Remember: Authentication identifies users. Authorization decides what they can access.**

---
