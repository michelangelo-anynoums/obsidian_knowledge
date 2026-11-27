# 🌐 CORS — Cross-Origin Resource Sharing

> [!abstract] 💡 What is CORS? CORS controls which external origins (websites) are allowed to access your backend from a browser.

## ⚙️ 1. Install


```bash
npm install cors
```

## 🚀 2. Basic usage (Express)

```js
const express = require("express");
const cors = require("cors");

const app = express();

app.use(cors());

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

🌍 `app.use(cors())` allows requests from any origin.

## 🔒 3. Allow a specific origin

```js
app.use(cors({
  origin: "http://localhost:5173"
}));
```

✅ Only the specified origin is allowed to access the backend through browser CORS requests.

## 🎯 4. Allow multiple origins


```js
const allowedOrigins = [
  "http://localhost:5173",
  "https://mywebsite.com"
];

app.use(cors({
  origin: allowedOrigins
}));
```

## 🍪 5. Allow credentials (cookies)

```js
app.use(cors({
  origin: "http://localhost:5173",
  credentials: true
}));
```

Frontend:

```js
fetch("http://localhost:3000/api", {
  credentials: "include"
});
```

⚠️ When using credentials, `origin: "*"` is not allowed.

## 🧠 Remember

- 🌐 **Origin** = protocol + domain + port.
- 🔒 CORS controls browser access to cross-origin responses.
- 🍪 `credentials: true` allows credentials such as cookies.
- ⚠️ CORS is NOT authentication or backend security. Non-browser clients are not restricted by browser CORS rules.

## 🔗 Reference

- [Express CORS middleware](https://expressjs.com/en/resources/middleware/cors.html)
- [MDN — CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS)

---
