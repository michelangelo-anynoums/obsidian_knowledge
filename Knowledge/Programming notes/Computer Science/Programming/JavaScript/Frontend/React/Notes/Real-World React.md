# 🟣 BLOCK 14 — Real-World React

> [!abstract] 🎯 Mission Build, secure, test, and deploy a real React application — not just a UI that works on your computer.

## 🧭 01. Environment Variables

**What:** Store configuration outside your source code, such as API URLs.

```bash
# .env
VITE_API_URL=https://api.example.com
```

```jsx
const API_URL = import.meta.env.VITE_API_URL;

fetch(`${API_URL}/products`);
```

**Why:** Easily switch between development and production.

⚠️ Variables prefixed with `VITE_` are exposed to browser code. **Never put passwords, private API keys, or server secrets there.**

## 🔐 02. Authentication vs. Authorization

- **Authentication:** Who are you? → Login.
- **Authorization:** What are you allowed to do? → Permissions.

Example:

```jsx
if (!user) {
  return <Login />;
}

if (user.role !== "admin") {
  return <p>Access denied.</p>;
}

return <AdminDashboard />;
```

This illustrates the UI logic only. The **backend must enforce permissions** on every protected operation. Hiding a button is not security.

## 🌐 03. API Architecture

Separate UI, API communication, and business logic.

```jsx
React Component
      ↓
API Service
      ↓
Backend API
      ↓
Database
```

Example API service:

```jsx
const API_URL = import.meta.env.VITE_API_URL;

export async function getProducts() {
  const response = await fetch(`${API_URL}/products`);

  if (!response.ok) {
    throw new Error("Could not load products");
  }

  return response.json();
}
```

**Why:** Reuse requests and keep components clean.

## 🚨 04. Error Handling

Real applications must handle loading, success, empty, and error states.

```jsx
const [products, setProducts] = useState([]);
const [loading, setLoading] = useState(true);
const [error, setError] = useState("");

useEffect(() => {
  getProducts()
    .then(setProducts)
    .catch(() => setError("Please try again."))
    .finally(() => setLoading(false));
}, []);

if (loading) return <p>Loading...</p>;
if (error) return <p role="alert">{error}</p>;
if (!products.length) return <p>No products found.</p>;

return products.map((product) => (
  <p key={product.id}>{product.name}</p>
));
```

_Note:_ Import `useState` and `useEffect`, and define `getProducts` in your API service. Production code should also handle component unmounting and request cancellation.

## 📝 05. Form Libraries

Use **React Hook Form** for form state, validation, and submission.

```jsx
import { useForm } from "react-hook-form";

function LoginForm() {
  const { register, handleSubmit, formState: { errors } } = useForm();

  const onSubmit = (data) => {
    console.log(data.email);
    // Send credentials to your authentication API.
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label htmlFor="email">Email</label>
      <input
        id="email"
        type="email"
        {...register("email", { required: "Email is required" })}
      />

      {errors.email && <p role="alert">{errors.email.message}</p>}

      <button type="submit">Log in</button>
    </form>
  );
}
```

**Learn:** Validation, errors, submission, and server-side validation.

## ⚡ 06. Data Fetching & Caching

Use **TanStack Query (React Query)** to manage server data, caching, refetching, and loading states.

```jsx
import { useQuery } from "@tanstack/react-query";

function Products() {
  const { data, isPending, isError } = useQuery({
    queryKey: ["products"],
    queryFn: getProducts,
  });

  if (isPending) return <p>Loading...</p>;
  if (isError) return <p>Failed to load products.</p>;

  return data.map((product) => (
    <p key={product.id}>{product.name}</p>
  ));
}
```

**Key idea:** React state manages UI state; a query library manages server state and its cache.

## ♿ 07. Accessibility (a11y)

Make your application usable with keyboards, screen readers, and assistive technologies.

```jsx
<label htmlFor="search">Search products</label>
<input id="search" type="search" />

<button type="submit">Search</button>
```

**Checklist:**

- Use semantic HTML.
- Associate labels with inputs.
- Support keyboard navigation.
- Provide visible focus indicators.
- Describe meaningful images with `alt`.
- Announce important errors accessibly.

## 📱 08. Responsive UI

Build layouts that adapt to different screen sizes.

```jsx
.product-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1rem;
}

@media (max-width: 768px) {
  .product-grid {
    grid-template-columns: 1fr;
  }
}
```

**Learn:** Mobile-first design, Flexbox, Grid, breakpoints, and fluid sizing.

## 🚀 09. Deployment

Turn your local project into a publicly accessible application.

For a Vite project:

```jsx
npm run build
npm run preview
```

Then deploy the generated `dist/` folder using a static hosting service.

**Before deploying:**

- Configure production environment variables.
- Test production builds.
- Check API URLs and CORS settings.
- Configure SPA routing if needed.
- Verify error pages and accessibility.
- Never ship secrets in frontend code.

## 🌿 10. Git & Version Control

Track changes and collaborate safely.

```jsx
git init
git add .
git commit -m "feat: build product dashboard"
git switch -c feature/product-search
```

A useful commit convention:

- `feat:` New functionality
- `fix:` Bug fix
- `refactor:` Code improvement
- `docs:` Documentation
- `test:` Tests

**Habit:** Commit small, meaningful changes. Never commit `.env` files containing secrets.

---
### 🧠 Definition of Done

Your app should work beyond the happy path: invalid forms, failed requests, unauthorized access, slow connections, small screens, and production configuration.

> [!success] The real milestone You can take a React application from an empty repository to a secure, accessible, maintainable, deployed product — and explain why each architectural decision exists.

## 🔗 Suggested Learning Order

1. Environment variables + Git
2. API architecture + error handling
3. Forms + validation
4. Data fetching + caching
5. Authentication + authorization
6. Accessibility + responsive UI
7. Deployment
8. Final project and review

**Rule:** Learn each concept, implement it in the project, and commit the working result before moving on.

---
