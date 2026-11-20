# ⚙️ dotenv

> Load environment variables from `.env` files to keep configuration, credentials, and API keys outside your source code.

## 📦 Installation

```bash
npm install dotenv
```

## 🚀 Basic usage

**1. Create a** **.env** **file**

```env
PORT=3000
DB_HOST=localhost
API_KEY=my_secret_key
```

**2. Load dotenv in Node.js**

```js
require('dotenv').config();

const port = process.env.PORT;
const apiKey = process.env.API_KEY;

console.log(port); // 3000
```

**ES Modules:**

```js
import 'dotenv/config';

console.log(process.env.PORT);
```

## 🔐 Important

- `process.env` → Access environment variables.
- `.env` → Store local configuration.
- Never commit `.env` to Git.

Add to `.gitignore`:

```gitignore
.env
```

## 💡 Default values


```js
const port = process.env.PORT || 3000;
```

If `PORT` is not defined, Node.js uses `3000`.

## 🧠 Remember

`dotenv` loads `.env` variables into `process.env`, keeping sensitive configuration out of your code.

🔗 [Official dotenv documentation](https://www.npmjs.com/package/dotenv)

---
