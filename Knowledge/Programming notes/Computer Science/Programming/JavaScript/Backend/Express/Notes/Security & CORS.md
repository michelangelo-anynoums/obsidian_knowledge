# 🛡️ Security & CORS — Node.js

Security protects your server, API, and users from malicious requests and unauthorized access.

## 1. Helmet

🔒 Sets secure HTTP headers to protect your Express application.

```bash
npm install helmet
```

js

```js
const helmet = require("helmet");

app.use(helmet());
```

## 2. CORS

🌐 Controls which external origins can access your API.

```bash
npm install cors
```

```js
const cors = require("cors");

// Allow a specific frontend
app.use(cors({
  origin: "https://example.com"
}));
```

## 3. Rate Limiting

🚦 Limits the number of requests from a client to prevent abuse.

```bash
npm install express-rate-limit
```

```js
const rateLimit = require("express-rate-limit");

app.use(rateLimit({
  windowMs: 15 * 60 * 1000,
  limit: 100
}));
```

**Result:** Maximum 100 requests per 15 minutes per client (subject to the configured key and proxy setup).

## 4. Input Validation

🧹 Validate user input before processing it.

```js
app.post("/user", (req, res) => {
  const { name } = req.body;

  if (typeof name !== "string" || !name.trim()) {
    return res.status(400).json({
      error: "Invalid name"
    });
  }

  res.json({ name });
});
```

## 5. Password Protection

🔑 Never store passwords as plain text. Use password hashing.

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

## 6. SQL / NoSQL Injection

⚠️ Prevent malicious input from manipulating database queries.

**SQL — Use parameterized queries:**

```js
db.query(
  "SELECT * FROM users WHERE email = ?",
  [email]
);
```

**NoSQL — Validate input and avoid passing raw user objects into queries.**

```js
const user = await User.findOne({
  email: validatedEmail
});
```

## 💡 Remember

- `helmet` → Secure HTTP headers.
- `cors` → Control allowed origins.
- `express-rate-limit` → Limit requests.
- Input validation → Reject invalid data.
- `bcrypt` → Hash passwords.
- Parameterized queries → Prevent SQL injection.

> 🔐 Security is not one package. It is a combination of safe configuration, validation, authentication, and database practices.

---
