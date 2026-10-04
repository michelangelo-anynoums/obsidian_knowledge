# CSS Flexbox

> [!summary] What is Flexbox?  
> **Flexbox** (Flexible Box Layout) is a CSS layout system for arranging elements in a **row or a column**.
> 
> It is especially useful for navigation bars, buttons, cards, menus, and aligning items.

---

## 1. The Basic Idea

Think of Flexbox like a flexible row or column:

```text
┌─────────┬─────────┬─────────┐
│  Item 1 │  Item 2 │  Item 3 │
└─────────┴─────────┴─────────┘
```

The **container** becomes a flex container, and its direct children become **flex items**.

### HTML

```html
<div class="container">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

### CSS

```css
.container {
  display: flex;
}
```

That's it — Flexbox is now active.

By default, the items are placed in a **row**.

---

## 2. `flex-direction`

The `flex-direction` property controls the direction of the items.

### Row — default

```css
.container {
  display: flex;
  flex-direction: row;
}
```

Result:

```text
┌───────┐ ┌───────┐ ┌───────┐
│ Item 1│ │ Item 2│ │ Item 3│
└───────┘ └───────┘ └───────┘
```

### Column

```css
.container {
  display: flex;
  flex-direction: column;
}
```

Result:

```text
┌─────────┐
│  Item 1 │
├─────────┤
│  Item 2 │
├─────────┤
│  Item 3 │
└─────────┘
```

> [!tip] Remember  
> `row` → left to right
> 
> `column` → top to bottom

---

## 3. `justify-content`

This controls how items are distributed along the **main axis**.

For a normal row, the main axis is horizontal.

### Center

```css
.container {
  display: flex;
  justify-content: center;
}
```

```text
┌──────────────────────────────┐
│      Item 1  Item 2  Item 3  │
└──────────────────────────────┘
```

### Space between

```css
.container {
  justify-content: space-between;
}
```

```text
┌──────────────────────────────┐
│ Item 1       Item 2     Item 3│
└──────────────────────────────┘
```

### Other useful values

```css
justify-content: flex-start;
justify-content: flex-end;
justify-content: center;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

> [!tip] Easy way to remember  
> `justify-content` controls **distribution along the main axis**.

---

## 4. `align-items`

This controls alignment along the **cross axis**.

With a row, this usually means vertical alignment.

```css
.container {
  display: flex;
  align-items: center;
}
```

For example:

```text
┌──────────────────────────────┐
│                              │
│   Item 1   Item 2   Item 3   │
│                              │
└──────────────────────────────┘
```

Useful values include:

```css
align-items: flex-start;
align-items: flex-end;
align-items: center;
align-items: stretch;
```

---

## 5. The Easy Centering Trick

One of the most useful Flexbox patterns is:

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

This centers an item **horizontally and vertically**.

For example:

```text
┌──────────────────────────────┐
│                              │
│                              │
│          Hello!              │
│                              │
│                              │
└──────────────────────────────┘
```

> [!success] Remember  
> `justify-content` + `align-items`
> 
> = a very easy way to center things.

---

## 6. `gap`

Just like Grid, Flexbox has a `gap` property.

```css
.container {
  display: flex;
  gap: 20px;
}
```

This adds 20px of space between the items.

```text
┌───────┐    ┌───────┐    ┌───────┐
│ Item 1│    │ Item 2│    │ Item 3│
└───────┘    └───────┘    └───────┘
     ↑            ↑
    20px         20px
```

You can also use:

```css
row-gap: 10px;
column-gap: 20px;
```

---

## 7. `flex-wrap`

By default, Flexbox tries to keep everything on one line.

`flex-wrap` allows items to move onto another line when necessary.

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
```

For example:

```text
┌──────┬──────┬──────┐
│ Item │ Item │ Item │
├──────┼──────┼──────┤
│ Item │ Item │ Item │
└──────┴──────┴──────┘
```

This is very useful for responsive designs.

> [!tip]  
> `flex-wrap: wrap` means:
> 
> **"If there isn't enough space, move items to the next line."**

---

## 8. `flex-grow`

`flex-grow` controls how much an item can grow to fill available space.

```css
.item {
  flex-grow: 1;
}
```

If several items have:

```css
.item {
  flex-grow: 1;
}
```

they will share the available space.

```text
┌──────────┬──────────┬──────────┐
│  Item 1  │  Item 2  │  Item 3  │
└──────────┴──────────┴──────────┘
```

You can give one item more space:

```css
.item1 {
  flex-grow: 2;
}

.item2 {
  flex-grow: 1;
}
```

The first item gets twice the available growth.

---

## 9. `flex-shrink`

`flex-shrink` controls how an item shrinks when there isn't enough space.

```css
.item {
  flex-shrink: 1;
}
```

The default is:

```css
flex-shrink: 1;
```

You can prevent an item from shrinking:

```css
.item {
  flex-shrink: 0;
}
```

---

## 10. The `flex` Shorthand

Instead of writing:

```css
flex-grow: 1;
flex-shrink: 1;
flex-basis: 0;
```

you can use:

```css
flex: 1;
```

This is extremely common.

For example:

```css
.container {
  display: flex;
}

.item {
  flex: 1;
}
```

The items will share the available space.

```text
┌──────────┬──────────┬──────────┐
│  Item 1  │  Item 2  │  Item 3  │
└──────────┴──────────┴──────────┘
```

---

## 11. `flex-basis`

`flex-basis` defines the initial size of an item before the remaining space is distributed.

```css
.item {
  flex-basis: 200px;
}
```

Think of it as:

> **"Start this item at approximately 200px."**

For example:

```css
.container {
  display: flex;
}

.item {
  flex-basis: 200px;
}
```

---

## 12. Changing the Order

You can change the visual order of individual items.

```css
.item1 {
  order: 3;
}

.item2 {
  order: 1;
}

.item3 {
  order: 2;
}
```

The HTML order doesn't change, but the visual order does.

> [!warning] Be careful  
> Don't use `order` unnecessarily, especially for important content, because visual order can differ from the logical/HTML order.

---

## 13. Aligning One Item

`align-self` lets you override the alignment of a particular item.

```css
.item2 {
  align-self: flex-end;
}
```

For example:

```text
┌──────────────────────────────┐
│                              │
│ Item 1   Item 3              │
│                              │
│             Item 2           │
└──────────────────────────────┘
```

Useful values include:

```css
align-self: flex-start;
align-self: center;
align-self: flex-end;
align-self: stretch;
```

---

## 14. A Simple Navigation Bar

Flexbox is perfect for navigation menus.

### HTML

```html
<nav class="navbar">
  <div class="logo">My Site</div>

  <div class="links">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </div>
</nav>
```

### CSS

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.links {
  display: flex;
  gap: 20px;
}
```

Result:

```text
┌─────────────────────────────────────┐
│ My Site       Home  About  Contact  │
└─────────────────────────────────────┘
```

This is one of the most common real-world uses of Flexbox.

---

## 15. Responsive Cards

Flexbox can also create a row of cards.

### HTML

```html
<div class="cards">
  <div class="card">HTML</div>
  <div class="card">CSS</div>
  <div class="card">JavaScript</div>
</div>
```

### CSS

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 200px;
  padding: 30px;
  background: #eeeeee;
  border-radius: 10px;
}
```

The important part is:

```css
flex: 1 1 200px;
```

This means:

```text
grow   shrink   basis
  ↓       ↓       ↓
  1       1      200px
```

The cards can grow, shrink, and start at around 200px.

---

## 16. Flexbox vs Grid

A simple way to remember the difference:

|Flexbox|Grid|
|---|---|
|One-dimensional|Two-dimensional|
|Row **or** column|Rows **and** columns|
|Great for components|Great for page layouts|
|Navigation bars|Complete page structures|
|Buttons and menus|Galleries and dashboards|
|Easy alignment|Precise layout control|

### Think:

**Flexbox → arrange things**

**Grid → design the layout**

They can also work together.

For example, use Grid for the overall page and Flexbox inside individual cards.

---

## 17. Main Axis vs Cross Axis

This is one of the most important Flexbox concepts.

With:

```css
flex-direction: row;
```

```text
Main axis ──────────────────────→

┌──────────────────────────────┐
│  Item 1   Item 2   Item 3    │
└──────────────────────────────┘
              ↑
         Cross axis
```

With:

```css
flex-direction: column;
```

the axes switch:

```text
       Main axis
           ↓
      ┌─────────┐
      │ Item 1  │
      │ Item 2  │
      │ Item 3  │
      └─────────┘
           →
       Cross axis
```

> [!important] The key idea  
> `justify-content` works along the **main axis**.
> 
> `align-items` works along the **cross axis**.

---

## 18. Useful Flexbox Properties

### Container properties

```css
display: flex;

flex-direction:
flex-wrap:

justify-content:
align-items:
align-content:

gap:
row-gap:
column-gap:
```

### Item properties

```css
flex:
flex-grow:
flex-shrink:
flex-basis:

order:
align-self:
```

---

## 19. Complete Mini Example

### HTML

```html
<div class="container">
  <div class="card">HTML</div>
  <div class="card">CSS</div>
  <div class="card">JavaScript</div>
</div>
```

### CSS

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 200px;
  padding: 30px;
  background: #eeeeee;
  border-radius: 10px;
  text-align: center;
}
```

Result:

```text
┌─────────────┬─────────────┬─────────────┐
│    HTML     │     CSS     │ JavaScript  │
└─────────────┴─────────────┴─────────────┘
```

On a smaller screen, the cards can wrap:

```text
┌─────────────┬─────────────┐
│    HTML     │     CSS     │
├─────────────┴─────────────┤
│         JavaScript        │
└────────────────────────────┘
```

---

## 🧠 Quick Cheat Sheet

```css
/* Turn on Flexbox */
display: flex;

/* Direction */
flex-direction: row;
flex-direction: column;

/* Main-axis alignment */
justify-content: center;
justify-content: space-between;

/* Cross-axis alignment */
align-items: center;

/* Allow items to wrap */
flex-wrap: wrap;

/* Space between items */
gap: 20px;

/* Let an item grow */
flex-grow: 1;

/* Let an item shrink */
flex-shrink: 1;

/* Flexible shorthand */
flex: 1;

/* Change visual order */
order: 2;

/* Align one specific item */
align-self: center;
```

---

## 🎯 The 5 Things to Learn First

If you're just starting with Flexbox, don't try to memorize everything.

Learn these five first:

### 1. `display: flex`

Turns Flexbox on.

### 2. `flex-direction`

Decides between:

```css
row
```

and

```css
column
```

### 3. `justify-content`

Controls distribution along the **main axis**.

### 4. `align-items`

Controls alignment along the **cross axis**.

### 5. `gap`

Adds space between items.

Once these make sense, you already understand the foundation of Flexbox.

> [!success] The main idea  
> **Flexbox = a flexible way to arrange items in one direction.**
> 
> Start with:
> 
> `display: flex`
> 
> then think about:
> 
> **Direction → Alignment → Spacing**
> 
> ```text
> display: flex
>       ↓
> flex-direction
>       ↓
> justify-content + align-items
>       ↓
> gap
> ```
> 
> Master these concepts first, and properties such as `flex-grow`, `flex-shrink`, and `flex-basis` will become much easier to understand.