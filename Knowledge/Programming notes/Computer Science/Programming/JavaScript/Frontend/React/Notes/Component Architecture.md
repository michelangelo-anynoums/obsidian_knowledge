# 🟡 Block 5 — Component Architecture

> **Goal:** Stop putting your entire application into one component.

Component architecture is about breaking a large UI into **small, focused pieces**.

Instead of having one huge `App.jsx`, we create components that each have a clear responsibility.

---

## 🧠 1. Parent → Child Props

A **parent** can send information to a **child** using `props`.

Think:

```js
Parent
  ↓
  props
  ↓
Child
```

### Example

```js
function App() {
  return <UserCard name="John" age={25} />;
}

function UserCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
    </div>
  );
}
```

Here:

```js
<UserCard name="John" age={25} />
```

is the parent giving information to `UserCard`.

The child receives it through `props`:

```js
function UserCard(props) {
```

You can also use destructuring:

```js
function UserCard({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
    </div>
  );
}
```

### ⭐ Remember

**Parent → Child = Props**

---

# 🔄 2. Child → Parent Communication

Things are slightly different when a child needs to communicate with its parent.

A child **cannot directly change the parent's state**.

Instead, the parent gives the child a **function**.

### Example

```js
function App() {
  function handleMessage() {
    console.log("Hello from the child!");
  }

  return <Button onClick={handleMessage} />;
}

function Button({ onClick }) {
  return (
    <button onClick={onClick}>
      Click me
    </button>
  );
}
```

What's happening?

```js
App
 │
 │ gives function
 ↓
Button
 │
 │ calls function
 ↓
App
```

The parent owns the function:

```js
function handleMessage() {
  console.log("Hello from the child!");
}
```

Then passes it down:

```js
<Button onClick={handleMessage} />
```

The child calls it:

```js
<button onClick={onClick}>
```

### ⭐ Remember

**Child → Parent = Callback function**

---

# ⬆️ 3. Lifting State Up

Sometimes two components need access to the same state.

Instead of keeping the state inside one child, move it **up to their common parent**.

This is called **lifting state up**.

### ❌ Before

Imagine `Search` has its own search state:

```js
function Search() {
  const [search, setSearch] = useState("");

  return (
    <input
      value={search}
      onChange={(e) => setSearch(e.target.value)}
    />
  );
}
```

But now `UserList` also needs to know what the user searched for.

The state is in the wrong place.

### ✅ After

Move the state into `App`:

```js
function App() {
  const [search, setSearch] = useState("");

  return (
    <>
      <Search
        search={search}
        setSearch={setSearch}
      />

      <UserList search={search} />
    </>
  );
}
```

Now both components can work with the same state.

```js
             App
              │
       search state
          /       \
         ↓         ↓
      Search    UserList
```

### ⭐ Remember

If multiple components need the same state:

> **Move the state up to their common parent.**

---

# ♻️ 4. Reusable Components

A good component should ideally be reusable.

For example, instead of creating three different user cards:

```js
<UserCard />
<UserCard />
<UserCard />
```

we can create **one** `UserCard` component and give it different data.

```js
function UserCard({ name, role }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{role}</p>
    </div>
  );
}
```

Then:

```js
<UserCard
  name="Alice"
  role="Developer"
/>

<UserCard
  name="Bob"
  role="Designer"
/>

<UserCard
  name="Sarah"
  role="Manager"
/>
```

One component.

Three different uses.

### ⭐ Think:

```js
One component
      ↓
Different props
      ↓
Different results
```

---

# 🧩 5. Component Composition

Composition means **building a bigger component by combining smaller components**.

For example:

```js
App
├── Header
├── Search
├── UserList
│   └── UserCard
└── Footer
```

Each piece does one job.

Your `App` might look like:

```js
function App() {
  return (
    <>
      <Header />

      <Search />

      <UserList />

      <Footer />
    </>
  );
}
```

`UserList` can then contain multiple `UserCard` components:

```js
function UserList() {
  return (
    <div>
      <UserCard name="Alice" />
      <UserCard name="Bob" />
      <UserCard name="Sarah" />
    </div>
  );
}
```

This gives you a hierarchy:

```js
App
 │
 ├── Header
 │
 ├── Search
 │
 ├── UserList
 │    ├── UserCard
 │    ├── UserCard
 │    └── UserCard
 │
 └── Footer
```

That's **component composition**.

---

# 🎨 6. Separate UI From Logic

Try not to put everything into the same component.

For example, this can become difficult to maintain:

```js
function App() {
  // fetching data
  // filtering data
  // handling forms
  // managing state
  // rendering UI
  // handling buttons
  // etc...
}
```

Instead, separate responsibilities.

For example:

```js
components/
├── Header.jsx
├── Search.jsx
├── UserList.jsx
├── UserCard.jsx
└── Footer.jsx

hooks/
└── useUsers.js
```

Your UI components can focus on **what things look like**.

Your hooks or other logic can focus on **how things work**.

---

# 🏗️ Putting Everything Together

Let's create a small user application.

## Folder structure

```js
src/
├── components/
│   ├── Header.jsx
│   ├── Search.jsx
│   ├── UserList.jsx
│   ├── UserCard.jsx
│   └── Footer.jsx
│
└── App.jsx
```

---

## `App.jsx`

The parent owns the search state:

```js
import { useState } from "react";

import Header from "./components/Header";
import Search from "./components/Search";
import UserList from "./components/UserList";
import Footer from "./components/Footer";

function App() {
  const [search, setSearch] = useState("");

  return (
    <>
      <Header />

      <Search
        search={search}
        setSearch={setSearch}
      />

      <UserList search={search} />

      <Footer />
    </>
  );
}

export default App;
```

Notice that `App` isn't responsible for rendering the entire application.

It's mainly **connecting the pieces together**.

---

## `Search.jsx`

```js
function Search({ search, setSearch }) {
  return (
    <input
      type="text"
      placeholder="Search users..."
      value={search}
      onChange={(e) => setSearch(e.target.value)}
    />
  );
}

export default Search;
```

The `Search` component receives:

```js
search
setSearch
```

from `App`.

---

## `UserList.jsx`

```js
import UserCard from "./UserCard";

function UserList({ search }) {
  const users = [
    { id: 1, name: "Alice", role: "Developer" },
    { id: 2, name: "Bob", role: "Designer" },
    { id: 3, name: "Sarah", role: "Manager" },
  ];

  const filteredUsers = users.filter((user) =>
    user.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div>
      {filteredUsers.map((user) => (
        <UserCard
          key={user.id}
          name={user.name}
          role={user.role}
        />
      ))}
    </div>
  );
}

export default UserList;
```

`UserList` handles the list.

It doesn't need to know how the search input works.

It simply receives:

```js
<UserList search={search} />
```

---

## `UserCard.jsx`

```js
function UserCard({ name, role }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{role}</p>
    </div>
  );
}

export default UserCard;
```

`UserCard` has **one simple job**:

> Display one user.

That's exactly what we want from a component.

---

# 🔗 How Everything Connects

The complete flow looks like this:

```js
                         App
                          │
                    owns search state
                          │
              ┌───────────┴───────────┐
              ↓                       ↓
           Search                  UserList
              │                       │
              │                       ↓
              │                  filters users
              │                       │
              │                       ↓
              │                  UserCard
              │
              └── updates search
```

Or, more simply:

```js
App
│
├── Header
│
├── Search
│     ↑
│     │
│     └── updates App's state
│
├── UserList
│     │
│     └── UserCard
│
└── Footer
```

---

# 🧠 The 6 Things to Remember

|Concept|Remember|
|---|---|
|Props|Parent → Child|
|Callback|Child → Parent|
|Lifting State|Move shared state upward|
|Reusable Components|Build once, reuse many times|
|Composition|Build big UI from small components|
|Separate Logic/UI|Keep responsibilities clear|

---
