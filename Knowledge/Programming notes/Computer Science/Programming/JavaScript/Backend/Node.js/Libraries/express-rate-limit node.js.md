# 📡 express-rate-limit

> Protect your Node.js API from excessive requests, brute-force attacks and abuse.

## ⚙️ Installation

```bash
npm install express-rate-limit
```

## 🚀 Basic usage

```js
const express = require('express');
const rateLimit = require('express-rate-limit');

const app = express();

const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    limit: 100,               // Max 100 requests
    message: 'Too many requests. Try again later.'
});

app.use(limiter);

app.listen(3000);
```

## 🔍 Key options

|Option|Description|
|---|---|
|`windowMs`|Time window in milliseconds|
|`limit`|Maximum requests allowed|
|`message`|Response when limit is exceeded|
|`standardHeaders`|Enables standard rate-limit headers|
|`skip`|Excludes specific requests|

## 🎯 Protect specific routes

Apply rate limiting only where needed (e.g. login):

```js
const loginLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    limit: 5,
    message: 'Too many login attempts.'
});

app.post('/login', loginLimiter, loginHandler);
```

## 💡 Remember

- 🌍 `app.use(limiter)` → Protects all routes.
- 🎯 Route middleware → Protects specific endpoints.
- 🔐 Login limits → Helps prevent brute-force attacks.
- ⚡ Rate limiting → Controls how frequently clients can make requests.

🔗 [Official documentation](https://express-rate-limit.mintlify.app/)

---
