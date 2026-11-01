# ⚛️ React — useRef (References)

## 🎯 What is useRef?

`useRef` creates a reference that allows us to access a DOM element directly.

> [!abstract] Think of it as a **pointer to an HTML element**.

```jsx
import { useRef } from "react";

function App() {
  const myRef = useRef(null);

  return <div ref={myRef}>Hello!</div>;
}
```

## 🔍 How does it work?

**1. Create the reference**

```jsx
const myRef = useRef(null);
```

- Creates a reference object.
- Initially, its value is `null`.

**2. Connect it to an element**

```jsx
<div ref={myRef}>Hello!</div>
```

React automatically connects the reference to that DOM element.

**3. Access the element**

```jsx
myRef.current
```

`.current` contains the actual HTML element.

For example:

```jsx
myRef.current.style.color = "red";
```

Now the text becomes red.

## 💡 Practical example — Focus an input


```jsx
import { useRef } from "react";

function App() {
  const inputRef = useRef(null);

  function handleClick() {
    inputRef.current.focus();
  }

  return (
    <>
      <input ref={inputRef} />

      <button onClick={handleClick}>
        Focus input
      </button>
    </>
  );
}
```

When clicking the button, React uses the reference to focus the input.

## 🧠 useRef vs useState

|useRef|useState|
|---|---|
|Stores a reference/value|Stores reactive state|
|Changes don't trigger re-render|Changes trigger re-render|
|Access using `.current`|Access using state variable|
|Useful for DOM elements|Useful for UI updates|

## ⭐ Remember

- `useRef(null)` → Creates a reference.
- `ref={myRef}` → Connects it to a DOM element.
- `myRef.current` → Accesses the element.
- React manages the connection automatically.

**Key idea:** `useRef` gives us a way to reach an actual HTML element without manually searching the DOM.

---
