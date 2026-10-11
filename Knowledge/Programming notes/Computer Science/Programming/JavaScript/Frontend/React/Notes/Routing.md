# 🟡 Block 6 — Routing

> [!abstract] Goal Build a **multi-page-feeling Single Page Application (SPA)** using React Router.

## 1. What Is Routing?

Routing allows a React application to display different pages or components based on the URL, without a full page reload.

**Example:**

- `/` → Home
- `/about` → About
- `/products` → Products
- `/products/1` → Product Details
- `/login` → Login

## 2. React Router

**React Router** is a library used to handle navigation and routing in React applications.

Install:

```js
npm install react-router-dom
```

## 3. Core Concepts

### 📍 Routes

Define which component appears for each URL.

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/products" element={<Products />} />
        <Route path="/login" element={<Login />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### 🔗 Links

Navigate between pages without reloading the entire application.

```jsx
import { Link } from "react-router-dom";

<Link to="/">Home</Link>
<Link to="/about">About</Link>
<Link to="/products">Products</Link>
```

**Remember:** Use `Link` instead of a normal `<a>` tag for internal navigation.

### 🔄 Dynamic Routes

Use dynamic routes when a page depends on a specific ID or value.

```jsx
<Route path="/products/:id" element={<ProductDetails />} />
```

Here, `:id` is a dynamic URL parameter.

### 🆔 URL Parameters

Read values from a dynamic URL using `useParams()`.

```jsx
import { useParams } from "react-router-dom";

function ProductDetails() {
  const { id } = useParams();

  return <h1>Product ID: {id}</h1>;
}
```

**Example:** `/products/42` → `id = "42"`

### 🧭 Navigation

Navigate programmatically using `useNavigate()`.

```jsx
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  return (
    <button onClick={() => navigate("/")}>
      Go Home
    </button>
  );
}
```

### 🚫 404 Pages

Display a Not Found page when the URL doesn't match any defined route.

```jsx
<Route path="*" element={<NotFound />} />
```

## 4. Route Structure

```jsx
/                  → Home
/about             → About
/products          → Products
/products/:id      → Product Details
/login             → Login
/*                 → 404 Not Found
```

## 5. Key Differences

|Concept|Purpose|
|---|---|
|`BrowserRouter`|Enables browser-based routing|
|`Routes`|Groups route definitions|
|`Route`|Maps a URL to a component|
|`Link`|Navigates through links|
|`useParams()`|Reads URL parameters|
|`useNavigate()`|Navigates through code|
|`path="*"`|Matches unmatched routes|

---
