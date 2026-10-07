# 🟡 React — useEffect

> [!summary] Mental Model  
> **==useEffect== synchronizes your component with something outside React.**
> 
> Think:  
> **“When these dependencies change, synchronize with this external system.”**
> 
> Not:  
> ~~“Run this code after rendering.”~~

---

## 🧠 What is a Side Effect?

A **side effect** is something your component does that interacts with the world outside of React.

Common examples:

- 🌐 Fetching data from an API
    
- ⏱️ Starting a timer
    
- 📡 Subscribing to events
    
- 🖥️ Using browser APIs
    
- 💾 Synchronizing with external systems
    

That's where `useEffect` comes in.

---

## 🔧 Basic Syntax

```jsx
useEffect(() => {
  // effect
}, [dependencies]);
```

There are two important parts:

- **Effect function** → the code React should run
    
- **Dependency array** → tells React when the effect should run again
    

---

## 1️⃣ Run Once

```jsx
useEffect(() => {
  fetchUsers();
}, []);
```

The empty dependency array `[]` means:

> Run the effect after the initial render, and don't re-run it because of later renders.

This is commonly used for initial data fetching.

---

## 2️⃣ With Dependencies

```jsx
useEffect(() => {
  fetchUser(id);
}, [id]);
```

Now the effect depends on `id`.

It runs:

1. After the component initially renders
    
2. Again whenever `id` changes
    

### Example

```text
id = 1
  ↓
fetchUser(1)

id changes to 2
  ↓
fetchUser(2)
```

---

## 🧹 Cleanup Functions

Some effects create something that needs to be stopped or removed.

For example, a timer:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("tick");
  }, 1000);

  return () => clearInterval(timer);
}, []);
```

The function returned from `useEffect` is the **cleanup function**.

```text
Effect starts
    ↓
Timer runs
    ↓
Component/effect is cleaned up
    ↓
clearInterval(timer)
```

### Common cleanup examples

- `clearInterval()`
    
- `clearTimeout()`
    
- Unsubscribing from events
    
- Removing event listeners
    
- Disconnecting from external systems
    

---

## 🌐 Fetching API Data

A common React pattern is:

```text
Loading
   ↓
 Fetch
   ↓
Success
   ↘
   Error
```

For example:

```jsx
const [users, setUsers] = useState([]);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);

useEffect(() => {
  async function fetchUsers() {
    try {
      const response = await fetch("/api/users");

      if (!response.ok) {
        throw new Error("Failed to fetch users");
      }

      const data = await response.json();
      setUsers(data);
    } catch (error) {
      setError(error.message);
    } finally {
      setLoading(false);
    }
  }

  fetchUsers();
}, []);
```

Then your UI can represent the three states:

```jsx
if (loading) {
  return <p>Loading...</p>;
}

if (error) {
  return <p>Error: {error}</p>;
}

return (
  <ul>
    {users.map((user) => (
      <li key={user.id}>{user.name}</li>
    ))}
  </ul>
);
```

---

## 🎯 The Important Pattern

When fetching data, think in terms of **state transitions**:

```text
┌─────────┐
│ Loading │
└────┬────┘
     │
     ▼
  Fetch API
   /     \
  /       \
 ▼         ▼
Success   Error
  │         │
  ▼         ▼
Display   Show error
data
```

Usually you'll need at least:

```jsx
const [data, setData] = useState([]);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
```

---

## 🧩 Dependency Array Cheat Sheet

|Dependencies|Meaning|
|---|---|
|`[]`|Run after the initial render|
|`[id]`|Run initially and whenever `id` changes|
|`[id, user]`|Run initially and whenever `id` or `user` changes|
|No array|Run after every render — use carefully|

```jsx
// Once
useEffect(() => {
  // ...
}, []);
```

```jsx
// When id changes
useEffect(() => {
  // ...
}, [id]);
```

---

## ⚠️ Common Mistakes

### Forgetting dependencies

If your effect uses a value from the component, that value may need to be included in the dependency array.

```jsx
useEffect(() => {
  fetchUser(id);
}, [id]);
```

### Forgetting cleanup

If an effect creates a timer, subscription, or event listener, consider whether it needs cleanup.

### Putting everything in `useEffect`

Not every piece of code belongs in an effect.

> **Use effects for synchronization with external systems — not simply because you want some code to run.**

---

## 🧠 Remember

```text
useEffect
    │
    ├── 🌐 API requests
    ├── ⏱️ Timers
    ├── 📡 Subscriptions
    ├── 🖥️ Browser APIs
    └── 🔄 External systems
```

The core idea:

> **When a dependency changes, synchronize with the outside world.**

---
