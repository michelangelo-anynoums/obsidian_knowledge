# Java String Methods

A `String` in Java is used to store text.

```java
String name = "Alice";
```

## Common String Methods

|Method|What it does|Example|
|---|---|---|
|`length()`|Returns the number of characters|`"Hello".length()` → `5`|
|`charAt()`|Gets a character at a position|`"Hello".charAt(1)` → `'e'`|
|`toUpperCase()`|Converts text to uppercase|`"hello".toUpperCase()` → `"HELLO"`|
|`toLowerCase()`|Converts text to lowercase|`"HELLO".toLowerCase()` → `"hello"`|
|`equals()`|Compares two strings|`"Hi".equals("Hi")` → `true`|
|`equalsIgnoreCase()`|Compares strings ignoring case|`"hi".equalsIgnoreCase("HI")` → `true`|
|`contains()`|Checks if text contains something|`"Hello".contains("ell")` → `true`|
|`startsWith()`|Checks the beginning of a string|`"Hello".startsWith("He")` → `true`|
|`endsWith()`|Checks the end of a string|`"Hello".endsWith("lo")` → `true`|
|`indexOf()`|Finds the position of text|`"Hello".indexOf("l")` → `2`|
|`substring()`|Extracts part of a string|`"Hello".substring(1, 4)` → `"ell"`|
|`replace()`|Replaces characters/text|`"Hello".replace("H", "J")` → `"Jello"`|
|`trim()`|Removes spaces at the beginning/end|`" Hi ".trim()` → `"Hi"`|
|`isEmpty()`|Checks if the string has no characters|`"".isEmpty()` → `true`|

## Example

```java
String text = "Hello World";

System.out.println(text.length());        // 11
System.out.println(text.toUpperCase());   // HELLO WORLD
System.out.println(text.toLowerCase());   // hello world
System.out.println(text.contains("World")); // true
System.out.println(text.charAt(0));       // H
System.out.println(text.substring(0, 5)); // Hello
```

## Important: Comparing Strings

Use `.equals()` to compare the **contents** of strings.

```java
String a = "Hello";
String b = "Hello";

System.out.println(a.equals(b)); // true
```

Avoid using `==` when you want to compare string contents:

```java
a == b
```

`==` checks whether two references point to the same object, while `.equals()` checks the string's contents.

## Quick Memory Tip

- **Size:** `length()`
    
- **Character:** `charAt()`
    
- **Change case:** `toUpperCase()`, `toLowerCase()`
    
- **Compare:** `equals()`
    
- **Search:** `contains()`, `indexOf()`
    
- **Extract:** `substring()`
    
- **Replace:** `replace()`
    
- **Remove outer spaces:** `trim()`

---
