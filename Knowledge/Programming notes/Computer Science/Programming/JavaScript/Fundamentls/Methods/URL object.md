# 🔗 JavaScript — URL Object

> [!abstract] Overview The **URL** **object** in JavaScript is used to create, read, modify, and work with URLs (Uniform Resource Locators). It makes it easy to access parts of a URL, such as the protocol, hostname, pathname, and query parameters.

## 1. Creating a URL

Use `new URL()` to create a URL object.

```js
// Create a URL
const url = new URL("https://example.com/products?id=25");

console.log(url);
```

You can also create a URL relative to a base URL.

```js
const url = new URL(
  "/about",
  "https://example.com"
);

console.log(url.href);
// "https://example.com/about"
```

> [!tip] Remember A relative URL needs a **base URL** to determine the complete address.

## 2. Getting URL Information

A URL object provides properties to access different parts of a URL.

```js
const url = new URL(
  "https://example.com:8080/products?id=25#details"
);

console.log(url.href);      // Complete URL
console.log(url.origin);    // Protocol + hostname + port
console.log(url.protocol);  // "https:"
console.log(url.hostname);  // "example.com"
console.log(url.port);      // "8080"
console.log(url.host);      // "example.com:8080"
console.log(url.pathname);  // "/products"
console.log(url.search);    // "?id=25"
console.log(url.hash);      // "#details"
```

> [!info] Important difference - `hostname` contains the domain name. - `host` contains the domain name and port, if present. - `origin` contains the scheme, hostname, and port, where applicable.

## 3. Working with Query Parameters

Query parameters are the key-value pairs that appear after `?` in a URL.

Example:

```js
https://example.com/products?id=25&category=books
```

Use `searchParams` to read them.

```js
const url = new URL(
  "https://example.com/products?id=25&category=books"
);

console.log(url.searchParams.get("id"));
// "25"

console.log(url.searchParams.get("category"));
// "books"

console.log(url.searchParams.has("id"));
// true
```

> [!tip] Remember Query parameter values are returned as **strings**, even when they look like numbers.

## 4. Adding and Modifying Parameters

Use `searchParams.set()` to add or update a parameter.

```js
const url = new URL("https://example.com/products");

url.searchParams.set("id", "25");
url.searchParams.set("category", "books");

console.log(url.href);
// "https://example.com/products?id=25&category=books"
```

Use `append()` to add another value, even if the parameter already exists.

```js
url.searchParams.append("tag", "javascript");
url.searchParams.append("tag", "web");

console.log(url.searchParams.getAll("tag"));
// ["javascript", "web"]
```

Use `delete()` to remove a parameter.

```js
url.searchParams.delete("category");
```

## 5. Modifying URL Properties

URL properties can be changed directly.

```js
const url = new URL("https://example.com/products");

url.hostname = "shop.example.com";
url.pathname = "/cart";
url.hash = "checkout";

console.log(url.href);
// "https://shop.example.com/cart#checkout"
```

> [!warning] Be careful Changing one property may affect the complete URL. Always inspect `url.href` if you need to verify the final result.

## 6. Converting a URL to a String

Use `href` or `toString()` to get the complete URL as a string.

```js
const url = new URL("https://example.com/about");

console.log(url.href);
console.log(url.toString());
```

Both return the complete serialized URL.

You can also use:

```js
console.log(url.toJSON());
```

`toJSON()` returns the URL as a string, which can be useful when serializing objects to JSON.

## 7. Checking Whether a URL Is Valid

The URL constructor throws a `TypeError` if the input cannot be parsed as a valid URL.

```js
try {
  const url = new URL("https://example.com");

  console.log("Valid URL:", url.href);
} catch (error) {
  console.log("Invalid URL");
}
```

For relative URLs, provide a base URL.

```js
const url = new URL("/about", "https://example.com");
```

> [!note] Important A successfully parsed URL is not necessarily a reachable website. Parsing checks the URL's structure, not whether the server exists or responds.

## 8. URL vs. URLSearchParams

These two APIs are related but have different purposes.

```js
const url = new URL(
  "https://example.com/products?id=25"
);

const params = new URLSearchParams("id=25&sort=price");
```

- **URL** works with the complete address and its components.
- **URLSearchParams** works specifically with query parameters.

Example:

```js
params.set("page", "2");

console.log(params.toString());
// "id=25&sort=price&page=2"
```

## 9. Important Things to Remember

- Use `new URL()` to create a URL object.
- Use `href` to get the complete URL.
- Use `pathname` to access the path.
- Use `searchParams` to read, add, update, or delete query parameters.
- Use `try...catch` to handle invalid URLs.
- Provide a base URL when working with relative addresses.
- Query parameters may contain repeated keys.
- URL objects are available in modern browsers and many JavaScript runtimes, including Node.js.

## 10. Quick Reference

|Property / Method|Purpose|
|---|---|
|`new URL()`|Create a URL object|
|`href`|Get the complete URL|
|`origin`|Get the origin|
|`protocol`|Get the scheme|
|`hostname`|Get the domain name|
|`port`|Get the port|
|`pathname`|Get the path|
|`search`|Get the query string|
|`hash`|Get the fragment|
|`searchParams.get()`|Read a parameter|
|`searchParams.set()`|Add or update a parameter|
|`searchParams.append()`|Add another parameter value|
|`searchParams.delete()`|Remove a parameter|
|`toString()`|Convert the URL to a string|

---
