# 🌐 JavaScript — Essential DOM Methods

> [!summary] What is the DOM?  
> The **DOM (Document Object Model)** is JavaScript's representation of an HTML page.
> 
> JavaScript can use the DOM to:
> 
> - 🔎 Find HTML elements
>     
> - ✏️ Change content
>     
> - 🎨 Change styles/classes
>     
> - 🖱️ Respond to events
>     
> - ➕ Create and remove elements
>     
> 
> ```js
> document
> ```
> 
> is the main entry point to the DOM.

---

## 🔎 Finding Elements

### `querySelector()`

Finds the **first element** matching a CSS selector.

```js
const title = document.querySelector("h1");
```

You can use CSS selectors:

```js
document.querySelector("#title");    // ID
document.querySelector(".button");   // Class
document.querySelector("p");         // Element
```

### 🧠 Think:

> **"Give me the first element matching this selector."**

---

## 🔎 `querySelectorAll()`

Finds **all elements** matching a CSS selector.

```js
const buttons = document.querySelectorAll(".button");
```

It returns a **NodeList**.

You can loop through it:

```js
buttons.forEach(button => {
  console.log(button);
});
```

### `querySelector()` vs `querySelectorAll()`

```text
querySelector()
      ↓
   ONE element

querySelectorAll()
      ↓
  ALL matching elements
```

---

## 🆔 `getElementById()`

Finds an element by its `id`.

```html
<h1 id="title">Hello</h1>
```

```js
const title = document.getElementById("title");
```

> [!tip] Modern JavaScript  
> `querySelector("#title")` can do the same thing and is more flexible, but `getElementById()` is still very common.

---

# ✏️ Changing Content

## `textContent`

Gets or changes the text inside an element.

```js
const title = document.querySelector("h1");

title.textContent = "Hello World!";
```

HTML:

```html
<h1>Hello World!</h1>
```

> [!important] `textContent` is for **text**.  
> It doesn't interpret HTML.

---

## `innerHTML`

Gets or changes the HTML inside an element.

```js
const container = document.querySelector(".container");

container.innerHTML = "<strong>Hello!</strong>";
```

This creates:

```html
<div class="container">
  <strong>Hello!</strong>
</div>
```

> [!warning] Be careful  
> Don't put untrusted/user-provided content directly into `innerHTML`, because it can create security problems such as XSS.

---

# 🎨 Classes & Attributes

## `classList.add()`

Adds a CSS class.

```js
const button = document.querySelector("button");

button.classList.add("active");
```

---

## `classList.remove()`

Removes a class.

```js
button.classList.remove("active");
```

---

## `classList.toggle()`

Adds a class if it isn't there, and removes it if it is.

```js
button.classList.toggle("active");
```

This is extremely useful for things like menus, dark mode, and showing/hiding elements.

---

## `classList.contains()`

Checks whether an element has a class.

```js
if (button.classList.contains("active")) {
  console.log("Active!");
}
```

### 🧠 Remember

```text
add()       → ➕ Add
remove()    → ➖ Remove
toggle()    → 🔄 Add / Remove
contains()  → ❓ Check
```

---

# 🏷️ Attributes

## `getAttribute()`

Gets an HTML attribute.

```html
<a id="link" href="https://example.com">
  Website
</a>
```

```js
const link = document.querySelector("#link");

console.log(link.getAttribute("href"));
```

Output:

```text
https://example.com
```

---

## `setAttribute()`

Adds or changes an attribute.

```js
link.setAttribute("target", "_blank");
```

You can also change existing attributes:

```js
link.setAttribute("href", "https://google.com");
```

---

## `removeAttribute()`

Removes an attribute.

```js
link.removeAttribute("target");
```

---

# 🖱️ Events

## `addEventListener()`

One of the **most important DOM methods**.

It listens for an event and runs a function when that event happens.

```js
const button = document.querySelector("button");

button.addEventListener("click", () => {
  console.log("Button clicked!");
});
```

Common events:

```text
click
input
change
submit
keydown
keyup
mouseover
mouseenter
mouseleave
```

### Example

```js
button.addEventListener("click", () => {
  button.textContent = "Clicked!";
});
```

> [!tip] Think:  
> **"When this happens → do this."**

---

# ⌨️ Getting User Input

For an `<input>`:

```html
<input id="name">
```

```js
const input = document.querySelector("#name");

console.log(input.value);
```

Listen for changes:

```js
input.addEventListener("input", () => {
  console.log(input.value);
});
```

> 🧠 **.value → get the current value of form controls**

---

# ➕ Creating Elements

## `createElement()`

Creates a new HTML element.

```js
const paragraph = document.createElement("p");

paragraph.textContent = "Hello!";
```

At this point, the element exists in JavaScript but **isn't yet on the page**.

---

## `append()`

Adds an element to the end of another element.

```js
const container = document.querySelector(".container");

container.append(paragraph);
```

Now the paragraph appears inside the container.

---

## `prepend()`

Adds an element to the beginning.

```js
container.prepend(paragraph);
```

### 🧠 Remember

```text
append()  → ➡️ End
prepend() → ⬅️ Beginning
```

---

# 🗑️ Removing Elements

## `remove()`

Removes an element from the DOM.

```js
const paragraph = document.querySelector("p");

paragraph.remove();
```

Simple and very commonly used.

---

# 🔗 Navigating the DOM

Elements can access their relationships with other elements.

## `parentElement`

Gets the parent element.

```js
const button = document.querySelector("button");

console.log(button.parentElement);
```

---

## `children`

Gets the element's child elements.

```js
const list = document.querySelector("ul");

console.log(list.children);
```

---

## `firstElementChild`

Gets the first child element.

```js
console.log(list.firstElementChild);
```

---

## `lastElementChild`

Gets the last child element.

```js
console.log(list.lastElementChild);
```

---

## 🧭 DOM Navigation

```text
        parentElement
             ↑
             │
     ┌──── Element ────┐
     │                 │
     ↓                 ↓
 first child       last child
```

---

# 🎨 Changing Styles

You can directly change CSS with `.style`.

```js
const title = document.querySelector("h1");

title.style.color = "blue";
title.style.fontSize = "2rem";
```

However, for larger style changes, it's usually cleaner to use classes:

```js
title.classList.add("highlight");
```

```css
.highlight {
  color: blue;
  font-size: 2rem;
}
```

> [!tip] Prefer classes  
> Use `classList` for reusable styling and `.style` for small, dynamic changes.

---

# 📐 Useful DOM Properties

These aren't methods, but they're very useful:

```js
element.id
element.className
element.textContent
element.innerHTML
element.value
element.children
element.parentElement
```

---

# 🧩 A Real Example

HTML:

```html
<button id="add">Add item</button>

<ul id="list"></ul>
```

JavaScript:

```js
const button = document.querySelector("#add");
const list = document.querySelector("#list");

button.addEventListener("click", () => {
  const item = document.createElement("li");

  item.textContent = "New item";

  list.append(item);
});
```

Every time the button is clicked, a new `<li>` is created and added to the list.

### What's happening?

```text
querySelector()
      ↓
Find elements
      ↓
addEventListener()
      ↓
Wait for click
      ↓
createElement()
      ↓
Create <li>
      ↓
textContent
      ↓
Add text
      ↓
append()
      ↓
Put it on the page
```

---

# 🧠 Quick Reference

|Method / Property|Purpose|
|---|---|
|`querySelector()`|Find first matching element|
|`querySelectorAll()`|Find all matching elements|
|`getElementById()`|Find element by ID|
|`textContent`|Get/set text|
|`innerHTML`|Get/set HTML|
|`classList.add()`|Add class|
|`classList.remove()`|Remove class|
|`classList.toggle()`|Toggle class|
|`classList.contains()`|Check class|
|`getAttribute()`|Get attribute|
|`setAttribute()`|Set/change attribute|
|`removeAttribute()`|Remove attribute|
|`addEventListener()`|Listen for events|
|`createElement()`|Create element|
|`append()`|Add to end|
|`prepend()`|Add to beginning|
|`remove()`|Remove element|
|`parentElement`|Get parent|
|`children`|Get child elements|
|`.value`|Get form input value|
|`.style`|Change inline styles|

---

# 🎯 The Core DOM Toolkit

If you're just starting, focus on these first:

```text
🔎 Find
querySelector()
querySelectorAll()

✏️ Change
textContent
classList
setAttribute()

🖱️ Events
addEventListener()

➕ Create
createElement()
append()

🗑️ Remove
remove()

📝 Forms
value
```

> [!tip] The most important pattern

```js
const element = document.querySelector(".button");

element.addEventListener("click", () => {
  element.classList.toggle("active");
});
```

This pattern — **find → listen → change** — is at the heart of a huge amount of browser JavaScript.

### 🎯 In One Sentence

**The DOM API lets JavaScript find HTML elements, listen for events, and dynamically change the webpage.**