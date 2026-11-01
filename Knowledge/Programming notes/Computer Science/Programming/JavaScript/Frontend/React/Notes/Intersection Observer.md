# ⚛️ React — Render Components on Viewport (Intersection Observer)

> 🎯 Render or activate components only when they become visible in the viewport. Useful for lazy loading, animations, and improving performance.

## 1. 👀 Intersection Observer

The browser API `IntersectionObserver` detects when an element enters or leaves the viewport.

```jsx
const observer = new IntersectionObserver(([entry]) => {
  if (entry.isIntersecting) {
    console.log("Element is visible!");
  }
});

observer.observe(element);
```

## 2. 🧩 React Custom Hook

Create a reusable hook to detect visibility.

```jsx
import { useEffect, useRef, useState } from "react";

function useOnScreen() {
  const ref = useRef(null);
  const [visible, setVisible] = useState(false);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        setVisible(entry.isIntersecting);
      }
    );

    if (ref.current) {
      observer.observe(ref.current);
    }

    return () => observer.disconnect();
  }, []);

  return [ref, visible];
}
```

## 3. 🚀 Use the Hook

Render a component only when it becomes visible.

```jsx
function LazyComponent() {
  const [ref, visible] = useOnScreen();

  return (
    <div ref={ref}>
      {visible ? <MyComponent /> : null}
    </div>
  );
}
```

## 4. ⚡ Load Only Once

If you don't want the component to disappear when scrolling away:

```jsx
const observer = new IntersectionObserver(
  ([entry]) => {
    if (entry.isIntersecting) {
      setVisible(true);
      observer.disconnect();
    }
  }
);
```

## 5. 🎛️ Useful Options

```jsx
const observer = new IntersectionObserver(callback, {
  root: null,        // Browser viewport
  threshold: 0.2,    // 20% visibility
  rootMargin: "100px" // Trigger before entering
});
```

|Option|Meaning|
|---|---|
|`root`|Element used as viewport|
|`threshold`|Visibility percentage|
|`rootMargin`|Expands or shrinks detection area|

---

## 💡 Remember

- `IntersectionObserver` detects visibility.
- `useRef` references the DOM element.
- `useState` controls conditional rendering.
- `useEffect` manages observer lifecycle.
- `disconnect()` cleans up the observer.

**Best use cases:** Lazy loading, infinite scrolling, animations, images and heavy components.

✨ **Key idea:** Don't render expensive UI until the user is about to see it.

---
