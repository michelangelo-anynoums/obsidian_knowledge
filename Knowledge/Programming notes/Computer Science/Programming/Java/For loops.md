# ☕ Java — For Loops

> [!abstract] Overview A `for` loop repeats a block of code a certain number of times or iterates through elements in a collection.

## 1. 🔁 Traditional `for` Loop

Use it when you know how many times you want to repeat something, or when you need control over a counter.

**Syntax**

```java
for (initialization; condition; update) {
    // Code to repeat
}
```

**Example**

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

**Output**

```java
1
2
3
4
5
```

- `int i = 1` → Initializes the counter.
- `i <= 5` → Continues while the condition is true.
- `i++` → Increases the counter by 1 after each iteration.

## 2. 📦 Enhanced `for` Loop (For-Each)

Use it to go through every element of an array or a collection without managing an index.

**Example**

```java
String[] fruits = {"Apple", "Banana", "Orange"};

for (String fruit : fruits) {
    System.out.println(fruit);
}
```

**Output**

```java
Apple
Banana
Orange
```

- `String fruit` → Holds the current element.
- `fruits` → The array being traversed.
- `:` → Means “for each element in.”

✨ **Tip:** Use this loop when you don't need the element's index.

## 3. ♾️ Infinite `for` Loop

An infinite loop continues indefinitely unless something inside it stops the loop, usually with `break`.

**Example**

```java
for (;;) {
    System.out.println("Hello!");

    break;
}
```

**Output**

```java
Hello!
```

The loop has no initialization, condition, or update expression. The `break` statement stops it after one iteration.


> [!warning] Without a stopping condition or a `break`, an infinite loop can run forever.

## 4. 🧩 Nested `for` Loop

A nested loop is a `for` loop inside another `for` loop. It's useful for grids, tables, and patterns.

**Example**

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 2; j++) {
        System.out.println(i + ", " + j);
    }
}
```

**Output**

```java
1, 1
1, 2
2, 1
2, 2
3, 1
3, 2
```

- The **outer loop** controls the rows or main repetitions.
- The **inner loop** completes all its iterations for each outer iteration.

## 5. 🎛️ `for` Loop with Multiple Variables

A traditional `for` loop can initialize or update multiple variables.

**Example**

```java
for (int i = 1, j = 5; i <= 5; i++, j--) {
    System.out.println(i + " - " + j);
}
```

**Output**

```java
1 - 5
2 - 4
3 - 3
4 - 2
5 - 1
```

Here, `i` increases while `j` decreases during each iteration.

## 🧠 Quick Summary

|Type|Best used for|
|---|---|
|Traditional `for`|Counter-based repetition|
|Enhanced `for`|Traversing arrays and collections|
|Infinite `for`|Repeating until explicitly stopped|
|Nested `for`|Grids, tables, and patterns|
|Multiple-variable `for`|Updating multiple variables together|

> [!tip] Remember - `i++` increases a variable by one. - `break` exits a loop immediately. - `continue` skips to the next iteration. - A loop's condition determines whether it continues.

**Practice idea:** Try printing the numbers from 10 down to 1, then print a small triangle of `*` characters using nested loops.

---
