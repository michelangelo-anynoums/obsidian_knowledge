# 🟠 Block 10 — State Management in React

> [!abstract] Overview **State management** is the process of storing, organizing, sharing, and updating data in a React application. The objective is to keep application behavior predictable as components and features become more complex.

## 1. 🧠 Understanding React State

### What is state?

State is data that a React component remembers between renders. It can change in response to user interactions, network responses, or other events.

For example, a counter needs to remember its current number. A form needs to remember what the user has typed. A shopping cart needs to remember which products have been added.

React provides the `useState` Hook to manage state inside function components.

### Example: A counter

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount(count + 1);
  }

  return (
    <div>
      <p>Current count: {count}</p>
      <button onClick={increment}>
        Increment
      </button>
    </div>
  );
}

export default Counter;
```

**How it works:**

- `useState(0)` initializes the state with the value `0`.
- `count` contains the current state value for that render.
- `setCount` requests a state update.
- React renders the component again when the update is processed.
- The paragraph displays the new count.

State is not simply an ordinary variable. Changing a normal variable does not tell React to update the interface.

### Example: Why ordinary variables are not enough

```jsx
function Counter() {
  let count = 0;

  function increment() {
    count = count + 1;
    console.log(count);
  }

  return (
    <button onClick={increment}>
      Count: {count}
    </button>
  );
}
```

Clicking this button changes the local variable, but the displayed number does not update as intended. React does not track ordinary variable assignments as state updates.

Using `useState` solves this problem because React knows that the component needs to render again.

### Updating state based on its previous value

When the next state depends on the previous state, use the functional updater form.

```jsx
setCount(previousCount => previousCount + 1);
```

This is particularly useful when multiple updates are queued together.

```jsx
function incrementThreeTimes() {
  setCount(count => count + 1);
  setCount(count => count + 1);
  setCount(count => count + 1);
}
```

Each updater receives the result of the previous update. Clicking the button that calls this function increases the count by three.

> [!important] State is a snapshot A state variable represents the value for the current render. Calling its setter requests a future update; it does not change the value of that variable immediately within the already-running function.

## 2. 📦 Managing Objects and Arrays in State

React state often contains more than a number or a string. It can contain objects, arrays, or nested data structures.

### Example: Updating an object

Imagine a profile containing a user's name and age.

```jsx
import { useState } from "react";

function Profile() {
  const [user, setUser] = useState({
    name: "Alex",
    age: 25
  });

  function changeName() {
    setUser(previousUser => ({
      ...previousUser,
      name: "Jordan"
    }));
  }

  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Age: {user.age}</p>

      <button onClick={changeName}>
        Change name
      </button>
    </div>
  );
}
```

The spread operator (`...previousUser`) copies the existing properties into a new object. The `name` property is then replaced while `age` remains unchanged.

Without the spread, the update could accidentally discard other properties.

### Why direct mutation is a problem

```jsx
// ❌ Avoid mutating the existing object
user.name = "Jordan";
setUser(user);
```

This changes the existing object instead of creating a new one. React relies heavily on object identity when determining whether values have changed, so this pattern can prevent expected updates and introduce bugs.

Prefer immutable updates:

```jsx
// ✅ Create a new object
setUser(previousUser => ({
  ...previousUser,
  name: "Jordan"
}));
```

### Example: Updating an array

Consider a list of tasks.

```jsx
const [tasks, setTasks] = useState([
  { id: 1, title: "Learn React", done: false },
  { id: 2, title: "Learn state", done: false }
]);
```

Adding a task:

```jsx
setTasks(previousTasks => [
  ...previousTasks,
  { id: 3, title: "Learn Zustand", done: false }
]);
```

Removing a task:

```jsx
setTasks(previousTasks =>
  previousTasks.filter(task => task.id !== 2)
);
```

Marking a task as completed:

```jsx
setTasks(previousTasks =>
  previousTasks.map(task =>
    task.id === 1
      ? { ...task, done: true }
      : task
  )
);
```

These operations create new arrays and, when necessary, new objects. They do not mutate the existing state.

## 3. 🧩 Local State and Shared State

### Local state

Local state belongs to a component and is used to control its own behavior.

Common examples include:

- Whether a dropdown is open.
- The current value of an input.
- Whether a modal is visible.
- The currently selected tab.

```jsx
function Toggle() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div>
      <button onClick={() => setIsOpen(open => !open)}>
        Toggle details
      </button>

      {isOpen && <p>Additional information.</p>}
    </div>
  );
}
```

The `isOpen` value only needs to be shared if another component also needs to control or read it.

### Sharing state through a common parent

Suppose an application has two components:

- `SearchInput`, which lets the user enter a search term.
- `SearchResults`, which displays matching results.

Both components need access to the same search term.

One solution is to store the state in their closest common parent and pass it down through props.

```jsx
import { useState } from "react";

function SearchInput({ query, onQueryChange }) {
  return (
    <input
      value={query}
      onChange={event => onQueryChange(event.target.value)}
      placeholder="Search products..."
    />
  );
}

function SearchResults({ query }) {
  return <p>Searching for: {query || "nothing yet"}</p>;
}

function SearchPage() {
  const [query, setQuery] = useState("");

  return (
    <div>
      <SearchInput
        query={query}
        onQueryChange={setQuery}
      />

      <SearchResults query={query} />
    </div>
  );
}
```

Here, `SearchPage` owns the state. Both child components receive the same value, so the input and results remain synchronized.

This technique is called **lifting state up**.

### When does prop drilling become a problem?

Imagine a deeply nested component tree:

`App → Layout → Sidebar → UserMenu → UserAvatar`

If `UserAvatar` needs user data stored in `App`, every intermediate component might have to receive and forward the data through props.

This is called **prop drilling**.

Passing props through a few components is perfectly reasonable. It becomes inconvenient when many intermediate components pass data they do not actually use.

At that point, React Context or a global state-management library may help.

## 4. 🌍 What Is Global State?

Global state is shared data that can be accessed by multiple components without manually passing it through every level of the component tree.

Common examples include:

- The currently authenticated user.
- Shopping cart contents.
- Application preferences.
- Shared UI state used by different pages.
- Data needed by several distant components.

Imagine an e-commerce application with this component structure:

```jsx
App
├── Header
│   └── CartIcon
├── ProductPage
│   └── AddToCartButton
└── CartPage
    └── CartItems
```

When a user adds a product, the cart icon and cart page need to reflect the updated cart.

Without shared state, you might have to lift the cart state to a common parent and pass it through several layers. As the application grows, a dedicated store can make the relationship clearer.

> [!tip] A useful distinction Global state does not mean every component can or should modify every value. Shared state still needs clear ownership and predictable update rules.

---
