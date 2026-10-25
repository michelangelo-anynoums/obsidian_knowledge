# 🔗 URL Query Parameters in JavaScript

> [!abstract] Overview **URL query parameters** are key-value pairs included in a URL after the `?` symbol. In JavaScript, the `URLSearchParams` API allows us to read, add, update, and remove these parameters. They are especially useful in React applications for search filters, pagination, sorting, and sharing a specific application state through a URL.

## 1. 🌐 Understanding URL Query Parameters

Consider this URL:

```jsx
https://example.com/products?category=books&sort=price&page=2
```

The part after the `?` contains the query parameters:

|Parameter|Value|
|---|---|
|`category`|`books`|
|`sort`|`price`|
|`page`|`2`|

Each parameter consists of a key and a value.

- `?` starts the query string.
- `&` separates multiple parameters.
- `=` separates a parameter's key from its value.

The query string is:

```jsx
category=books&sort=price&page=2
```

Query parameters are commonly used to represent information that should be visible in the URL, such as search terms, filters, pagination, and sorting preferences.

> [!note] Important distinction Query parameters are not the same as URL path segments. In `/products/42?sort=price`, the `42` belongs to the path, while `sort=price` is a query parameter.

## 2. 🧰 What Is `URLSearchParams`?

`URLSearchParams` is a built-in JavaScript Web API for working with URL query strings.

It provides methods to:

- Read parameter values.
- Add new parameters.
- Update existing parameters.
- Delete parameters.
- Check whether a parameter exists.
- Iterate over parameters.
- Convert parameters back into a query string.

You do not need to install a package to use it in a browser.

### Creating a `URLSearchParams` object

```jsx
const params = new URLSearchParams(
  "category=books&sort=price&page=2"
);

console.log(params.get("category")); // "books"
console.log(params.get("sort"));     // "price"
console.log(params.get("page"));     // "2"
```

Notice that the returned values are strings, including `"2"`.

`URLSearchParams` does not automatically convert values into numbers, booleans, arrays, or objects.

### Creating it from a URL

You can also create a `URL` object and access its `searchParams` property.

```jsx
const url = new URL(
  "https://example.com/products?category=books&page=2"
);

const params = url.searchParams;

console.log(params.get("category")); // "books"
console.log(params.get("page"));     // "2"
```

The `URL` object represents the full URL, while `URLSearchParams` handles the query parameters.

## 3. 📖 Reading Query Parameters

### The `.get()` method

Use `.get()` to retrieve the first value associated with a parameter name.

```jsx
const params = new URLSearchParams(
  "name=Alex&age=25"
);

const name = params.get("name");
const age = params.get("age");

console.log(name); // "Alex"
console.log(age);  // "25"
```

If the parameter does not exist, `.get()` returns `null`.

```jsx
console.log(params.get("country")); // null
```

This is useful when a parameter is optional.

```jsx
const category = params.get("category");

if (category === null) {
  console.log("No category was specified.");
}
```

### The `.has()` method

Use `.has()` to check whether a parameter exists.

```jsx
const params = new URLSearchParams(
  "category=books"
);

console.log(params.has("category")); // true
console.log(params.has("page"));     // false
```

There is a difference between a missing parameter and an empty parameter.

```jsx
const params = new URLSearchParams("search=");

console.log(params.has("search")); // true
console.log(params.get("search")); // ""
console.log(params.get("page"));   // null
```

Here, `search` exists but has an empty value. `page` does not exist.

### The `.getAll()` method

A URL can contain the same parameter more than once.

```jsx
/products?tag=react&tag=javascript&tag=css
```

Use `.getAll()` to retrieve every value associated with that key.

```jsx
const params = new URLSearchParams(
  "tag=react&tag=javascript&tag=css"
);

console.log(params.get("tag"));
// "react"

console.log(params.getAll("tag"));
// ["react", "javascript", "css"]
```

This is particularly useful for multiple filters or selected categories.

## 4. ✏️ Adding and Updating Parameters

### The `.set()` method

Use `.set()` to add a parameter or replace its existing value.

```jsx
const params = new URLSearchParams();

params.set("category", "books");
params.set("page", "2");

console.log(params.toString());
// "category=books&page=2"
```

If the parameter already exists, `.set()` replaces its value and removes any additional occurrences of that parameter.

```jsx
const params = new URLSearchParams(
  "tag=react&tag=css"
);

params.set("tag", "javascript");

console.log(params.toString());
// "tag=javascript"
```

### The `.append()` method

Use `.append()` to add another occurrence of a parameter.

```jsx
const params = new URLSearchParams();

params.append("tag", "react");
params.append("tag", "javascript");

console.log(params.toString());
// "tag=react&tag=javascript"
```

The key difference:

|Method|Behavior|
|---|---|
|`.set(key, value)`|Adds or replaces a parameter|
|`.append(key, value)`|Adds another occurrence, preserving existing values|

Choose `.set()` for parameters such as `page` or `sort`, where you usually want one value. Choose `.append()` when repeated keys are intentional.

## 5. 🗑️ Removing Parameters

Use `.delete()` to remove a parameter and all its occurrences.

```jsx
const params = new URLSearchParams(
  "category=books&page=2&sort=price"
);

params.delete("page");

console.log(params.toString());
// "category=books&sort=price"
```

This is useful when clearing a filter or returning pagination to its default state.

```jsx
params.delete("category");
```

Deleting a nonexistent parameter is safe; it does not throw an error.

## 6. 🔄 Converting Parameters to a Query String

Use `.toString()` to convert the parameters into a query string.

```jsx
const params = new URLSearchParams();

params.set("search", "react hooks");
params.set("page", "2");

console.log(params.toString());
// "search=react+hooks&page=2"
```

Notice that the space in `"react hooks"` becomes `+` in the serialized query string. This is valid form-style query encoding.

To build a full URL, use the `URL` object:

```jsx
const url = new URL("https://example.com/products");

url.searchParams.set("search", "react hooks");
url.searchParams.set("page", "2");

console.log(url.toString());
// https://example.com/products?search=react+hooks&page=2
```

This approach is generally safer and easier than manually concatenating query strings.

## 7. 🔐 Encoding and Special Characters

Query parameters may contain spaces, symbols, or characters that need encoding.

```jsx
const params = new URLSearchParams();

params.set("search", "React & JavaScript");

console.log(params.toString());
// search=React+%26+JavaScript
```

The `&` inside the value is encoded as `%26`, so it is not mistaken for a separator between parameters.

When using `URLSearchParams`, you generally do not need to call `encodeURIComponent()` on individual values before passing them to `.set()` or `.append()`.

```jsx
// ✅ Let URLSearchParams handle encoding
params.set("search", "React & JavaScript");
```

Manually encoding a value first can result in double encoding.

```jsx
// ⚠️ Avoid encoding the same value twice
params.set(
  "search",
  encodeURIComponent("React & JavaScript")
);
```

### Decoding values

When you retrieve a parameter with `.get()`, its encoded representation is decoded automatically.

```jsx
const params = new URLSearchParams(
  "search=React+%26+JavaScript"
);

console.log(params.get("search"));
// "React & JavaScript"
```

## 8. 🔢 Converting Query Values to Other Types

Query parameter values are strings. If an application needs a number or boolean, you must convert and validate the value.

### Converting to a number

```jsx
const params = new URLSearchParams("page=3");

const page = Number(params.get("page"));

console.log(page);      // 3
console.log(typeof page); // "number"
```

However, blindly converting user-provided values can introduce unexpected results.

```jsx
Number(null);   // 0
Number("abc");  // NaN
```

A safer example is:

```jsx
const params = new URLSearchParams(window.location.search);
const rawPage = params.get("page");

const parsedPage = Number(rawPage);

const page =
  rawPage !== null &&
  rawPage.trim() !== "" &&
  Number.isInteger(parsedPage) &&
  parsedPage > 0
    ? parsedPage
    : 1;
```

This defaults to page `1` if the parameter is missing or invalid.

### Converting to a boolean

A URL parameter containing `"true"` is still a string.

```jsx
const params = new URLSearchParams("darkMode=true");

const darkMode = params.get("darkMode") === "true";

console.log(darkMode); // true
```

Avoid relying on `Boolean()` for string values:

```jsx
Boolean("false"); // true
```

Non-empty strings are truthy, including the string `"false"`.

## 9. 🔍 Iterating Over Parameters

`URLSearchParams` is iterable, so you can loop through its key-value pairs.

### Using `for...of`

```jsx
const params = new URLSearchParams(
  "category=books&page=2&sort=price"
);

for (const [key, value] of params) {
  console.log(key, value);
}
```

Output:

```jsx
category books
page 2
sort price
```

### Using `.forEach()`

```jsx
params.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});
```

Notice that the callback receives the value first and the key second.

Iteration is useful when displaying active filters, debugging URLs, or processing a dynamic set of parameters.

## 10. ⚛️ Using URL Query Parameters in React

Query parameters are especially useful in React applications because they allow certain UI states to be represented in the URL.

For example:

```jsx
/products?category=books&sort=price&page=2
```

This URL describes a product page with a selected category, sorting option, and page number.

Because the state is represented in the URL, users can bookmark the page or share the link with someone else.

### Example: Reading a search query

```jsx
import { useState } from "react";

function SearchPage() {
  const [search, setSearch] = useState(() => {
    const params = new URLSearchParams(
      window.location.search
    );

    return params.get("search") ?? "";
  });

  return (
    <div>
      <input
        value={search}
        onChange={event => setSearch(event.target.value)}
        placeholder="Search..."
      />

      <p>Search term: {search}</p>
    </div>
  );
}
```

If the URL is:

```jsx
/search?search=react
```

The input initially displays `"react"`.

This example reads the query string only when the component initializes. Typing in the input changes React state but does not automatically update the URL.

### Example: Updating the URL

A basic browser-based example can update a query parameter without a full page reload.

```jsx
const url = new URL(window.location.href);

url.searchParams.set("search", "react");

window.history.pushState({}, "", url);
```

This changes the browser's URL, for example to:

```jsx
/search?search=react
```

However, calling `pushState()` does not automatically trigger a React re-render or a `popstate` event. The application must keep its own state synchronized with the URL.

For a real React application, a router is often the better solution.

### Example: React Router

React Router provides `useSearchParams()` for reading and updating query parameters.

```jsx
import { useSearchParams } from "react-router";

function ProductPage() {
  const [searchParams, setSearchParams] = useSearchParams();

  const category = searchParams.get("category") ?? "all";
  const page = Number(searchParams.get("page") ?? 1);

  function changeCategory(nextCategory) {
    setSearchParams(previousParams => {
      const nextParams = new URLSearchParams(previousParams);

      if (nextCategory === "all") {
        nextParams.delete("category");
      } else {
        nextParams.set("category", nextCategory);
      }

      nextParams.delete("page");

      return nextParams;
    });
  }

  return (
    <div>
      <p>Category: {category}</p>
      <p>Page: {page}</p>

      <button onClick={() => changeCategory("books")}>
        Show books
      </button>

      <button onClick={() => changeCategory("all")}>
        Show all products
      </button>
    </div>
  );
}
```

This example assumes the component is rendered inside a React Router application.

Changing the category updates the URL. Changing the category also removes the page parameter because the new filter should normally start at the first page.

> [!tip] Why use a router? A router helps synchronize navigation, browser history, URL parameters, and the React interface. Avoid manually managing these separately unless you have a specific reason to do so.

## 11. 🛍️ Real-World Example: Search, Filtering, and Pagination

Imagine a product listing page with these URL parameters:

```jsx
/products?search=keyboard&category=electronics&sort=price&page=2
```

Each parameter has a clear responsibility:

- `search` contains the search term.
- `category` determines the selected category.
- `sort` determines the sorting order.
- `page` determines the current page.

The application can read them like this:

```jsx
const params = new URLSearchParams(window.location.search);

const search = params.get("search") ?? "";
const category = params.get("category") ?? "all";
const sort = params.get("sort") ?? "popular";

const rawPage = Number(params.get("page"));
const page =
  Number.isInteger(rawPage) && rawPage > 0
    ? rawPage
    : 1;
```

When a user changes the sorting option, the application can update the URL while preserving other parameters.

```jsx
const url = new URL(window.location.href);

url.searchParams.set("sort", "price");
url.searchParams.delete("page");

window.history.pushState({}, "", url);
```

The resulting URL becomes:

```jsx
/products?search=keyboard&category=electronics&sort=price
```

The existing search and category filters remain intact, while the page parameter is removed.

In a router-based application, use the router's navigation or search-parameter API so that the rendered interface remains synchronized with navigation.

## 12. ⚠️ Common Mistakes

### Mistake 1: Expecting a number

```jsx
const params = new URLSearchParams("page=2");

console.log(params.get("page") + 1);
// "21"
```

The result is `"21"` because `"2"` is a string.

Convert it first:

```jsx
console.log(Number(params.get("page")) + 1);
// 3
```

### Mistake 2: Confusing `.set()` with `.append()`

```jsx
const params = new URLSearchParams("tag=react");

params.set("tag", "css");
```

The result contains only `tag=css`.

If you want both values, use `.append()` instead.

### Mistake 3: Treating a missing value as an empty string

```
const params = new URLSearchParams();

console.log(params.get("search")); // null
```

Use `??` when a default should apply only to `null` or `undefined`:

```jsx
const search = params.get("search") ?? "";
```

### Mistake 4: Assuming URL changes automatically update React

Changing `window.history` directly does not automatically synchronize React state. Use a router or explicitly manage synchronization.

### Mistake 5: Storing sensitive information in the URL

Query parameters may appear in browser history, server logs, copied links, and other places. Never use them to store passwords, access tokens, or other sensitive information.

## 13. 📌 Quick Reference

|Method or property|Purpose|Example|
|---|---|---|
|`new URLSearchParams()`|Create a query-parameter object|`new URLSearchParams("page=2")`|
|`.get(key)`|Read the first value|`params.get("page")`|
|`.getAll(key)`|Read all values for a key|`params.getAll("tag")`|
|`.has(key)`|Check whether a key exists|`params.has("page")`|
|`.set(key, value)`|Add or replace a value|`params.set("page", "3")`|
|`.append(key, value)`|Add another occurrence|`params.append("tag", "css")`|
|`.delete(key)`|Remove a parameter|`params.delete("page")`|
|`.toString()`|Serialize the query string|`params.toString()`|
|`.forEach()`|Iterate over key-value pairs|`params.forEach(...)`|
|`url.searchParams`|Access parameters on a URL object|`url.searchParams.get("page")`|

---
