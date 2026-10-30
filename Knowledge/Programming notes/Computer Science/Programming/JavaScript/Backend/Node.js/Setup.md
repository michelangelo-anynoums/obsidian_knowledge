# 🟢 Node.js — Installation & Setup

> Install Node.js, configure your environment, and create your first project.

## 📥 1. Installation

**Official download:** https://nodejs.org/

- Download the **LTS (Long-Term Support)** version.
- Install Node.js (npm is included).
- Restart your terminal.

> [!abstract] 💡 LTS is the recommended choice for most projects.

## 🔍 2. Verify Installation

Check that Node.js and npm are installed correctly.

```bash
node -v
npm -v
```

- `node -v` → Node.js version.
- `npm -v` → npm version.

## 🛠️ 3. Essential Terminal Commands

|Command|Description|
|---|---|
|`node app.js`|Run a JS file|
|`npm init`|Create package.json|
|`npm init -y`|Initialize project quickly|
|`npm install`|Install dependencies|
|`npm install <package>`|Install a package|
|`npm uninstall <package>`|Remove a package|
|`npm update`|Update dependencies|
|`npm run <script>`|Execute a script|
|`npm list`|List installed packages|
|`npm -v`|Check npm version|

## 📁 4. Create Your First Project

Create a folder and enter it:

```bash
mkdir my-project
cd my-project
```

Initialize the project:


```bash
npm init -y
```

Create your entry file:

```bash
touch app.js
```

Add some JavaScript:

```js
console.log("Hello, Node.js! 🚀");
```

Run it:

```bash
node app.js
```

## 📦 5. Install a Package

Example using Express:

```bash
npm install express
```

Import and use it:

```js
const express = require("express");

const app = express();

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

## ⚙️ 6. package.json

The project configuration file.

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "node --watch app.js"
  }
}
```

Run scripts:

```bash
npm start
npm run dev
```

## 📂 7. Project Structure

```js
my-project/
│
├── node_modules/    # Installed packages
├── app.js           # Entry point
├── package.json     # Project configuration
├── package-lock.json
└── .gitignore       # Files Git should ignore
```

**Important:**

- `node_modules/` → Installed dependencies.
- `package.json` → Project metadata and dependencies.
- `package-lock.json` → Locks dependency versions.
- `.gitignore` → Prevents selected files from being tracked by Git.

Example `.gitignore`:

```js
node_modules/
.env
```

## 🔄 8. Node Version Management (Optional)

Use NVM to install and switch between Node.js versions.

**macOS / Linux:** https://github.com/nvm-sh/nvm

```js
nvm install --lts
nvm use --lts
nvm list
node -v
```

**Windows:** https://github.com/coreybutler/nvm-windows

```js
nvm list available
nvm install <version>
nvm use <version>
nvm list
```

## 🧠 Quick Reference

|Tool|Purpose|
|---|---|
|Node.js|JavaScript runtime|
|npm|Package manager|
|npx|Execute package binaries|
|NVM|Manage Node.js versions|
|package.json|Project configuration|
|node_modules|Installed dependencies|
|.gitignore|Ignore files in Git|

---

## 🔗 Useful Resources

- 🌐 Node.js — Official Website
- 📚 Node.js — Documentation
- 📦 npm — Official Website
- 📖 npm — Documentation
- 💻 Visual Studio Code
- 🔄 NVM — GitHub

---