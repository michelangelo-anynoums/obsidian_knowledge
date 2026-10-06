# 🟢 BLOCK 3 — Lists & Forms

This block is about displaying **lists of data** and letting users **enter information through forms**.

---

## 1. Rendering Lists with `.map()`

In React, we commonly use `.map()` to turn an array into JSX elements.

```jsx
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
  { id: 3, name: "Charlie" }
];

function App() {
  return (
    <div>
      {users.map(user => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
```

Think of `.map()` as:

> **"For every item in this array, create some JSX."**

---

## 2. Why `key`?

When React renders a list, each item needs a **unique key**.

```jsx
{users.map(user => (
  <p key={user.id}>{user.name}</p>
))}
```

The `key` helps React keep track of which item is which.

### ✅ Good

```jsx
key={user.id}
```

### ⚠️ Avoid when possible

```jsx
key={index}
```

A unique ID is usually better than the array index, especially when items can be added, removed, or reordered.

---

## 3. Rendering Components from an Array

You can also use `.map()` to create components.

```jsx
{users.map(user => (
  <User key={user.id} user={user} />
))}
```

Here:

- `user` → the current item
    
- `key={user.id}` → uniquely identifies the item
    
- `user={user}` → passes the user to the `User` component as a prop
    

For example:

```jsx
function User({ user }) {
  return <p>{user.name}</p>;
}
```

---

# 📝 Forms

Forms allow users to enter information.

A simple form:

```jsx
function App() {
  return (
    <form>
      <input />
      <button>Submit</button>
    </form>
  );
}
```

But in React, we usually want to **control the input with state**.

---

## 4. `value` + `onChange`

First, create some state:

```jsx
const [name, setName] = useState("");
```

Then connect it to the input:

```jsx
<input
  value={name}
  onChange={e => setName(e.target.value)}
/>
```

The flow is:

```text
User types
    ↓
onChange runs
    ↓
setName(...) updates state
    ↓
React re-renders
    ↓
value displays the new state
```

This is called a **controlled input**.

---

## 5. Form Submission

Use `onSubmit` on the `<form>`.

```jsx
function App() {
  const [name, setName] = useState("");

  function handleSubmit(e) {
    e.preventDefault();

    console.log(name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={name}
        onChange={e => setName(e.target.value)}
      />

      <button type="submit">
        Submit
      </button>
    </form>
  );
}
```

### Why `e.preventDefault()`?

Normally, submitting a form causes the browser to reload the page.

```jsx
e.preventDefault();
```

stops that default behaviour so React can handle the submission.

---

# ✅ Basic Validation

Before submitting, we can check whether the input is valid.

```jsx
function handleSubmit(e) {
  e.preventDefault();

  if (name.trim() === "") {
    alert("Please enter your name");
    return;
  }

  console.log("Submitted:", name);
}
```

The important pattern is:

```jsx
if (somethingIsWrong) {
  return;
}
```

If the validation fails, we stop the function before submitting.

---

# 🧩 Complete Mini Example

Here is a small form putting everything together:

```jsx
import { useState } from "react";

function App() {
  const [name, setName] = useState("");

  function handleSubmit(e) {
    e.preventDefault();

    if (name.trim() === "") {
      alert("Please enter your name");
      return;
    }

    alert(`Hello, ${name}!`);
    setName("");
  }

  return (
    <form onSubmit={handleSubmit}>
      <h1>Simple Form</h1>

      <input
        type="text"
        placeholder="Enter your name"
        value={name}
        onChange={e => setName(e.target.value)}
      />

      <button type="submit">
        Submit
      </button>
    </form>
  );
}

export default App;
```

---
