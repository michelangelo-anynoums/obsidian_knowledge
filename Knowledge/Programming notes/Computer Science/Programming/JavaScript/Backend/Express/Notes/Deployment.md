# 🚀 13. Deployment

> Make your Node.js server available online 🌍

> [!important] Deployment = moving your application from your local machine to a production server.

## 🌍 1. Production Environment

Development and production are different environments.

- **Development** → Where you build and test.
- **Production** → Where real users access your app.


```js
if (process.env.NODE_ENV === "production") {
  console.log("🚀 Production mode");
} else {
  console.log("🛠️ Development mode");
}
```

Set the environment:

```js
NODE_ENV=production node server.js
```

## 🔐 2. Environment Variables

Store sensitive or configurable values outside your code.

`.env` file:

```env
PORT=3000
DATABASE_URL=mongodb://localhost/mydb
API_KEY=your_secret_key
```

Install dotenv:

```bash
npm install dotenv
```

Use it:

```js
require("dotenv").config();

const port = process.env.PORT || 3000;

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

⚠️ Never upload `.env` to GitHub!

Add it to `.gitignore`:

```gitignore
.env
node_modules/
```

## 📋 3. Logging

Logging helps you understand what happens inside your application.

```js
console.log("✅ Server started");
console.error("❌ Something went wrong");
console.warn("⚠️ Warning");
```

For production, use a logging library such as **Winston** or **Pino**.

```js
const logger = require("pino")();

logger.info("Server started");
logger.error("Database connection failed");
```

## 🚨 4. Error Monitoring

Detect and track errors happening in production.

Example with basic Express error handling:

```js
app.use((err, req, res, next) => {
  console.error(err);

  res.status(500).json({
    message: "Internal Server Error"
  });
});
```

Popular monitoring tools:

- **Sentry** → Error tracking.
- **Datadog** → Application monitoring.

## 🔒 5. HTTPS

HTTPS encrypts communication between the client and server.

- HTTP → Unencrypted connection.
- HTTPS → Encrypted connection (TLS).

Production websites should use HTTPS.

```js
http://myapp.com   ❌
https://myapp.com  ✅
```

Most cloud platforms provide SSL/TLS certificates automatically.

## ☁️ 6. Cloud Hosting

Cloud hosting makes your application accessible through the internet.

Instead of running your server only on your computer, you deploy it to a remote server.

Popular platforms:

|Platform|Description|
|---|---|
|Render|Simple Node.js deployment|
|Railway|Quick deployment and databases|
|Fly.io|Deploy apps close to users|
|AWS|Powerful cloud infrastructure|

## 🚀 7. Basic Deployment Flow


```js
💻 Local Node.js App
        |
        ▼
📦 Push code to GitHub
        |
        ▼
☁️ Connect hosting platform
        |
        ▼
⚙️ Configure environment variables
        |
        ▼
🚀 Build & Start application
        |
        ▼
🌍 App available online!
```

Typical `package.json` scripts:

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

The hosting platform usually runs:

```bash
npm install
npm start
```

---

## 🧠 Key Takeaway

**Deployment = Making your application available to real users.**

Remember:

- 🌍 Production → Live environment.
- 🔐 Environment variables → Configuration and secrets.
- 📋 Logging → Understand application activity.
- 🚨 Monitoring → Detect errors.
- 🔒 HTTPS → Secure communication.
- ☁️ Cloud hosting → Run your app online.

**Localhost → GitHub → Cloud → Internet 🌍**

---
