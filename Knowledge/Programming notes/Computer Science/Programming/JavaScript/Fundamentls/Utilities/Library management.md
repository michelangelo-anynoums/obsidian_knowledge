# 📚 JavaScript — Library Management

> [!abstract] Overview **Library management** in JavaScript is the process of installing, importing, updating, and organizing external libraries that provide functionality for your application. Instead of building everything from scratch, we can reuse existing code written by other developers.

## 1. 📦 What Is a Library?

A **library** is reusable code that helps you perform specific tasks.

Common examples:

- **React** — building user interfaces.
- **Axios** — making HTTP requests.
- **Zustand** — managing shared state.
- **date-fns** — working with dates.

```js
import axios from "axios";

const response = await axios.get(
  "https://jsonplaceholder.typicode.com/users"
);

console.log(response.data);
```

Instead of writing all the HTTP request logic ourselves, we use Axios.

## 2. 🧰 What Is npm?

**npm (Node Package Manager)** is a tool used to install and manage JavaScript packages.

It allows us to download libraries, track dependencies, and run project scripts.

Common commands:

```bash
npm init -y          # Create package.json
npm install axios    # Install a dependency
npm uninstall axios  # Remove a dependency
npm update           # Update dependencies within allowed ranges
```

In modern JavaScript projects, npm is commonly used alongside Node.js and a build tool such as Vite.

## 3. 📄 Understanding `package.json`

The `package.json` file describes your project and its dependencies.

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build"
  },
  "dependencies": {
    "react": "^19.0.0",
    "axios": "^1.7.0"
  }
}
```

The versions above are illustrative, not recommendations for the latest releases.

Important fields:

- `name` — the project name.
- `version` — the project's version.
- `scripts` — commands you can run with npm.
- `dependencies` — packages needed by the application.
- `devDependencies` — packages mainly needed during development, such as build tools and testing tools.

Run a script with:

```bash
npm run dev
npm run build
```

## 4. 📥 Installing Libraries

To add a library to your project, use `npm install`.

```bash
npm install zustand
```

npm downloads the package and records it in `package.json`, normally under `dependencies`.

For development-only tools:

```bash
npm install -D eslint
```

The `-D` flag adds the package to `devDependencies`.

## 5. 📤 Importing and Using Libraries

Once installed, a package can be imported into your JavaScript files.

```bash
import { create } from "zustand";
```

There are two common import styles.

**Named import**

```js
import { useState } from "react";
```

Imports a specific exported member.

**Default import**

```js
import axios from "axios";
```

Imports the package's default export.

The correct syntax depends on how the library exports its functionality.

## 6. 🔒 What Is `package-lock.json`?

The `package-lock.json` file records the resolved dependency versions and related installation information.

It helps developers install consistent dependency trees across different machines.

For example, when cloning an existing project:

```bash
npm install
```

npm reads `package.json` and uses the lockfile when available to resolve the project's dependencies consistently.

> [!important] Remember Commit both `package.json` and `package-lock.json` to version control in a typical npm application. Do not manually edit the lockfile.

## 7. 🔄 Updating and Managing Versions

Dependencies use version numbers such as:

```text
1.4.2
```

This usually represents:

- `1` — major version.
- `4` — minor version.
- `2` — patch version.

In semantic versioning, major releases may introduce breaking changes, minor releases add backward-compatible features, and patch releases contain backward-compatible fixes.

Useful commands:

```bash
npm list             # Show installed packages
npm outdated         # Check for outdated packages
npm update           # Update within allowed version ranges
npm install axios@latest
```

Installing `@latest` requests the latest published version, which may introduce breaking changes. Check the library's documentation before updating important dependencies.

## 8. ⚛️ How This Connects to React

A React application often depends on multiple libraries.

For example:

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm install zustand
npm run dev
```

Here:

- Vite creates the project structure.
- npm installs the project's dependencies.
- React renders the user interface.
- Zustand can manage shared application state.
- `package.json` describes the dependencies and scripts.

Each library should have a clear purpose. Installing more packages does not automatically make an application better.

## 📌 Quick Reference

|Command|Purpose|
|---|---|
|`npm init -y`|Initialize a project|
|`npm install package`|Install a dependency|
|`npm install -D package`|Install a development dependency|
|`npm uninstall package`|Remove a dependency|
|`npm update`|Update eligible dependencies|
|`npm outdated`|Check for outdated packages|
|`npm list`|List installed packages|
|`npm run dev`|Run the configured development script|

---
