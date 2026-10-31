# 🔐 Node.js — Authentication & Security

> [!abstract] 💡 Core concept Security protects users, data, and backend resources.
> 
> - **Authentication:** Who are you?
> - **Authorization:** What are you allowed to do?

---

## 01 — 🔑 Authentication

Authentication verifies a user's identity.

### Password hashing — Argon2id / bcrypt

Never store passwords as plain text. Store password hashes.

```bash
npm install argon2
```

```js
import argon2 from "argon2";

// Hash password
const hash = await argon2.hash(password);

// Verify password
const valid = await argon2.verify(hash, password);
```

- `hash()` → Creates a secure password hash.
- `verify()` → Checks a password against its hash.
- **Argon2id** → Recommended modern password hashing algorithm.
- **bcrypt** → Another widely used password hashing algorithm.

### Registration & login

```js
// Register
const user = await User.create({
  email,
  password: await argon2.hash(password)
});

// Login
const valid = await argon2.verify(
  user.password,
  password
);

if (!valid) {
  return res.status(401).json({ error: "Invalid credentials" });
}
```

- Registration creates an account.
- Login verifies credentials.
- Logout terminates the authenticated session.
- Account recovery uses secure, short-lived reset tokens.

### 🍪 Cookie-based sessions

A session stores authentication state on the server.

```js
import session from "express-session";

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

- `httpOnly` → JavaScript cannot read the cookie.
- `secure` → Cookie is sent over HTTPS only.
- `sameSite` → Controls cross-site cookie sending.
- Use a persistent server-side session store in production, not the default MemoryStore.

### 🎟️ JWT (JSON Web Token)

A token used to transmit signed claims.

**Structure:**

```js
HEADER.PAYLOAD.SIGNATURE
```

- Header → Algorithm and token type.
- Payload → Claims, such as user ID and expiration.
- Signature → Protects token integrity.

```js
import jwt from "jsonwebtoken";

const token = jwt.sign(
  { sub: user.id },
  process.env.JWT_SECRET,
  { expiresIn: "15m" }
);

const decoded = jwt.verify(
  token,
  process.env.JWT_SECRET
);
```

⚠️ A JWT is signed, not automatically encrypted. Never put passwords or sensitive personal data in its payload.

**Important concepts:**

- Signing → Creates a cryptographic signature.
- Verification → Checks signature and validity.
- Expiration → Limits token lifetime.
- Key management → Protects and rotates signing keys.

### ♻️ Refresh tokens

Used to obtain new access tokens without requiring another login.

- Rotation → Issue a new refresh token after use.
- Revocation → Invalidate a token or token family.
- Storage → Keep refresh tokens securely.
- Reuse detection → Detect previously consumed tokens.

### 🌐 OAuth 2.0 & OpenID Connect

|Technology|Purpose|
|---|---|
|OAuth 2.0|Delegated authorization.|
|OpenID Connect (OIDC)|Authentication built on OAuth 2.0.|

- OAuth → Allows an application to access resources.
- OIDC → Provides identity information.
- MFA → Adds another authentication factor.
- Email verification → Confirms ownership of an email address.

---

## 02 — 🛡️ Authorization

Controls access after authentication.

### RBAC — Role-Based Access Control

Assign permissions based on user roles.

```js
const roles = {
  admin: ["read", "write", "delete"],
  user: ["read", "write"]
};
```

Example:

```js
function authorize(...allowedRoles) {
  return (req, res, next) => {
    if (!allowedRoles.includes(req.user.role)) {
      return res.sendStatus(403);
    }

    next();
  };
}

app.delete(
  "/users/:id",
  authorize("admin"),
  deleteUser
);
```

### Resource ownership

Users should only access their own private resources.

```js
const task = await Task.findOne({
  where: {
    id: req.params.id,
    userId: req.user.id
  }
});

if (!task) {
  return res.sendStatus(404);
}
```

- `userId` → Identifies the resource owner.
- `req.user.id` → Authenticated user's ID.
- `404` → Resource not found.

⚠️ Never trust an ID supplied by the client without checking permissions.

### IDOR — Insecure Direct Object Reference

A vulnerability where users access another user's resources by changing an ID.

```js
// ❌ Unsafe
const task = await Task.findByPk(req.params.id);

// ✅ Ownership checked
const task = await Task.findOne({
  where: {
    id: req.params.id,
    userId: req.user.id
  }
});
```

---

## 03 — 🚨 Express.js Security Essentials

### SQL / NoSQL Injection

Never build database queries from untrusted input.

```js
// ❌ Unsafe SQL
const query = `SELECT * FROM users WHERE email = '${email}'`;

// ✅ Parameterized SQL
const result = await db.query(
  "SELECT * FROM users WHERE email = $1",
  [email]
);
```

Use parameterized queries, safe ORM methods, and input validation.

### XSS — Cross-Site Scripting

Malicious scripts injected into pages.


```
// Validate input
// Escape output
// Avoid inserting untrusted HTML
```

### CSRF — Cross-Site Request Forgery

Tricks an authenticated browser into making unwanted requests.

```js
// Use CSRF protection where cookie-based
// authentication is vulnerable to cross-site requests.
```

### CORS — Cross-Origin Resource Sharing

Controls which browser origins can access your API.


```js
import cors from "cors";

app.use(cors({
  origin: "https://example.com",
  credentials: true
}));
```

⚠️ CORS is not authentication or authorization.

### Helmet — Security headers

```js
npm install helmet
```

```js
import helmet from "helmet";

app.use(helmet());
```

Adds HTTP security headers to help protect your application.

### Rate limiting

Restricts repeated requests, especially login attempts.

```js
npm install express-rate-limit
```

```js
import rateLimit from "express-rate-limit";

const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  limit: 5
});

app.use("/login", loginLimiter);
```

### 🔐 Secure cookies

```js
res.cookie("session", token, {
  httpOnly: true,
  secure: true,
  sameSite: "lax"
});
```

|Attribute|Purpose|
|---|---|
|`HttpOnly`|Prevents JavaScript access.|
|`Secure`|Requires HTTPS.|
|`SameSite`|Controls cross-site sending.|

### 📁 File upload security

```js
const upload = multer({
  limits: {
    fileSize: 2 * 1024 * 1024
  },
  fileFilter: (req, file, cb) => {
    const allowed = ["image/jpeg", "image/png"];

    cb(null, allowed.includes(file.mimetype));
  }
});
```

Validate:

- File size.
- File type and actual content.
- File names.
- Storage location.

⚠️ MIME type alone is not sufficient to establish that a file is safe.

---

## 04 — ⚙️ Environment & Application Security

### Environment variables

Keep secrets outside source code.

```bash
npm install dotenv
```

```env
SESSION_SECRET=your-secret
JWT_SECRET=your-secret
DATABASE_URL=your-database-url
```


```js
import "dotenv/config";

const secret = process.env.JWT_SECRET;
```

Never commit `.env` files to Git.

### Error handling

Avoid exposing internal information.

```js
app.use((err, req, res, next) => {
  console.error(err);

  res.status(500).json({
    error: "Internal server error"
  });
});
```

Never expose:

- Stack traces.
- Passwords or tokens.
- Database credentials.
- Personal information.

### Dependency security

```bash
npm audit
npm audit fix
npm outdated
```

- Keep packages updated.
- Review security advisories.
- Remove unnecessary dependencies.
- Audit regularly.

---

## 05 — 🧠 Security Summary

|Concept|Remember|
|---|---|
|Argon2id / bcrypt|Password hashing.|
|Sessions|Server-side authentication state.|
|JWT|Signed token-based authentication.|
|Refresh tokens|Renew access tokens.|
|OAuth 2.0|Delegated authorization.|
|OIDC|User authentication.|
|RBAC|Permissions based on roles.|
|IDOR|Missing resource ownership checks.|
|XSS|Malicious browser scripts.|
|CSRF|Forged authenticated requests.|
|CORS|Cross-origin browser access.|
|Helmet|HTTP security headers.|
|Rate limiting|Restricts excessive requests.|
|HTTPS|Encrypts data in transit.|

> [!success] 🎯 Golden rule Never trust client input. Authenticate users, authorize every protected resource, validate data, and protect secrets.

---
