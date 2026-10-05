# 🟢 BLOCK 2 — State & Events

### 🎯 Goal

Learn how to make React components **interactive and responsive to user actions**.

## 1. `useState()`

Use `useState` when a component needs to **remember and update information**.

```jsx
const [count, setCount] = useState(0);
```

- `count` → current value
    
- `setCount` → function used to update it
    
- `0` → initial value
    

---

## 2. Event Handlers

React can respond to user actions such as:

- Clicking a button
    
- Typing into an input
    
- Submitting a form
    
- Moving the mouse
    

Example:

```jsx
<button onClick={() => console.log("Clicked!")}>
  Click me
</button>
```

### Important events

```jsx
onClick
onChange
onSubmit
```

---

## 3. `onClick`

Run something when the user clicks an element.

```jsx
<button onClick={() => setCount(count + 1)}>
  {count}
</button>
```

Every click increases the count by `1`.

---

## 4. `onChange`

Use `onChange` to detect changes in an input.

```jsx
<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

React can now keep track of what the user types.

---

## 5. Controlled Inputs

A **controlled input** is an input whose value is controlled by React state.

```jsx
const [name, setName] = useState("");

<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

Think:

**Input → event → state → UI**

---

## 6. Conditional Rendering

Show different things depending on a condition.

```jsx
{isLoggedIn ? <p>Welcome!</p> : <p>Please log in.</p>}
```

Or simply:

```jsx
{isLoggedIn && <p>Welcome!</p>}
```

---

## 🧩 Putting It Together

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

### 🧠 Remember

**State** = information your component remembers.

**Events** = things the user does.

**Event handler** = code that reacts to those actions.

**Controlled input** = an input managed by React state.

**Conditional rendering** = showing UI based on a condition.

### 🎯 Block 2 Goal

> **Build interactive React components that respond to user actions and update their UI.**