# 🟢 Block 1 — React Basics

> **Goal:** Build a page using small, reusable components.

## 1. What is React?

**React** is a JavaScript library for building user interfaces.

Instead of creating one large page, we build it from **components**.

```text
Page
 ├── Header
 ├── Welcome
 ├── Content
 └── Footer
```

## 2. Components

A component is a JavaScript function that returns JSX.

```jsx
function Welcome() {
  return <h1>Welcome!</h1>;
}
```

Render it with:

```jsx
<Welcome />
```

Components can also contain other components:

```jsx
function App() {
  return (
    <div>
      <Welcome />
      <Footer />
    </div>
  );
}
```

## 3. JSX

JSX looks like HTML but lives inside JavaScript.

```jsx
function App() {
  return <h1>Hello React!</h1>;
}
```

### `className`

In JSX, use `className` instead of HTML's `class`:

```jsx
<h1 className="title">Hello</h1>
```

### JavaScript inside JSX

Use `{ }` to insert JavaScript:

```jsx
const name = "Alex";

<h1>Hello, {name}!</h1>
```

You can also use expressions:

```jsx
<p>2 + 2 = {2 + 2}</p>
```

## 4. Rendering

React renders a component into the HTML element with `id="root"`:

```jsx
createRoot(document.getElementById("root")).render(
  <App />
);
```

So:

```text
<App />
   ↓
App component
   ↓
Other components
   ↓
Browser UI
```

## 5. Props

**Props** allow a component to receive data.

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

Use it like this:

```jsx
<Welcome name="Alex" />
<Welcome name="Sam" />
```

Result:

```text
Hello, Alex!
Hello, Sam!
```

Think of **props as information passed into a component.**

---

## 🧠 Remember

```text
React
 └── Components
      ├── JSX
      ├── JavaScript { }
      ├── Other components
      └── Props
```

> **React = Build the page from reusable components.** 🎯

---
