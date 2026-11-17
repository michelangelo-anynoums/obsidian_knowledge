# 🟨 JavaScript

> [!abstract] Overview **JavaScript** is a versatile, high-level programming language used primarily for web development. Often referred to as the _language of the web_, it enables interactivity and dynamic behavior on web pages.

> [!tip] **Reference:** [JavaScript Ecosystem](https://www.youtube.com/watch?v=yMbUr5op98Y)

---

## 📦 1. Variables

One of the key features of **JavaScript** is the use of **variables**. Variables allow you to store and manage values.

You can declare variables using three keywords:

- `let` — declares a variable whose value can be reassigned.
- `const` — declares a variable that cannot be reassigned.
- `var` — the older way of declaring variables.

**Examples:**

```js
let age = 15;
const name = "Alice";
```

> [!tip] Remember Use `let` when a value may change and `const` by default when it won't need reassignment.

## ⚙️ 2. Functions

**Functions** are reusable blocks of code designed to perform specific tasks.

You can define a function using the `function` keyword:

```js
function greet() {
    console.log("Hello, world!");
}
```

To execute the function, simply call it:

```js
greet();
```

> [!info] Key concept Defining a function doesn't execute it. You must **call** it to run its code.

## 📚 3. Arrays and Objects

JavaScript provides two important data structures for organizing information.

### Arrays

An **array** is an ordered list of values.

```js
let fruits = ["apple", "banana", "cherry"];
```

You can access individual elements using their index (starting at `0`).

### Objects

An **object** stores information in **key-value pairs**.

```js
let person = {
    name: "Alice",
    age: 15
};
```

In this example:

- `"name"` and `"age"` are the **keys**.
- `"Alice"` and `15` are their corresponding **values**.

> [!example] Accessing object properties
> 
> javascript
> 
> ```
> console.log(person.name); // Alice
> console.log(person.age);  // 15
> ```

## 🔁 4. Loops

**Loops** allow you to repeat a block of code multiple times.

One of the most common loops in JavaScript is the **`for`** **loop**.

```js
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

This loop executes five times, printing the numbers `0` through `4`.

> [!note] How does it work?
> 
> - `let i = 0` → Initializes the counter.
> - `i < 5` → Defines the condition.
> - `i++` → Increases the counter by one after each iteration.

## 🖱️ 5. Events

JavaScript can handle **events**, such as mouse clicks, keyboard input, and other user interactions.

For example, you can create an event listener:

```js
document
    .getElementById("myButton")
    .addEventListener("click", function() {
        alert("Button clicked!");
    });
```

When the user clicks the button with the ID `myButton`, an alert displaying `"Button clicked!"` appears.

> [!tip] Practical use Events are essential for creating interactive websites, such as buttons, forms, menus, and pop-ups.

## ⏳ 6. Asynchronous JavaScript

JavaScript handles **asynchronous operations** using features such as:

- **Promises**
- **async/await**

For example, you can use `async/await` to fetch data from an API:

```js
async function fetchData() {
    let response = await fetch("https://api.example.com");
    let data = await response.json();

    console.log(data);
}
```

Here is what happens:

1. `async` declares an asynchronous function.
2. `fetch()` requests data from an API.
3. `await` waits for the response.
4. `response.json()` converts the response into JSON.
5. `console.log()` displays the retrieved data.

> [!important] Important `await` pauses the execution of the async function until the awaited Promise settles. It doesn't block the entire JavaScript application.

---

## 🌐 Conclusion

**JavaScript** is a powerful programming language that makes websites dynamic and interactive.

It is widely used in:

- **Front-end development** — creating interactive user interfaces.
- **Back-end development** — building server-side applications.
- **Web applications** — handling data, events, and asynchronous operations.

|Concept|Purpose|
|---|---|
|Variables|Store information|
|Functions|Reuse blocks of code|
|Arrays|Store ordered lists|
|Objects|Store key-value pairs|
|Loops|Repeat instructions|
|Events|Handle user interactions|
|Promises|Manage asynchronous operations|
|async/await|Simplify asynchronous code|

![[JavaScript_logo.png|309]]

---
