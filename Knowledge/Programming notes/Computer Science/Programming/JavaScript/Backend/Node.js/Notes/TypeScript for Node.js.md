# 🧠 13 — TypeScript for Node.js

> TypeScript = JavaScript + static types. It helps catch mistakes before your Node.js application runs.

## 1. Basic Types

Define what kind of values a variable can hold.

```ts
let username: string = "Alex";
let age: number = 25;
let isAdmin: boolean = false;

let skills: string[] = ["Node.js", "Express"];
```

## 2. Objects, Unions & Intersections

**Object types** describe the structure of an object.

```ts
type User = {
  id: number;
  name: string;
  email?: string; // Optional
};
```

**Union (****`|`****)** — one type OR another.

```ts
let id: string | number = 101;
id = "user-101";
```

**Intersection (****`&`****)** — combines multiple types.

```ts
type Person = { name: string };
type Employee = { salary: number };

type Worker = Person & Employee;
```

## 3. Interfaces & Type Aliases

Both describe data structures.

```ts
interface User {
  id: number;
  name: string;
}

type Status = "active" | "inactive";
```

- `interface` — commonly used for object contracts.
- `type` — flexible; supports unions, intersections and more.

## 4. Generics

Create reusable code that works with different types.

```ts
function identity<T>(value: T): T {
  return value;
}

identity<string>("Hello");
identity<number>(100);
```

`T` represents a type supplied when calling the function.

## 5. Type Narrowing

Check a type before using its specific methods or properties.

```ts
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(0));
  }
}
```

## 6. `any` vs `unknown`

Both accept different values, but they behave differently.

```ts
let a: any = "Hello";
a.toUpperCase(); // Allowed without checking

let b: unknown = "Hello";
// b.toUpperCase(); // Error

if (typeof b === "string") {
  b.toUpperCase(); // Safe
}
```

- `any` — disables type checking.
- `unknown` — requires checking before use.

💡 Prefer `unknown` for external or uncertain data.

## 7. Utility Types

Built-in tools for transforming existing types.

```ts
type User = {
  id: number;
  name: string;
  email: string;
};

type NewUser = Omit<User, "id">;
type UserPreview = Pick<User, "name">;
type PartialUser = Partial<User>;
type ReadonlyUser = Readonly<User>;
```

|Utility|Purpose|
|---|---|
|`Partial<T>`|Makes properties optional|
|`Required<T>`|Makes properties required|
|`Pick<T, K>`|Selects properties|
|`Omit<T, K>`|Removes properties|
|`Readonly<T>`|Prevents reassignment|

## 8. Type-Safe Error Handling

JavaScript errors can be anything. Use `unknown` and narrow the type.

```ts
try {
  throw new Error("Database failed");
} catch (error: unknown) {
  if (error instanceof Error) {
    console.log(error.message);
  }
}
```

## 9. TypeScript with Express

Give your routes and middleware clear types.

```ts
import express, {
  Request,
  Response,
  NextFunction
} from "express";

const app = express();

app.get(
  "/users/:id",
  (req: Request, res: Response) => {
    const id = req.params.id;

    res.json({ id });
  }
);
```

**Typed request body:**

```ts
type CreateUser = {
  name: string;
  email: string;
};

app.post(
  "/users",
  (req: Request<{}, {}, CreateUser>, res: Response) => {
    const { name, email } = req.body;

    res.json({ name, email });
  }
);
```

💡 Types describe expected data, but do not guarantee that incoming requests contain valid data.

## 10. Runtime Validation vs Compile-Time Types

Two different jobs:

- **Compile-time:** TypeScript checks your code before execution.
- **Runtime:** Validation checks actual data while the application runs.

Example using Zod:

```ts
import { z } from "zod";

const UserSchema = z.object({
  name: z.string(),
  age: z.number().min(18)
});

const result = UserSchema.safeParse(req.body);

if (!result.success) {
  return res.status(400).json({
    errors: result.error.issues
  });
}

const user = result.data;
```

⚠️ Never trust incoming JSON just because your project uses TypeScript.

## 11. TypeScript Configuration

Install TypeScript and Node.js types:

```bash
npm install -D typescript @types/node
npx tsc --init
```

Compile TypeScript:

```bash
npx tsc
```

Example `tsconfig.json` settings:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "strict": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "sourceMap": true
  }
}
```

**Important settings:**

- `strict` — enables stronger type checking.
- `rootDir` — source code directory.
- `outDir` — compiled JavaScript directory.
- `sourceMap` — connects compiled code to original TypeScript when debugging.

## 🧩 The Big Picture

```
TypeScript Code (.ts)
        ↓
Compile-Time Type Checking
        ↓
JavaScript Compilation
        ↓
JavaScript Code (.js)
        ↓
Node.js Runtime
        ↓
Runtime Validation (External Data)
```

**Remember:**

TypeScript protects your code during development. Runtime validation protects your application from invalid external data.

---
