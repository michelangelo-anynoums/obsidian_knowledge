# 🛡️ Helmet — Secure HTTP Headers

> Protects your Node.js / Express backend by setting HTTP headers that help prevent common web vulnerabilities.

## 📦 Installation

```bash
npm install helmet
```

## ⚙️ Basic usage

```js
const express = require('express');
const helmet = require('helmet');

const app = express();

app.use(helmet());

app.listen(3000);
```

**app.use(helmet())** enables Helmet's collection of security-related HTTP headers.
## 🔍 What does it protect against?

- 🛡️ **XSS** — Helps reduce cross-site scripting risks.
- 🖼️ **Clickjacking** — Controls whether your site can be embedded in frames.
- 🔒 **MIME sniffing** — Prevents browsers from guessing file types.
- 🌐 **HTTPS security** — Configures HTTP Strict Transport Security (HSTS).

## 🎛️ Custom configuration

```js
app.use(
  helmet({
    contentSecurityPolicy: false,
    crossOriginEmbedderPolicy: false,
  })
);
```

Disable individual protections only when your application requires it.
## 💡 Important

- Use Helmet early in your Express middleware stack.
- Keep its default protections enabled whenever possible.
- Helmet improves security but does not replace input validation or authentication.

## 🔗 References

- [Helmet — Official Documentation](https://helmetjs.github.io/)

---
