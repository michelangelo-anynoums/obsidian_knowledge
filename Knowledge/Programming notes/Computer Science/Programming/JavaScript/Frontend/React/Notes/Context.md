# 🟠 Block 8 — React Context

> [!abstract] 🎯 Goal Share genuinely global data across components without passing props through many layers.

## 🧠 1. What Is Context?

**React Context** allows components to share data without manually passing props through every component in between.

Normally, data flows from parent to child through **props**. When many components need the same data, this can lead to _prop drilling_.

Context helps solve this problem by making data available to components that need it.

## 🧩 2. The Three Main Concepts

### `createContext()`

Creates a Context object that components can use to share data.

```jsx
import { createContext } from "react";

const ThemeContext = createContext("light");
```

Here, `"light"` is the default value used when a component has no matching Provider above it.

### `Provider`

A Provider makes a value available to components inside its tree.

```jsx
import { createContext } from "react";

const ThemeContext = createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Home />
    </ThemeContext.Provider>
  );
}
```

In this example, `Home` and its descendants can access the value `"dark"`.

### `useContext()`

A Hook that reads the value of a Context.

```jsx
import { useContext } from "react";

function Home() {
  const theme = useContext(ThemeContext);

  return <h1>Current theme: {theme}</h1>;
}
```

**Remember:**

- `createContext()` → creates the Context.
- `Provider` → supplies the value.
- `useContext()` → reads the value.

## 🔄 3. How Context Works

```jsx
App
 └── ThemeContext.Provider
      └── Layout
           └── Navbar
                └── ThemeButton
```

`ThemeButton` can access the theme directly through Context, even though `Layout` and `Navbar` sit between it and the Provider.

This avoids passing the theme through every intermediate component.

## 🌍 4. When Is Context Useful?

Use Context when several components need access to the same shared data.

|Use case|Example|
|---|---|
|🎨 Theme|Light or dark mode|
|🔐 Authentication|Current user or login status|
|🌐 Language|Selected application language|
|⚙️ Global settings|User preferences|

Context is especially helpful when the data is needed by multiple components at different levels of the component tree.

## 🚫 5. When Is Context NOT Useful?

Context is not the best solution for every situation.

- **Simple parent-to-child data:** Use props.
- **Data needed by only one component:** Keep it local.
- **A few layers of components:** Passing props is often simpler.
- **Frequently changing, complex application state:** Consider whether a dedicated state-management solution is more appropriate.

⚠️ **Important:** Context does not automatically manage your state. It distributes a value. If that value comes from `useState`, changing the state can update the components consuming the Context.

## 💻 6. Complete Example — Theme Context

```jsx
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext("light");

function App() {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={theme}>
      <button
        onClick={() =>
          setTheme(theme === "light" ? "dark" : "light")
        }
      >
        Toggle Theme
      </button>

      <Home />
    </ThemeContext.Provider>
  );
}

function Home() {
  const theme = useContext(ThemeContext);

  return <h1>Current theme: {theme}</h1>;
}

export default App;
```

**What happens?**

1. `createContext()` creates `ThemeContext`.
2. `useState()` stores the current theme.
3. The Provider shares the theme with its descendants.
4. `useContext()` reads the theme inside `Home`.
5. Clicking the button changes the theme, updating the displayed value.

## ⚡ 7. Important Rules to Remember

- A component must be inside the relevant Provider to receive its provided value.
- `useContext()` must be called at the top level of a React component or custom Hook.
- The nearest matching Provider determines the value a consumer receives.
- A Context's default value is used when no matching Provider exists above the consumer.
- Context can trigger re-renders when its provided value changes.

## 📝 8. Quick Summary

|Concept|Purpose|
|---|---|
|`createContext()`|Creates a Context|
|Provider|Supplies a value to descendants|
|`useContext()`|Reads the Context value|
|Props|Pass data directly between components|
|Context|Shares data across multiple component levels|

> [!success] 💡 Key Takeaway Use **props** for direct communication between components and **Context** when genuinely shared data needs to reach many components without prop drilling.

---
