# 🧪 React Testing

## 🎯 Goal

Learn how to test React applications so you can make changes confidently without breaking existing features.

## 🧠 What Is Testing?

Testing means checking whether your application works as expected.

In React, we test components, application behavior, and user interactions.

## 📚 Types of Tests

### 1. Unit Tests

Test a small piece of code, such as a function.

**Example:** Check whether a function adds two numbers correctly.

### 2. Component Tests

Test whether a React component renders correctly.

**Example:** Check whether a button or heading appears on the screen.

### 3. User Interaction Tests

Test what happens when a user interacts with the application.

**Example:** Click a button and check whether the displayed number increases.

## 🛠️ Important Tools

- **React Testing Library:** Helps test React components the way users interact with them.
- **Vitest:** A fast testing tool that works well with Vite projects.
- **Jest:** Another popular JavaScript testing framework.

You can start with **Vitest + React Testing Library** if your React project uses Vite.

## 🔄 How React Testing Works

Test the behavior that users actually experience:

```
User clicks a button
        ↓
React state changes
        ↓
Component re-renders
        ↓
UI displays the new result
```

Example:

```
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

A test should check that:

- The button initially displays `Count: 0`.
- The user clicks the button.
- The button updates to `Count: 1`.

## ✅ What Should I Test?

- Does the component render correctly?
- Does the button work when clicked?
- Does the UI update when state changes?
- Does the application display the correct result?
- Do important features still work after code changes?

---
