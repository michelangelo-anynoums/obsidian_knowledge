
# 🟠 BLOCK 9 — Custom Hooks

> [!abstract] Overview **Custom Hooks** let you extract and reuse stateful logic between React components without duplicating code.

## 1. 🧠 What Is a Custom Hook?

A custom hook is a JavaScript function that uses React Hooks or other custom hooks to share reusable logic.

**Rules:**

- Its name must start with `use`.
- It can use hooks such as `useState`, `useEffect`, and `useRef`.
- It returns whatever values or functions the component needs.
- It shares logic, not the component's state itself.

### Example

```jsx
import { useState } from "react";

function useCounter() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount((prev) => prev + 1);
  }

  return { count, increment };
}
```

Use it in a component:

```jsx
function Counter() {
  const { count, increment } = useCounter();

  return (
    <button onClick={increment}>
      Count: {count}
    </button>
  );
}
```

> [!tip] Key idea Each component calling `useCounter()` gets its **own independent state**, while both components can reuse the same logic.

---

## 2. 📏 Rules of Hooks

React Hooks must follow specific rules to keep their state and behavior consistent.

### Rule 1 — Only Call Hooks at the Top Level

Do not call hooks inside conditions, loops, or nested functions.

❌ Incorrect:

```jsx
if (isLoggedIn) {
  const [user, setUser] = useState(null);
}
```

✅ Correct:

```jsx
const [user, setUser] = useState(null);

if (isLoggedIn) {
  // Use user here
}
```

### Rule 2 — Only Call Hooks from React Functions

Call hooks from:

- React function components.
- Custom hooks.

❌ Incorrect:

```jsx
function fetchUser() {
  const [user, setUser] = useState(null);
}
```

✅ Correct:

```jsx
function useUser() {
  const [user, setUser] = useState(null);
  return user;
}
```

### Rule 3 — Keep Hook Calls Consistent

Call hooks in the same order on every render. Avoid placing hook calls after conditional returns.

```jsx
function Profile({ userId }) {
  const [name, setName] = useState("");

  if (!userId) {
    return <p>No user selected.</p>;
  }

  return <p>{name}</p>;
}
```

> [!warning] Common mistake Calling a hook conditionally can cause React to associate state with the wrong hook call or throw an error.

---

## 3. ♻️ Extracting Reusable Logic

Custom hooks are useful when multiple components need the same behavior.

### Before — Duplicated Logic

```jsx
function UserProfile() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch("/api/user")
      .then((res) => res.json())
      .then(setUser);
  }, []);

  // Render user
}
```

Another component might repeat the same fetching logic.

### After — Reusable Custom Hook

Create a separate file: `useFetch.js`

```jsx
import { useEffect, useState } from "react";

export function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();

    async function fetchData() {
      setLoading(true);
      setError(null);

      try {
        const response = await fetch(url, {
          signal: controller.signal,
        });

        if (!response.ok) {
          throw new Error(`HTTP error: ${response.status}`);
        }

        const result = await response.json();
        setData(result);
      } catch (err) {
        if (err.name !== "AbortError") {
          setError(err);
        }
      } finally {
        if (!controller.signal.aborted) {
          setLoading(false);
        }
      }
    }

    fetchData();

    return () => controller.abort();
  }, [url]);

  return { data, loading, error };
}
```

### Use the Hook

```jsx
import { useFetch } from "./useFetch";

function Users() {
  const { data, loading, error } =
    useFetch("/api/users");

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data?.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

> [!info] Why use `AbortController`? It cancels an outdated or in-flight request when the URL changes or the component stops using the effect, helping prevent unnecessary work.

---

## 4. 🗂️ Common Custom Hook Patterns

|Hook|Purpose|
|---|---|
|`useFetch()`|Fetch and manage remote data|
|`useLocalStorage()`|Synchronize state with local storage|
|`useDebounce()`|Delay updates until activity pauses|
|`useToggle()`|Manage boolean state|
|`useWindowSize()`|Track viewport dimensions|
|`usePrevious()`|Remember a previous value|
|`useOnlineStatus()`|Track network connectivity|

These are common community patterns, not all built-in React hooks.

---

## 5. 🧩 Custom Hooks vs Components

|Custom Hook|React Component|
|---|---|
|Reuses behavior and logic|Renders UI|
|Named with a `use` prefix|Usually named with a capital letter|
|Called like a function|Rendered with JSX|
|Returns data, state, or functions|Returns JSX or another React node|
|Has no independent UI of its own|Defines a UI structure|

Example:

```jsx
const { count, increment } = useCounter();
```

Compared with:

```jsx
<Counter />
```

---

## 6. ⚠️ Common Mistakes

- Naming a custom hook without the `use` prefix.
- Calling hooks inside loops or conditions.
- Forgetting dependencies in `useEffect`.
- Duplicating logic that could be shared.
- Assuming two components calling the same hook share state automatically.
- Putting every small function into a custom hook unnecessarily.
- Ignoring request cancellation or error handling when fetching data.

---

