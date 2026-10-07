# JavaScript — HTML Table DOM Methods

The DOM provides special methods for working with HTML `<table>` elements.

## 🧱 Basic Table Structure

```html
<table id="users">
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Alice</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
```

---

## 🎯 Get the Table

```js
const table = document.querySelector("#users");
```

Or:

```js
const table = document.getElementById("users");
```

---

## 📋 Useful Table Properties

|Property|Returns|
|---|---|
|`table.rows`|All `<tr>` elements|
|`table.tHead`|`<thead>` element|
|`table.tBodies`|All `<tbody>` elements|
|`table.tFoot`|`<tfoot>` element|

```js
table.rows;
// HTMLCollection of all rows
```

---

## ➕ Create Rows & Cells

### `insertRow()`

Creates a new table row.

```js
const row = table.insertRow();
```

### `insertCell()`

Creates a cell inside a row.

```js
const cell = row.insertCell();
cell.textContent = "Alice";
```

Together:

```js
const row = table.insertRow();
const cell = row.insertCell();

cell.textContent = "Alice";
```

---

## 🗑️ Delete Rows

### `deleteRow()`

```js
table.deleteRow(0);
```

Deletes the row at index `0`.

```js
table.deleteRow(-1);
```

Useful for removing the last row in some DOM implementations, but for clarity you can use:

```js
table.deleteRow(table.rows.length - 1);
```

---

## 🔎 Access Individual Rows & Cells

```js
const row = table.rows[0];

const cell = row.cells[1];

console.log(cell.textContent);
```

### Useful properties

```js
row.cells
row.rowIndex
row.sectionRowIndex

cell.cellIndex
cell.textContent
```

---

## 🧩 `sectionRowIndex`

For rows inside `<thead>`, `<tbody>`, or `<tfoot>`:

```js
const tbody = table.tBodies[0];
const row = tbody.rows[0];

console.log(row.sectionRowIndex);
// 0
```

---

## 🛡️ Safe Access

If the table or row might not exist:

```js
const table = document.querySelector("#users");

const cell = table?.rows[0]?.cells[1];

console.log(cell?.textContent);
```

Using `?.` prevents errors when something is missing.

---

## ⚡ Quick Cheat Sheet

```text
TABLE
│
├─ table.rows
├─ table.tHead
├─ table.tBodies
├─ table.tFoot
│
├─ table.insertRow()
├─ table.deleteRow(index)
│
└─ row
   ├─ row.cells
   ├─ row.insertCell()
   ├─ row.deleteCell()
   ├─ row.rowIndex
   └─ row.sectionRowIndex
```

### ⭐ Most Useful

```js
table.rows[0]
row.cells[0]

table.insertRow()
row.insertCell()

table.deleteRow(0)
row.deleteCell(0)

cell.textContent
```

> **Think:** `table → row → cell`  
> **Access:** `table.rows → row.cells → cell`