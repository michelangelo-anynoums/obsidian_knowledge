# ⚛️ React Setup

> **Goal:** Create a React app, build a component, and render it.

## 1. Create the Project

```bash
npm create vite@latest my-react-app
cd my-react-app
npm install
npm run dev
```

Open the URL shown in your terminal, usually:

```text
http://localhost:5173
```

## 2. Create a Component

In `src/App.jsx`:

```jsx
function App() {
  return <h1>Hello, React!</h1>;
}

export default App;
```

This creates a React **component** called `App`.

## 3. Render the Component

React starts from `src/main.jsx`:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

The important part is:

```jsx
<App />
```

This tells React:

> **Render the App component inside the element with id="root".**

## 4. How It All Connects

```text
index.html
    ↓
<div id="root"></div>
    ↓
main.jsx
    ↓
<App />
    ↓
App.jsx
    ↓
<h1>Hello, React!</h1>
    ↓
🌐 Browser
```

### 🧠 Remember

- **Component** → describes the UI
    
- **main.jsx** → starts React
    
- **createRoot()** → connects React to the HTML
    
- **.render()** → tells React what to display
    
- **App** → renders your component

---
