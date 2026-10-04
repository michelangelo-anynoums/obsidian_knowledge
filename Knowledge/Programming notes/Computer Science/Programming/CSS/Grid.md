# CSS3 Grid

> [!summary] What is CSS Grid?  
> **CSS Grid** is a CSS layout system for arranging elements in **rows and columns**.
> 
> It is especially useful for creating page layouts, cards, galleries, dashboards, and responsive designs.

---

## 1. The Basic Idea

Think of Grid like a table:

```text
┌─────────┬─────────┬─────────┐
│ Item 1  │ Item 2  │ Item 3  │
├─────────┼─────────┼─────────┤
│ Item 4  │ Item 5  │ Item 6  │
└─────────┴─────────┴─────────┘
```

The **container** becomes the grid, and its direct children become **grid items**.

### HTML

```html
<div class="container">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
</div>
```

### CSS

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

`display: grid` activates Grid.

`grid-template-columns` creates three columns.

`1fr` means **one fraction of the available space**.

`gap` adds space between the items.

---

## 2. Creating Columns

The most important Grid property is:

```css
grid-template-columns
```

### Three equal columns

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

Or, more conveniently:

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

### Different column sizes

```css
.container {
  display: grid;
  grid-template-columns: 2fr 1fr;
}
```

This creates:

```text
┌───────────────────┬─────────┐
│                   │         │
│      2 parts      │ 1 part  │
│                   │         │
└───────────────────┴─────────┘
```

---

## 3. Creating Rows

Use:

```css
grid-template-rows
```

Example:

```css
.container {
  display: grid;
  grid-template-rows: 100px 200px;
}
```

This creates two rows:

- First row → `100px`
    
- Second row → `200px`
    

You can also use flexible units:

```css
grid-template-rows: 1fr 2fr;
```

---

## 4. The `gap` Property

`gap` controls the space between grid items.

```css
.container {
  display: grid;
  gap: 20px;
}
```

You can control rows and columns separately:

```css
.container {
  row-gap: 10px;
  column-gap: 20px;
}
```

Or use the shorthand:

```css
gap: 10px 20px;
```

The first value is the **row gap**.

The second value is the **column gap**.

---

## 5. The `fr` Unit

`fr` means **fraction of the available space**.

For example:

```css
grid-template-columns: 1fr 1fr;
```

Both columns get 50%.

```css
grid-template-columns: 1fr 2fr;
```

The second column gets twice as much space.

```text
┌────────────┬──────────────────────┐
│    1fr     │         2fr          │
└────────────┴──────────────────────┘
```

> [!tip] Remember  
> `1fr 1fr 1fr` = three equal columns.

---

## 6. Placing Items

You can control where an item starts and ends.

```css
.item {
  grid-column: 1 / 3;
}
```

This makes the item span from column line 1 to column line 3.

For example:

```text
┌──────────────────────────────┐
│           Item 1             │
├──────────────┬───────────────┤
│    Item 2    │    Item 3     │
└──────────────┴───────────────┘
```

### Spanning two columns

An easier way is:

```css
.item {
  grid-column: span 2;
}
```

Similarly, you can span rows:

```css
.item {
  grid-row: span 2;
}
```

---

## 7. A Simple Website Layout

Grid is excellent for page layouts.

```html
<div class="page">
  <header>Header</header>
  <aside>Sidebar</aside>
  <main>Main Content</main>
  <footer>Footer</footer>
</div>
```

```css
.page {
  display: grid;

  grid-template-columns: 200px 1fr;

  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
}

header {
  grid-area: header;
}

aside {
  grid-area: sidebar;
}

main {
  grid-area: main;
}

footer {
  grid-area: footer;
}
```

The result is roughly:

```text
┌──────────────────────────────┐
│            Header            │
├────────────┬─────────────────┤
│  Sidebar   │   Main Content  │
│            │                 │
├────────────┴─────────────────┤
│            Footer            │
└──────────────────────────────┘
```

> [!tip] `grid-template-areas`  
> This is one of the easiest ways to understand and create a website layout because the CSS visually describes the page structure.

---

## 8. Responsive Grid

Grid works very well with responsive designs.

A useful pattern is:

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}
```

This means:

- Each column should be at least `200px`.
    
- Columns can grow to fill available space.
    
- The number of columns automatically changes depending on screen size.
    

For example:

```text
Desktop:

┌──────┬──────┬──────┬──────┐
│ Card │ Card │ Card │ Card │
└──────┴──────┴──────┴──────┘


Smaller screen:

┌──────────┬──────────┐
│   Card   │   Card   │
├──────────┼──────────┤
│   Card   │   Card   │
└──────────┴──────────┘


Mobile:

┌──────────────┐
│     Card     │
├──────────────┤
│     Card     │
├──────────────┤
│     Card     │
└──────────────┘
```

---

## 9. Alignment

Grid provides several useful alignment properties.

### `justify-items`

Controls horizontal alignment of items.

```css
.container {
  justify-items: center;
}
```

### `align-items`

Controls vertical alignment.

```css
.container {
  align-items: center;
}
```

### Center everything

```css
.container {
  display: grid;
  place-items: center;
}
```

This is a very handy shortcut.

---

## 10. Grid vs Flexbox

A simple way to remember the difference:

|Grid|Flexbox|
|---|---|
|Two-dimensional|One-dimensional|
|Rows **and** columns|Row **or** column|
|Great for page layouts|Great for components|
|Great for galleries|Great for navigation bars|

### Think:

**Grid → layout**

**Flexbox → alignment**

They can also be used together.

For example, Grid can create the overall page layout while Flexbox aligns the buttons inside a card.

---

## 11. Useful Grid Properties

### Container properties

```css
display: grid;

grid-template-columns:
grid-template-rows:

gap:
row-gap:
column-gap:

grid-template-areas:

justify-items:
align-items:
place-items:

justify-content:
align-content:
```

### Item properties

```css
grid-column:
grid-row:
grid-area:
```

---

## 12. Complete Mini Example

### HTML

```html
<div class="cards">
  <div class="card">HTML</div>
  <div class="card">CSS</div>
  <div class="card">JavaScript</div>
  <div class="card">React</div>
</div>
```

### CSS

```css
.cards {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.card {
  padding: 30px;
  background: #eeeeee;
  border-radius: 10px;
  text-align: center;
}
```

Result:

```text
┌─────────────┬─────────────┐
│    HTML     │     CSS     │
├─────────────┼─────────────┤
│ JavaScript  │    React    │
└─────────────┴─────────────┘
```

---

## 🧠 Quick Cheat Sheet

```css
/* Turn on Grid */
display: grid;

/* Create columns */
grid-template-columns: repeat(3, 1fr);

/* Create rows */
grid-template-rows: 100px 200px;

/* Space between items */
gap: 20px;

/* Make an item span 2 columns */
grid-column: span 2;

/* Make an item span 2 rows */
grid-row: span 2;

/* Center items */
place-items: center;

/* Responsive columns */
grid-template-columns:
  repeat(auto-fit, minmax(200px, 1fr));
```

> [!success] The main idea  
> **CSS Grid = rows + columns + control.**
> 
> Start with:
> 
> `display: grid`
> 
> then define your columns with:
> 
> `grid-template-columns`
> 
> and add spacing with:
> 
> `gap`
> 
> Once these three ideas are comfortable, most basic Grid layouts become much easier to understand.

---
