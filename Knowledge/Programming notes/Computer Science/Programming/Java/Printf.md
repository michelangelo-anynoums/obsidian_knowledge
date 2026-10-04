# 🖨️ Java `printf()`

> [!summary] What is `printf()`?  
> `printf()` is used to **print formatted text** to the console.
> 
> It gives you more control over how values are displayed than `println()`.

---

## ✨ Basic Syntax

```java
System.out.printf("format", value);
```

### Example

```java
String name = "Alex";
int age = 20;

System.out.printf("My name is %s and I am %d years old.", name, age);
```

**Output:**

```text
My name is Alex and I am 20 years old.
```

---

## 🔑 Common Format Specifiers

|Specifier|Used for|Example|
|---|---|---|
|`%s`|String|`"Hello"`|
|`%d`|Integer|`25`|
|`%f`|Decimal number|`3.14`|
|`%c`|Character|`'A'`|
|`%b`|Boolean|`true`|
|`%n`|New line|—|

### Example

```java
String name = "Sam";
int age = 25;
double height = 1.75;
char grade = 'A';
boolean student = true;

System.out.printf(
    "Name: %s%nAge: %d%nHeight: %.2f%nGrade: %c%nStudent: %b%n",
    name, age, height, grade, student
);
```

**Output:**

```text
Name: Sam
Age: 25
Height: 1.75
Grade: A
Student: true
```

---

## 🎯 Controlling Decimal Places

Use `.number` before `f`.

```java
double price = 19.98765;

System.out.printf("%.2f", price);
```

**Output:**

```text
19.99
```

|Format|Result|
|---|---|
|`%.1f`|`20.0`|
|`%.2f`|`19.99`|
|`%.3f`|`19.988`|

---

## ↩️ New Lines

You can use `%n` to move to the next line.

```java
System.out.printf("Hello%nWorld");
```

**Output:**

```text
Hello
World
```

> 💡 `%n` is generally preferred over `\n` when using `printf()` because it uses the appropriate line separator for the operating system.

---

## 📐 Formatting Width

You can specify how much space a value should occupy.

```java
System.out.printf("%10s", "Java");
```

**Output:**

```text
      Java
```

The `10` means the text gets a field width of **10 characters**.

You can also left-align it:

```java
System.out.printf("%-10s", "Java");
```

**Output:**

```text
Java      
```

---

## 🧩 Multiple Values

You can insert several values into one statement.

```java
String product = "Laptop";
double price = 999.99;

System.out.printf("Product: %s | Price: $%.2f%n", product, price);
```

**Output:**

```text
Product: Laptop | Price: $999.99
```

---

## ⚖️ `print()` vs `println()` vs `printf()`

|Method|Purpose|
|---|---|
|`print()`|Prints without a new line|
|`println()`|Prints and adds a new line|
|`printf()`|Prints **formatted** text|

```java
System.out.print("Hello");
System.out.println("Hello");
System.out.printf("Hello %s", "Java");
```

---

## 🧠 Remember

> **printf() = print formatted text**

The most important specifiers to remember:

```text
%s  → String
%d  → Integer
%f  → Decimal
%c  → Character
%b  → Boolean
%n  → New line
```

### ⭐ Most common example

```java
String name = "Alex";
int age = 21;
double score = 95.5;

System.out.printf(
    "Name: %s | Age: %d | Score: %.1f%n",
    name, age, score
);
```

**Output:**

```text
Name: Alex | Age: 21 | Score: 95.5
```

---
