# 🟡 Block 7 — React: API, Async Data & Data Handling

## 1. What Is an API?

An **API** allows a React application to communicate with a server to get, send, update, or delete data.

Example: A React app requests a list of users from a server and displays them on the screen.

## 2. HTTP Methods

- **GET** — Retrieve data.
- **POST** — Create new data.
- **PUT** — Replace or update existing data.
- **DELETE** — Delete data.

## 3. Handling Data in React

React uses **state** to store data that can change and needs to update the UI.

### `useState()`

Use `useState()` to store and update data in a component.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}

export default Counter;
```

- `count` — The current value.
- `setCount` — Updates the value.
- `useState(0)` — Sets the initial value to `0`.

When state changes, React re-renders the component.

### Handling Arrays

Use `.map()` to display a list of data.

```jsx
const users = ["Alex", "Maria", "John"];

function UserList() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user}>{user}</li>
      ))}
    </ul>
  );
}
```

### Handling Objects

Use objects to store related information.

```jsx
const user = {
  name: "Alex",
  age: 25,
  email: "alex@example.com",
};

<p>{user.name}</p>
<p>{user.email}</p>
```

### Updating State

Never modify state objects or arrays directly. Create a new object or array instead.

```jsx
const [user, setUser] = useState({
  name: "Alex",
  age: 25,
});

setUser((previousUser) => ({
  ...previousUser,
  age: 26,
}));
```

The spread operator (`...`) keeps the existing properties while updating `age`.

## 4. Fetching Data with `fetch()`

The `fetch()` function sends an HTTP request to an API.

```jsx
fetch("https://jsonplaceholder.typicode.com/users")
  .then((response) => {
    if (!response.ok) {
      throw new Error("Failed to fetch users");
    }

    return response.json();
  })
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

- `fetch()` — Sends the request.
- `response.ok` — Checks whether the HTTP response indicates success.
- `response.json()` — Reads the response body as JSON.
- `catch()` — Handles errors.

## 5. Async/Await

`async/await` makes asynchronous code easier to read.

- `async` allows a function to use `await`.
- `await` waits for a Promise to settle before continuing.
- `try/catch` handles errors.

Example:

```jsx
async function getUsers() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/users"
    );

    if (!response.ok) {
      throw new Error("Failed to fetch users");
    }

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

## 6. Displaying API Data in React

Use `useState()` to store API data and `useEffect()` to fetch it when the component loads.

```jsx
import { useState, useEffect } from "react";

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function getUsers() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );

        if (!response.ok) {
          throw new Error("Failed to fetch users");
        }

        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    getUsers();
  }, []);

  if (loading) return <p>Loading...</p>;

  if (error) return <p>Error: {error}</p>;

  if (users.length === 0) {
    return <p>No users found.</p>;
  }

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.name} - {user.email}
        </li>
      ))}
    </ul>
  );
}

export default Users;
```

### Important Concepts

- `useState()` stores the users, loading status, and error message.
- `useEffect()` runs the data-fetching logic after the component renders.
- `[]` means the effect runs on mount, subject to React Strict Mode's development behavior.
- `setUsers(data)` saves the API response in React state.
- `.map()` displays each user.
- `key={user.id}` helps React identify list items.
- `finally` runs whether the request succeeds or fails.

## 7. Loading, Success, Error & Empty States

Every API-powered component should handle these situations:

- **Loading:** The request is in progress.
- **Success:** Data was received and can be displayed.
- **Error:** The request failed.
- **Empty:** The request succeeded, but there is no data to display.

### API Request Flow

```
Component Loads
      |
      v
Loading = true
      |
      v
API Request (fetch)
      |
      v
Check Response
      |
      +---- Error ----> Show Error Message
      |
      v
Save Data in State
      |
      v
Loading = false
      |
      +---- No Data ---> Show Empty Message
      |
      +---- Has Data --> Display Data
```

## 8. Sending Data with POST

Use `POST` to send new data to an API, for example, when a user submits a form.

```jsx
async function createUser() {
  try {
    const response = await fetch("/api/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: "Alex",
        email: "alex@example.com",
      }),
    });

    if (!response.ok) {
      throw new Error("Failed to create user");
    }

    const newUser = await response.json();
    console.log(newUser);
  } catch (error) {
    console.error(error);
  }
}
```

- `method` specifies the HTTP method.
- `headers` describe the request body.
- `JSON.stringify()` converts a JavaScript object into JSON.
- `body` contains the data being sent.
- `response.json()` reads the returned data.

## 9. Updating and Deleting Data

### PUT — Update Data

```jsx
await fetch("/api/users/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Alex Updated",
    email: "alex@example.com",
  }),
});
```

### DELETE — Remove Data

```jsx
await fetch("/api/users/1", {
  method: "DELETE",
});
```

Always check `response.ok` and handle errors in real applications. After a successful request, update your React state or fetch the latest data so the UI reflects the change.

## 10. Handling Forms in React

React forms commonly use state to track user input.

```jsx
import { useState } from "react";

function UserForm() {
  const [name, setName] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    console.log("Submitted name:", name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="Enter your name"
      />

      <button type="submit">Submit</button>
    </form>
  );
}
```

- `value` connects the input to React state.
- `onChange` updates the state as the user types.
- `onSubmit` handles form submission.
- `event.preventDefault()` prevents the browser's default form submission.

You can use the submitted values in a `POST` request to send form data to your API.

## 11. Important Rules to Remember

- Use `useState()` to store changing data.
- Use `useEffect()` for side effects such as fetching data when a component loads.
- Use `fetch()` to communicate with APIs.
- Use `async/await` to make asynchronous code easier to read.
- Use `.map()` to render arrays.
- Use unique keys when rendering lists.
- Do not modify state directly.
- Check `response.ok` because HTTP errors do not automatically reject a `fetch()` Promise.
- Handle loading, error, and empty states.
- Keep form inputs connected to state when using controlled components.

---
