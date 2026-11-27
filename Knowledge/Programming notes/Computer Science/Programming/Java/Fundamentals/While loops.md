# 🔁 While & Do-While Loops in Java

> [!abstract] What are they? Both loops repeat a block of code while a condition is `true`. - `while` checks the condition **before** executing the code. - `do-while` checks the condition **after** executing the code.

## 1. 🔄 While Loop

### Syntax

```Java
while (condition) {
    // Code to repeat
}
```

### Example

```Java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

**Output:**

```Java
1
2
3
4
5
```

### ⚙️ How it works

1. Check if `i <= 5`.
2. Execute the code if the condition is `true`.
3. Increase `i` by one using `i++`.
4. Repeat until the condition becomes `false`.

> [!tip] Remember A `while` loop can execute **zero times** if the condition is initially `false`.

---

## 2. 🔁 Do-While Loop

### Syntax

```Java
do {
    // Code to repeat
} while (condition);
```

Notice the **semicolon (****`;`****)** at the end!

### Example

```Java
int i = 1;

do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

**Output:**

```Java
1
2
3
4
5
```

### ⚙️ How it works

1. Execute the code inside `do`.
2. Increase `i` by one.
3. Check if `i <= 5`.
4. Repeat if the condition is `true`.

> [!tip] Remember A `do-while` loop always executes **at least once**, because the condition is checked at the end.

---

## 3. ⚖️ Key Differences

|Feature|`while`|`do-while`|
|---|---|---|
|Condition checked|Before|After|
|Minimum executions|0|1|
|Semicolon after condition|No|Yes|
|Best for|Checking before acting|Acting at least once|

---
