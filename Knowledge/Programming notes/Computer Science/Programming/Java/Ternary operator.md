# ☕ Ternary Operator in Java

> [!abstract] Definition The **ternary operator** (`?:`) is a shorthand for writing a simple `if-else` statement. It evaluates a condition and returns one of two values depending on whether the condition is `true` or `false`.

## 1. Syntax

```java
condition ? valueIfTrue : valueIfFalse;
```

- `condition` → An expression that evaluates to `true` or `false`.
- `?` → Separates the condition from the first value.
- `:` → Separates the two possible values.

## 2. Basic Example

```java
int age = 20;

String result = (age >= 18) ? "Adult" : "Minor";

System.out.println(result); // Adult
```

**How it works:**

1. Java checks whether `age >= 18`.
2. If `true`, it returns `"Adult"`.
3. If `false`, it returns `"Minor"`.

The ternary operator chooses a value and assigns it to `result`.

## 3. Equivalent `if-else` Statement

The same code can be written using `if-else`:

```java
int age = 20;
String result;

if (age >= 18) {
    result = "Adult";
} else {
    result = "Minor";
}
```

Both versions produce the same result.

**Key idea:** Use the ternary operator when you want to choose between two values based on a condition.

## 4. More Examples

**Example A — Finding the greater number**

```java
int a = 10;
int b = 25;

int max = (a > b) ? a : b;

System.out.println(max); // 25
```

**Example B — Checking a number**

```java
int number = 7;

String type = (number % 2 == 0) ? "Even" : "Odd";

System.out.println(type); // Odd
```

**Example C — Assigning a boolean**

```java
int score = 85;

boolean passed = (score >= 50) ? true : false;
```

This last example can be simplified to:

```java
boolean passed = score >= 50;
```

## 5. When Should You Use It?

✅ **Use it when:**

- The condition is simple.
- You need to choose between two values.
- You want to keep a short assignment readable.

❌ **Avoid it when:**

- The logic becomes complicated.
- You need multiple statements in each branch.
- Nested ternary operators make the code difficult to read.

## 6. Nested Ternary Operator

You can place one ternary operator inside another, but be careful with readability.

```java
int score = 75;

String grade = (score >= 90) ? "A"
             : (score >= 70) ? "B"
             : (score >= 50) ? "C"
             : "F";

System.out.println(grade); // B
```

For more complex logic, an `if-else-if` statement is often easier to understand.

## 🧠 Quick Recap

- **Operator:** `?:`
- **Purpose:** Choose one of two values based on a condition.
- **?** separates the condition from the true result.
- **:** separates the true result from the false result.
- **Result:** The ternary expression evaluates to one of the two values.
- **Best practice:** Prefer readability over shorter code.

> [!tip] Remember Think of the ternary operator as a compact question: **Condition true? → First value : Otherwise → Second value**


---
