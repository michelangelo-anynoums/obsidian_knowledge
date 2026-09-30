# Java Integer Object Methods

`Integer` is a **wrapper class** in Java for the primitive `int`.

```java
int number = 10;
Integer obj = 10;
```

## Essential Methods

|Method|What it does|Example|Result|
|---|---|---|---|
|`parseInt()`|String → `int`|`Integer.parseInt("10")`|`10`|
|`valueOf()`|String/int → `Integer`|`Integer.valueOf("10")`|`10`|
|`toString()`|Integer → String|`number.toString()`|`"10"`|
|`compare()`|Compares two integers|`Integer.compare(10, 20)`|Negative|
|`max()`|Finds the larger number|`Integer.max(10, 20)`|`20`|
|`min()`|Finds the smaller number|`Integer.min(10, 20)`|`10`|
|`sum()`|Adds two integers|`Integer.sum(10, 20)`|`30`|
|`intValue()`|`Integer` → `int`|`number.intValue()`|`10`|

## 1. `parseInt()`

Converts a `String` into a primitive `int`.

```java
int number = Integer.parseInt("123");
```

---

## 2. `valueOf()`

Converts a `String` or `int` into an `Integer` object.

```java
Integer number = Integer.valueOf("123");
```

### Difference

```java
int a = Integer.parseInt("10");     // int
Integer b = Integer.valueOf("10");  // Integer
```

---

## 3. `toString()`

Converts an `Integer` into a `String`.

```java
Integer number = 123;
String text = number.toString();
```

---

## 4. `compare()`

Compares two integers.

```java
Integer.compare(10, 20);
```

- Negative → first number is smaller
    
- `0` → numbers are equal
    
- Positive → first number is bigger
    

---

## 5. `max()`

Returns the larger number.

```java
Integer.max(10, 20); // 20
```

---

## 6. `min()`

Returns the smaller number.

```java
Integer.min(10, 20); // 10
```

---

## 7. `sum()`

Adds two integers.

```java
Integer.sum(10, 20); // 30
```

---

## 8. `intValue()`

Converts an `Integer` object into a primitive `int`.

```java
Integer number = 100;

int value = number.intValue();
```

In modern Java, this can usually happen automatically:

```java
Integer number = 100;
int value = number; // unboxing
```

## Useful Constants

|Constant|Meaning|Value|
|---|---|---|
|`Integer.MAX_VALUE`|Largest possible `int`|`2147483647`|
|`Integer.MIN_VALUE`|Smallest possible `int`|`-2147483648`|

## Quick Reminder

```text
parseInt()   → String → int
valueOf()    → String/int → Integer
toString()   → Integer → String
compare()    → Compare two integers
max()        → Larger number
min()        → Smaller number
sum()        → Add two numbers
intValue()   → Integer → int
```