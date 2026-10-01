# ⚛️ React Roadmap

> [!summary] Goal  
> Learn React by building things. Don't try to learn the entire ecosystem before making your first app.

---

## 🟢 BLOCK 0 — JavaScript Foundation [[JavaScript Foundation]]

Before React, be comfortable with:

- Variables: `let`, `const`
    
- Functions & arrow functions
    
- Objects & arrays
    
- Destructuring
    
- Spread operator `...`
    
- `map()`, `filter()`, `find()`, `reduce()`
    
- `import` / `export`
    
- Promises
    
- `async` / `await`
    
- DOM basics
    
- ES6+ syntax
    

> 🎯 **Goal:** You should be able to read modern JavaScript comfortably.

---

## 🟢 BLOCK 1 — React Basics

Learn:

- What React is
    
- Components
    
- JSX
    
- Rendering
    
- `className`
    
- JavaScript inside JSX `{ }`
    
- Components inside components
    
- Props
    

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

> 🎯 **Goal:** Build a page from reusable components.

---

## 🟢 BLOCK 2 — State & Events

Learn:

- `useState()`
    
- Event handlers
    
- `onClick`
    
- `onChange`
    
- Controlled inputs
    
- Conditional rendering
    

```jsx
const [count, setCount] = useState(0);

<button onClick={() => setCount(count + 1)}>
  {count}
</button>
```

> 🎯 **Goal:** Build interactive components.

---

## 🟢 BLOCK 3 — Lists & Forms

Learn:

- `.map()` in JSX
    
- `key`
    
- Rendering arrays
    
- Forms
    
- Inputs
    
- `value`
    
- `onChange`
    
- Form submission
    
- Basic validation
    

```jsx
{users.map(user => (
  <User key={user.id} user={user} />
))}
```

> 🎯 **Goal:** Build a todo list or simple form.

---

## 🟡 BLOCK 4 — `useEffect`

Learn:

- What effects are
    
- `useEffect()`
    
- Dependency array
    
- Cleanup
    
- Fetching data
    

```jsx
useEffect(() => {
  fetchUsers();
}, []);
```

Understand **why** an effect runs, not just the syntax.

> 🎯 **Goal:** Fetch and display API data.

---

## 🟡 BLOCK 5 — Component Architecture

Learn:

- Parent → child props
    
- Child → parent communication
    
- Lifting state up
    
- Reusable components
    
- Component composition
    
- Separating UI and logic
    

```text
App
├── Header
├── Search
├── UserList
│   └── UserCard
└── Footer
```

> 🎯 **Goal:** Stop putting your entire application into one component.

---

## 🟡 BLOCK 6 — Routing

Learn:

- React Router
    
- Routes
    
- Links
    
- Dynamic routes
    
- URL parameters
    
- Navigation
    
- 404 pages
    

Example:

```text
/
├── /about
├── /products
├── /products/:id
└── /login
```

> 🎯 **Goal:** Build a multi-page-feeling SPA.

---

## 🟡 BLOCK 7 — API & Async Data

Learn:

- `fetch()`
    
- GET / POST / PUT / DELETE
    
- Loading states
    
- Error states
    
- Empty states
    
- Async/await
    
- Sending form data
    
- API response handling
    

```text
Loading...
     ↓
API Request
     ↓
Success → Show data
     ↓
Error → Show error
```

> 🎯 **Goal:** Build a frontend that communicates with a real API.

---

## 🟠 BLOCK 8 — Context

Learn:

- `createContext()`
    
- `useContext()`
    
- Provider
    
- When Context is useful
    
- When Context is **not** useful
    

Good examples:

- Theme
    
- Authentication
    
- Language
    
- Global settings
    

> 🎯 **Goal:** Share genuinely global data without passing props through many layers.

---

## 🟠 BLOCK 9 — Custom Hooks

Learn:

- What a custom hook is
    
- Rules of Hooks
    
- Extracting reusable logic
    

```jsx
function useFetch(url) {
  // reusable data-fetching logic
}
```

> 🎯 **Goal:** Reuse **logic**, not just components.

---

## 🟠 BLOCK 10 — State Management

First understand React state well.

Then learn **one** state-management solution:

- Redux Toolkit
    
- Zustand
    
- Another current solution
    

Understand:

- Global state
    
- Stores
    
- Actions
    
- Updating state
    
- When global state is actually necessary
    

> 🎯 **Goal:** Manage complex application state without chaos.

---

## 🔵 BLOCK 11 — Performance

Learn the basics:

- Re-renders
    
- `React.memo`
    
- `useMemo`
    
- `useCallback`
    
- Lazy loading
    
- Code splitting
    

But don't optimize everything automatically.

> 🎯 **Goal:** Understand **why** something is slow before optimizing it.

---

## 🔵 BLOCK 12 — Testing

Learn:

- Unit tests
    
- Component tests
    
- User interaction tests
    
- React Testing Library
    
- Vitest or Jest
    

Test things users actually do:

```text
Click button
     ↓
State changes
     ↓
UI updates
```

> 🎯 **Goal:** Be able to confidently change your application without breaking it.

---

## 🟣 BLOCK 13 — TypeScript

Once you're comfortable with React + JavaScript:

Learn:

- Types
    
- Interfaces
    
- Props types
    
- State types
    
- Function types
    
- API response types
    
- Generics — later
    

```tsx
type UserProps = {
  name: string;
  age: number;
};
```

> 🎯 **Goal:** Build React applications with fewer type-related mistakes.

---

## 🟣 BLOCK 14 — Real-World React

Learn:

- Environment variables
    
- Authentication
    
- Authorization
    
- API architecture
    
- Error handling
    
- Form libraries
    
- Data-fetching/caching libraries
    
- Accessibility
    
- Responsive UI
    
- Deployment
    
- Git
    

> 🎯 **Goal:** Build and deploy a real application.

---

# 🚀 PROJECT ROADMAP

Don't just watch tutorials. Build these:

### 1️⃣ Beginner

**Todo App**

Learn:

```text
Components
Props
useState
Events
Forms
map()
filter()
```

### 2️⃣ Beginner+

**Weather App**

Learn:

```text
API
fetch()
useEffect
Loading
Errors
Conditional rendering
```

### 3️⃣ Intermediate

**Movie / Product App**

Learn:

```text
Routing
Search
Filters
API
Reusable components
URL parameters
```

### 4️⃣ Intermediate+

**Dashboard**

Learn:

```text
Authentication
Routing
Context
Charts
Forms
API
Reusable layouts
```

### 5️⃣ Advanced

**Full-stack application**

Learn:

```text
React
TypeScript
API
Database
Authentication
State management
Testing
Deployment
```

---

# 🧠 THE ORDER TO REMEMBER

```text
JavaScript
    ↓
JSX
    ↓
Components
    ↓
Props
    ↓
useState
    ↓
Events
    ↓
Lists & Forms
    ↓
useEffect
    ↓
API
    ↓
Component Architecture
    ↓
Routing
    ↓
Context
    ↓
Custom Hooks
    ↓
State Management
    ↓
Performance
    ↓
Testing
    ↓
TypeScript
    ↓
Real Projects
```

> [!important] Don't Overlearn  
> You **do not** need to master every React feature before building projects.
> 
> Learn a block → build something → get stuck → learn what you need → continue.

# 🎯 The 80/20 React Stack

If you want the **minimum essential path**, focus on:

```text
JavaScript
+
React
├── JSX
├── Components
├── Props
├── useState
├── Events
├── Forms
├── Lists
├── useEffect
├── API calls
├── Routing
├── Context
└── Custom Hooks

Then:
TypeScript
Testing
Deployment
```

> [!tip] Final Rule  
> **Don't learn React as a collection of APIs. Learn it as a way to build UI from components and state.**