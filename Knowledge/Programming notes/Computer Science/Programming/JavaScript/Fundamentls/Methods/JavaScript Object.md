# JavaScript Object & Map Methods

## 🧱 `Object` — useful methods

```js
const user = {
  name: "Alice",
  age: 25
};
```

|Method|What it does|
|---|---|
|`Object.keys(obj)`|Get all keys|
|`Object.values(obj)`|Get all values|
|`Object.entries(obj)`|Get `[key, value]` pairs|
|`Object.fromEntries(arr)`|Convert pairs → object|
|`Object.assign(a, b)`|Copy/merge objects|
|`Object.hasOwn(obj, key)`|Check if key exists|
|`Object.create(obj)`|Create object with a prototype|
|`Object.freeze(obj)`|Prevent changes|
|`Object.seal(obj)`|Prevent adding/removing properties|

### Examples

```js
Object.keys(user);
// ["name", "age"]

Object.values(user);
// ["Alice", 25]

Object.entries(user);
// [["name", "Alice"], ["age", 25]]

Object.hasOwn(user, "name");
// true
```

---

## 🗺️ `Map` — key/value collection

```js
const users = new Map();

users.set("id", 123);
users.set("name", "Alice");
```

|Method / Property|What it does|
|---|---|
|`.set(key, value)`|Add/update a value|
|`.get(key)`|Get a value|
|`.has(key)`|Check if key exists|
|`.delete(key)`|Remove a key|
|`.clear()`|Remove everything|
|`.keys()`|Get keys|
|`.values()`|Get values|
|`.entries()`|Get key/value pairs|
|`.size`|Number of entries|

```js
users.get("name");
// "Alice"

users.has("id");
// true

users.delete("id");

users.size;
// 1
```

### Loop through a `Map`

```js
for (const [key, value] of users) {
  console.log(key, value);
}
```

---

## ⭐ Quick Memory

```text
Object
├─ keys()
├─ values()
├─ entries()
├─ fromEntries()
├─ assign()
├─ hasOwn()
├─ freeze()
└─ seal()

Map
├─ set()
├─ get()
├─ has()
├─ delete()
├─ clear()
├─ keys()
├─ values()
├─ entries()
└─ size
```

> **Object** → simple structured data  
> **Map** → key/value collection with powerful lookup methods

---

# JavaScript — Accessing Object Data

```js
const user = {
  name: "Alice",
  address: {
    city: "Madrid"
  }
};
```

## 🔑 Accessing properties

### Dot notation

```js
user.name;
// "Alice"
```

### Bracket notation

```js
user["name"];
// "Alice"
```

Useful when the property name is stored in a variable:

```js
const key = "name";

user[key];
// "Alice"
```

---

## 🛡️ Safe access — Optional Chaining `?.`

Prevents an error when something doesn't exist.

```js
user.address?.city;
// "Madrid"

user.contact?.phone;
// undefined
```

Without `?.`:

```js
user.contact.phone;
// ❌ Cannot read properties of undefined
```

### Nested data

```js
user.address?.location?.country;
// undefined
```

---

## 🎯 Safe access + Default value

Use `??` when you want a fallback.

```js
const city = user.address?.city ?? "Unknown";

console.log(city);
// "Madrid"
```

If the property doesn't exist:

```js
const phone = user.contact?.phone ?? "No phone";

console.log(phone);
// "No phone"
```

### `??` vs `||`

```js
0 ?? 10      // 0
0 || 10      // 10

"" ?? "Hi"   // ""
"" || "Hi"   // "Hi"
```

**`??`** only falls back for `null` or `undefined`.

---

## 🔍 Check if a property exists

```js
Object.hasOwn(user, "name");
// true
```

For older code:

```js
"name" in user;
// true
```

---

## ✨ Quick Cheat Sheet

```text
user.name
→ Access property

user["name"]
→ Access using a key

user?.name
→ Safely access property

user.address?.city
→ Safely access nested property

user?.name ?? "Unknown"
→ Safe access + fallback

Object.hasOwn(user, "name")
→ Check if own property exists
```

> **Rule of thumb:** Use `?.` when data might be missing, and `??` when you want a sensible default.