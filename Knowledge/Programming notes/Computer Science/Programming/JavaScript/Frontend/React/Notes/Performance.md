# ⚡ React — Performance Optimization

React performance optimization is about making an application faster and smoother by **avoiding unnecessary work**.

The goal is not to optimize everything, but to understand **what is slow and why**.

## 1. Re-renders

A **re-render** happens when React runs a component again to determine what the UI should look like.

Common causes include:

- A component's state changes.
- Its parent re-renders.
- Its consumed context value changes.

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  console.log("Rendered!");

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

Every time the count changes, `Counter` re-renders.

**Important:** A re-render is normal and does not automatically mean there is a performance problem.

## 2. `React.memo`

`React.memo` can skip re-rendering a component when its props haven't changed according to a shallow comparison using `Object.is`.

```jsx
const Greeting = React.memo(function Greeting({ name }) {
  console.log("Greeting rendered!");

  return <h2>Hello, {name}</h2>;
});
```

If the parent re-renders but `name` remains unchanged, React can reuse the previous result of `Greeting`.

**Use it when:** A component renders frequently with the same props and its rendering is expensive.

**Remember:** `React.memo` does not prevent re-renders caused by the component's own state or consumed context.

## 3. `useMemo`

`useMemo` caches the result of a calculation between renders, as long as its dependencies remain unchanged.

```jsx
const expensiveValue = useMemo(() => {
  return numbers.reduce((sum, n) => sum + n, 0);
}, [numbers]);
```

- The calculation runs when the component renders and the dependencies require it.
- If `numbers` stays the same reference, React can reuse the cached result.
- When `numbers` changes, React recalculates the value.

**Use it when:** A calculation is genuinely expensive or when a stable value helps another optimization.

## 4. `useCallback`

`useCallback` caches a **function definition** between renders while its dependencies remain unchanged.

```jsx
const handleClick = useCallback(() => {
  console.log("Button clicked!");
}, []);
```

Without `useCallback`, a function defined inside a component is normally recreated on each render.

This can matter when passing callbacks to memoized child components.

```jsx
const Child = React.memo(function Child({ onClick }) {
  return <button onClick={onClick}>Click me</button>;
});
```

If the parent passes a new function reference every time, `Child` may re-render even when the function behaves identically.

**Quick distinction:**

- `useMemo` → Caches a calculated value.
- `useCallback` → Caches a function.

## 5. Lazy Loading

Lazy loading means loading a component only when it is needed, rather than loading all components immediately.

React provides `lazy()` and `Suspense` for this.

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard.jsx"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

When React first needs to render `Dashboard`, it loads the component module. While it is loading, `Suspense` displays the fallback.

**Use it when:** A component is large or not needed immediately, such as an admin dashboard or settings page.

## 6. Code Splitting

Code splitting divides your JavaScript into smaller bundles that can be loaded separately.

For example:

```jsx
src/
├── App.jsx
├── Home.jsx
└── Dashboard.jsx
```

With a dynamic import:

```jsx
const Dashboard = lazy(() => import("./Dashboard.jsx"));
```

A compatible build tool can create a separate chunk for `Dashboard`, which can be downloaded when needed.

**The difference:**

- **Code splitting** → Divides code into separate bundles.
- **Lazy loading** → Delays loading until the code is needed.

They often work together, but they are not the same thing.

## 7. When Should You Optimize?

Not every re-render is expensive, and caching has its own costs.

- Start by writing simple, readable components.
- Use React DevTools Profiler to identify slow renders.
- Use `React.memo`, `useMemo`, and `useCallback` when measurements or a clear performance issue justify them.
- Use lazy loading and code splitting to reduce the initial JavaScript that users need to download.
- Avoid adding memoization everywhere without understanding the problem.

## 🧠 Quick Summary

|Feature|Main purpose|
|---|---|
|Re-renders|Recalculate a component's UI|
|`React.memo`|Skip some re-renders when props are unchanged|
|`useMemo`|Cache a calculated value|
|`useCallback`|Cache a function definition|
|Lazy loading|Load a component when needed|
|Code splitting|Divide code into separate bundles|

**Golden rule:** Measure first, understand the bottleneck, and optimize only where it makes a meaningful difference.

---
