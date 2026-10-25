# 📦 JavaScript — Modules (`import` & `export`)

Modules let us **split code into separate files** and reuse functions, variables, and classes across our projects.

## 1. Exporting

Use `export` to make something available to other files.

### Named exports

**math.js**

```js
export const PI = 3.14159;

export function add(a, b) {
  return a + b;
}
```

You can export multiple values from the same file.

## 2. Importing

Use `import` to access exported values from another module.

**app.js**

```js
import { PI, add } from "./math.js";

console.log(PI);
console.log(add(2, 3));
```

- Use `{ }` for named imports.
- Use the file path to identify the module.
- `./` means the file is in the current directory.

## 3. Default export

A module can have **one default export**.

**greet.js**

```js
export default function greet(name) {
  return `Hello, ${name}!`;
}
```

Import it without curly braces:

**app.js**

```js
import greet from "./greet.js";

console.log(greet("Alex"));
```

You can choose the name of a default import.

## 4. Rename imports and exports

Use `as` to give an imported or exported value another name.

```js
// Export
function multiply(a, b) {
  return a * b;
}

export { multiply as times };
```

```js
// Import
import { times as product } from "./math.js";

console.log(product(3, 4)); // 12
```

## 5. Import everything

Use `* as` to group all named exports under one object.

```js
import * as math from "./math.js";

console.log(math.add(2, 3));
console.log(math.PI);
```

## 🧠 Quick Reference

|Syntax|Purpose|
|---|---|
|`export const x = 1`|Export a named value|
|`export default value`|Export the main value|
|`import { x } from "./file.js"`|Import a named value|
|`import value from "./file.js"`|Import the default value|
|`import { x as y } from "./file.js"`|Rename an import|
|`import * as obj from "./file.js"`|Import all named exports|

## ⚙️ Important Notes

- Use `export` and `import` with **ES modules (ESM)**.
- Named imports must match the exported name unless renamed with `as`.
- A module can have multiple named exports but only one default export.
- In a browser, use `<script type="module" src="app.js"></script>`.
- In Node.js, configure your project to use ES modules, for example by setting `"type": "module"` in `package.json`.

**Remember:** `export` makes something available; `import` brings it into another module.

---
