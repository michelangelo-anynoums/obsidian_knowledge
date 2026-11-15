# ⚛️ Environment Variables — `import.meta.env` (Vite + React)

> 💡 Environment variables allow us to store configuration values outside our React code.

## 1. Create an environment file

Create `.env` in your project root:

```
VITE_API_URL=https://api.example.com
VITE_APP_NAME=My React App
```

⚠️ In Vite, variables exposed to the frontend must start with `VITE_`.

## 2. Access variables in React

Use `import.meta.env`

## 3. Different environments

Vite supports different `.env` files:

| File               | Purpose                        |
| ------------------ | ------------------------------ |
| `.env`             | All environments               |
| `.env.development` | Development only               |
| `.env.production`  | Production only                |
| `.env.local`       | Local settings (not committed) |

Example:

```
# .env.development
VITE_API_URL=http://localhost:3000
```


```
# .env.production
VITE_API_URL=https://api.example.com
```

## 4. Built-in environment variables

Vite provides useful variables:

```js
import.meta.env.MODE
// development or production

import.meta.env.DEV
// true in development

import.meta.env.PROD
// true in production

import.meta.env.BASE_URL
// Base URL configured in vite.config.js
```

## 5. Important security rules 🔐

- Never store passwords, private keys or secrets in `VITE_` variables.
- All `VITE_` variables are exposed to browser code.
- Add `.env.local` to `.gitignore`.
- Restart the development server after changing `.env` files.
- Environment variables are replaced during the build process.

## 💡 Example: API request

```jsx
const API_URL = import.meta.env.VITE_API_URL

async function getUsers() {
  const response = await fetch(`${API_URL}/users`)
  return response.json()
}
```

---

✨ **Remember:**

`import.meta.env` → Access environment variables.

`VITE_` → Required prefix for custom client-side variables.

`.env.production` → Production configuration.

🔐 **Never put secrets in frontend environment variables!**

---
