# 🟣 BLOCK 13 — TypeScript in React

> [!abstract] The idea **TypeScript = JavaScript + types.**
> 
> TypeScript helps you catch mistakes before your React application runs. You describe the data your components expect, and TypeScript warns you when something doesn't match.

## 1. Types — Describe your data

A type tells TypeScript what kind of value a variable can hold.

```ts
let username: string = "Alex";
let age: number = 25;
let isAdmin: boolean = false;
```

Common types:

|Type|Example|
|---|---|
|`string`|`"Hello"`|
|`number`|`42`|
|`boolean`|`true`|
|`string[]`|`["React", "TypeScript"]`|
|`number \| null`|`25` or `null`|

TypeScript catches incorrect assignments:

```ts
let age: number = 25;

// TypeScript error:
age = "twenty-five";
```

**Remember:** Types describe the values your code should use. They don't automatically validate external data at runtime.

## 2. Interfaces and type aliases

Both `type` and `interface` can describe the shape of an object.

```ts
type User = {
  name: string;
  age: number;
};

interface Product {
  title: string;
  price: number;
}
```

Use them to make your data structure clear.

```ts
const user: User = {
  name: "Alex",
  age: 25,
};
```

If you omit `age` or assign it a string, TypeScript reports an error.

**When should you use each?**

- `type` is flexible and supports unions, primitives, and object shapes.
- `interface` is commonly used for object contracts and can be extended or declaration-merged.

For everyday React development, either is a good choice for object shapes.

## 3. Props types — Give components a contract

Props are the values passed from a parent component to a child component.

Create a file called `UserCard.tsx`:

```ts
type UserProps = {
  name: string;
  age: number;
};

function UserCard({ name, age }: UserProps) {
  return (
    <article>
      <h2>{name}</h2>
      <p>Age: {age}</p>
    </article>
  );
}

export default UserCard;
```

Use the component like this:

```ts
<UserCard name="Alex" age={25} />
```

Incorrect usage:

```ts
<UserCard name="Alex" age="25" />
```

TypeScript flags the second example because `age` must be a number, not a string.

> [!tip] Optional props Add `?` when a prop isn't required.

```ts
type UserProps = {
  name: string;
  age?: number;
};
```

Now `age` can be omitted. Its type is effectively `number | undefined` when read.

## 4. State types — Type your React state

React's `useState` often infers the type from the initial value.

```ts
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

Because the initial value is a number, TypeScript understands that `count` is numeric.

For state that may be empty initially, specify the type:

```ts
type User = {
  name: string;
  age: number;
};

const [user, setUser] = useState<User | null>(null);
```

Why `User | null`? Initially, there may be no user. Later, you can store a `User` object.

```ts
setUser({ name: "Alex", age: 25 });
setUser(null);
```

When displaying the user, check for `null` first:

```ts
return (
  <div>
    {user ? <p>Hello, {user.name}</p> : <p>No user loaded.</p>}
  </div>
);
```

## 5. Function types — Describe what functions accept

You can type the parameters and return value of a function.

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

Here, the function accepts two numbers and returns a number.

You can also describe a function as a type:

```ts
type OnSelect = (id: number) => void;
```

This means the function accepts a number and isn't expected to return a meaningful value.

In React, function types are useful for callback props:

```ts
type ButtonProps = {
  onSave: (message: string) => void;
};

function SaveButton({ onSave }: ButtonProps) {
  return (
    <button onClick={() => onSave("Saved!")}>
      Save
    </button>
  );
}
```

The parent provides the callback:

```ts
<SaveButton onSave={(message) => console.log(message)} />
```

## 6. API response types — Describe external data

Imagine an API returns this JSON:

```ts
{
  "id": 1,
  "name": "Alex",
  "email": "alex@example.com"
}
```

Define the expected structure:

```ts
type User = {
  id: number;
  name: string;
  email: string;
};
```

You can use this type in a fetch function:

```ts
async function getUser(): Promise<User> {
  const response = await fetch("/api/user");

  if (!response.ok) {
    throw new Error("Failed to load user");
  }

  return response.json() as Promise<User>;
}
```

`Promise<User>` describes the value the promise is expected to resolve to.

> [!warning] An important distinction The type assertion in this example does **not** validate the actual JSON. If the API returns unexpected data, TypeScript won't automatically catch it at runtime. For untrusted API responses, validate the data with a runtime schema or explicit checks.

## 7. Generics — Learn later

Generics let you write reusable code that works with different types while preserving type information.

```ts
function firstItem<T>(items: T[]): T | undefined {
  return items[0];
}

const firstName = firstItem(["Alex", "Sam"]);
// string | undefined

const firstNumber = firstItem([10, 20, 30]);
// number | undefined
```

`T` represents a type that TypeScript infers from the input.

You don't need to master generics yet. Start with props, state, and ordinary functions first.

## 8. The `.ts` and `.tsx` distinction

- `.ts` — TypeScript files without JSX.
- `.tsx` — TypeScript files that contain JSX, commonly React components.

For a new React project using Vite:

```ts
npm create vite@latest my-app -- --template react-ts
cd my-app
npm install
npm run dev
```

This creates a React project configured for TypeScript.

## 🧠 Practice — Build a typed profile card

Try creating a component with these requirements:

- A `Profile` type containing `name`, `age`, and `isOnline`.
- A `ProfileCard` component receiving a `profile` prop.
- Display the name, age, and online status.
- Make `isOnline` a boolean.
- Intentionally pass a string to `age` and observe the TypeScript error.

Example starting point:

```ts
type Profile = {
  name: string;
  age: number;
  isOnline: boolean;
};

type ProfileCardProps = {
  profile: Profile;
};

function ProfileCard({ profile }: ProfileCardProps) {
  return (
    <article>
      <h2>{profile.name}</h2>
      <p>Age: {profile.age}</p>
      <p>{profile.isOnline ? "Online" : "Offline"}</p>
    </article>
  );
}
```

> [!success] 🎯 Goal Build React applications with fewer type-related mistakes by typing props, state, functions, and API data.
> 
> **Learning order:** Types → Interfaces → Props → State → Functions → API responses → Generics.

---

