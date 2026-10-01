# 🟢 React Basics

> **Goal:** Build a page using **reusable components**.

## 1. ⚛️ What is React?

**React** is a JavaScript library for building user interfaces.

It lets you build a page from small, reusable pieces called **components**.

---

## 2. 🧩 Components

A component is a JavaScript function that returns JSX.

```jsx
function Welcome() {
  return <h1>Hello!</h1>;
}
```

Think:

> **Component = reusable piece of UI**

---

## 3. ✨ JSX

JSX lets you write HTML-like code inside JavaScript.

```jsx
const title = <h1>Hello World!</h1>;
```

JSX looks like HTML, but it is written inside JavaScript.

---

## 4. 🖥️ Rendering

Rendering means **displaying a component on the screen**.

```jsx
function App() {
  return <h1>Hello React!</h1>;
}
```

`App` is rendered to show the UI.

---

## 5. 🎨 `className`

In JSX, use `className` instead of HTML's `class`.

```jsx
<h1 className="title">Hello!</h1>
```

---

## 6. `{ }` — JavaScript inside JSX

Use `{ }` to put JavaScript expressions inside JSX.

```jsx
const name = "Alex";

function Welcome() {
  return <h1>Hello, {name}!</h1>;
}
```

Output:

```text
Hello, Alex!
```

---

## 7. 🧱 Components inside Components

Components can be used inside other components.

```jsx
function Welcome() {
  return <h1>Hello!</h1>;
}

function App() {
  return (
    <div>
      <Welcome />
      <Welcome />
    </div>
  );
}
```

This is how we build bigger interfaces from smaller pieces.

---

## 8. 📦 Props

**Props** let you pass information from one component to another.

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

Use it like this:

```jsx
<Welcome name="Alex" />
<Welcome name="Sam" />
```

Result:

```text
Hello, Alex
Hello, Sam
```

> **Props = information passed into a component**

---

## 🧠 Remember

- **React** → builds user interfaces
    
- **Component** → reusable UI piece
    
- **JSX** → HTML-like syntax in JavaScript
    
- **className** → CSS class in JSX
    
- **{ }** → JavaScript inside JSX
    
- **Props** → pass data to components
    

### 🎯 Block 1 Goal

> **Build a page from reusable components.**

**Next → Block 2 🚀**

---
