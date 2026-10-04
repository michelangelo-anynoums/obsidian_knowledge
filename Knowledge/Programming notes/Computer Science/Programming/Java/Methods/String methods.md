# Java String Methods

A `String` in Java is used to store text.

```java
String name = "Alice";
```

Strings are **immutable**, which means String methods do not change the original string. Instead, they return a new `String`.

```java
String text = "hello";

text.toUpperCase();

System.out.println(text); // hello
```

To keep the result, assign it to a variable:

```java
text = text.toUpperCase();

System.out.println(text); // HELLO
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
|`indexOf()`|Finds the first position of text|`"Hello".indexOf("l")` → `2`|
|`lastIndexOf()`|Finds the last position of text|`"Hello".lastIndexOf("l")` → `3`|
|`substring()`|Extracts part of a string|`"Hello".substring(1, 4)` → `"ell"`|
|`replace()`|Replaces characters/text|`"Hello".replace("H", "J")` → `"Jello"`|
|`replaceAll()`|Replaces text using a regular expression|`"a1b2".replaceAll("\\d", "")` → `"ab"`|
|`replaceFirst()`|Replaces the first regex match|`"123123".replaceFirst("123", "X")` → `"X123"`|
|`trim()`|Removes leading/trailing whitespace|`" Hi ".trim()` → `"Hi"`|
|`strip()`|Removes leading/trailing Unicode whitespace|`" Hi ".strip()` → `"Hi"`|
|`isEmpty()`|Checks if the string has no characters|`"".isEmpty()` → `true`|
|`isBlank()`|Checks if the string is empty or only whitespace|`" ".isBlank()` → `true`|
|`concat()`|Joins another string to the end|`"Hello".concat(" World")` → `"Hello World"`|
|`repeat()`|Repeats a string a number of times|`"Hi".repeat(3)` → `"HiHiHi"`|
|`join()`|Joins multiple strings with a delimiter|`String.join("-", "A", "B", "C")` → `"A-B-C"`|
|`split()`|Splits a string into an array|`"A,B,C".split(",")` → `["A", "B", "C"]`|
|`compareTo()`|Compares strings lexicographically|`"A".compareTo("B")` → negative value|
|`compareToIgnoreCase()`|Compares strings ignoring case|`"a".compareToIgnoreCase("A")` → `0`|
|`getBytes()`|Converts the string to a byte array|`"Hello".getBytes()`|
|`toCharArray()`|Converts the string to a character array|`"Hello".toCharArray()`|

> **Note:** `strip()`, `isBlank()`, and `repeat()` were introduced in **Java 11**. If you're using an older version of Java, use alternatives such as `trim()` where appropriate.

## `length()`

Returns the number of characters in the string.

```java
String text = "Hello";

System.out.println(text.length()); // 5
```

---

## `charAt()`

Returns the character at a specified index.

Indexes start at **0**.

```java
String text = "Hello";

System.out.println(text.charAt(0)); // H
System.out.println(text.charAt(1)); // e
System.out.println(text.charAt(4)); // o
```

Think of it like this:

```text
 H  e  l  l  o
 0  1  2  3  4
```

---

## `toUpperCase()` and `toLowerCase()`

Change the case of the string.

```java
String text = "Hello";

System.out.println(text.toUpperCase()); // HELLO
System.out.println(text.toLowerCase()); // hello
```

---

## `equals()`

Checks whether two strings contain the same text.

```java
String a = "Hello";
String b = "Hello";

System.out.println(a.equals(b)); // true
```

### `equalsIgnoreCase()`

Compares strings without considering uppercase/lowercase differences.

```java
System.out.println("Hello".equalsIgnoreCase("HELLO")); // true
```

---

## `contains()`

Checks whether a string contains another sequence of characters.

```java
String text = "Hello World";

System.out.println(text.contains("World")); // true
System.out.println(text.contains("Java"));  // false
```

---

## `startsWith()` and `endsWith()`

Check whether a string starts or ends with specific text.

```java
String file = "document.pdf";

System.out.println(file.startsWith("doc")); // true
System.out.println(file.endsWith(".pdf"));  // true
```

These are particularly useful for checking file names, URLs, prefixes, and suffixes.

---

## `indexOf()`

Finds the position of the first occurrence of a character or string.

```java
String text = "Hello";

System.out.println(text.indexOf("l")); // 2
System.out.println(text.indexOf("e")); // 1
```

If the text cannot be found, `indexOf()` returns `-1`.

```java
System.out.println(text.indexOf("x")); // -1
```

### `lastIndexOf()`

Finds the position of the **last** occurrence.

```java
String text = "Hello";

System.out.println(text.lastIndexOf("l")); // 3
```

---

## `substring()`

Extracts part of a string.

```java
String text = "Hello World";

System.out.println(text.substring(0, 5)); // Hello
System.out.println(text.substring(6));    // World
```

The first index is **inclusive** and the second index is **exclusive**.

```text
H e l l o   W o r l d
0 1 2 3 4 5 6 7 8 9 10
```

So:

```java
text.substring(0, 5)
```

returns characters at indexes `0` through `4`.

---

## `replace()`

Replaces characters or sequences of characters.

```java
String text = "Hello";

System.out.println(text.replace("H", "J")); // Jello
```

It can also replace words:

```java
String text = "I like cats";

System.out.println(text.replace("cats", "dogs"));
// I like dogs
```

---

## `replaceAll()`

`replaceAll()` uses **regular expressions (regex)**.

For example, this removes all digits:

```java
String text = "a1b2c3";

System.out.println(text.replaceAll("\\d", ""));
// abc
```

For simple replacements, prefer `replace()` because it doesn't interpret the search text as a regular expression.

---

## `trim()` and `strip()`

Remove whitespace from the beginning and end of a string.

```java
String text = "   Hello   ";

System.out.println(text.trim());  // "Hello"
System.out.println(text.strip()); // "Hello"
```

Neither method removes spaces **inside** the string:

```java
"Hello World".trim()
```

still gives:

```text
Hello World
```

`strip()` is generally preferable in modern Java because it handles Unicode whitespace more appropriately.

---

## `isEmpty()`

Checks whether a string contains zero characters.

```java
String text = "";

System.out.println(text.isEmpty()); // true
```

A string containing spaces is **not** empty:

```java
System.out.println("   ".isEmpty()); // false
```

---

## `isBlank()`

Checks whether a string is empty or contains only whitespace.

```java
System.out.println("".isBlank());    // true
System.out.println("   ".isBlank()); // true
System.out.println("Hello".isBlank()); // false
```

This is often useful when validating user input.

```java
String name = "   ";

if (name.isBlank()) {
    System.out.println("Please enter your name.");
}
```

> `isBlank()` was introduced in **Java 11**.

---

## `concat()`

Adds one string to the end of another.

```java
String first = "Hello";
String result = first.concat(" World");

System.out.println(result); // Hello World
```

In normal Java code, the `+` operator is usually more convenient:

```java
String result = "Hello" + " World";
```

---

## `repeat()`

Repeats a string a specified number of times.

```java
String text = "Hi";

System.out.println(text.repeat(3));
// HiHiHi
```

Another example:

```java
System.out.println("-".repeat(10));
// ----------
```

> Available since **Java 11**.

---

## `split()`

Splits a string into an array.

```java
String text = "Apple,Banana,Orange";

String[] fruits = text.split(",");

System.out.println(fruits[0]); // Apple
System.out.println(fruits[1]); // Banana
System.out.println(fruits[2]); // Orange
```

A useful way to remember it:

```text
String → split() → String[]
```

For example:

```java
String text = "one two three";

String[] words = text.split(" ");
```

---

## `String.join()`

Joins multiple strings together using a delimiter.

```java
String result = String.join("-", "2026", "09", "30");

System.out.println(result);
// 2026-09-30
```

It can also join a collection:

```java
List<String> names = List.of("Alice", "Bob", "Charlie");

String result = String.join(", ", names);

System.out.println(result);
// Alice, Bob, Charlie
```

---

## `compareTo()`

Compares two strings lexicographically (dictionary-style).

```java
System.out.println("A".compareTo("B")); // negative
System.out.println("B".compareTo("A")); // positive
System.out.println("A".compareTo("A")); // 0
```

The important thing to remember is:

- `0` → strings are equal
    
- negative value → first string comes before the second
    
- positive value → first string comes after the second
    

You usually don't need to know the exact negative or positive number.

### `compareToIgnoreCase()`

Same idea, but ignores case:

```java
System.out.println("hello".compareToIgnoreCase("HELLO")); // 0
```

---

## `toCharArray()`

Converts a `String` into a character array.

```java
String text = "Hello";

char[] letters = text.toCharArray();

System.out.println(letters[0]); // H
```

This can be useful when you need to process individual characters.

---

## `getBytes()`

Converts a string into a byte array.

```java
String text = "Hello";

byte[] bytes = text.getBytes();
```

This is commonly encountered when working with files, networking, encryption, or character encodings.

For explicit character encoding, it's better to specify the charset:

```java
byte[] bytes = text.getBytes(StandardCharsets.UTF_8);
```

---

# Important: Comparing Strings

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

For example:

```java
String a = new String("Hello");
String b = new String("Hello");

System.out.println(a == b);      // false
System.out.println(a.equals(b)); // true
```

### Why `==` can sometimes appear to work

Java has a feature called the **String Pool**, so this can sometimes produce `true`:

```java
String a = "Hello";
String b = "Hello";

System.out.println(a == b); // true
```

However, this is **not** a reason to use `==` for String content comparison.

Use:

```java
a.equals(b)
```

---

# Useful String Patterns

## Check whether text exists

```java
if (text.contains("Java")) {
    System.out.println("Found Java!");
}
```

## Check whether a string is blank

```java
if (text.isBlank()) {
    System.out.println("No text entered.");
}
```

## Check a file extension

```java
if (filename.endsWith(".pdf")) {
    System.out.println("PDF file");
}
```

## Convert user input to lowercase

```java
String answer = input.toLowerCase();

if (answer.equals("yes")) {
    System.out.println("Continuing...");
}
```

A common alternative is:

```java
if (input.equalsIgnoreCase("yes")) {
    System.out.println("Continuing...");
}
```

---

# Example

```java
String text = "Hello World";

System.out.println(text.length());           // 11
System.out.println(text.toUpperCase());      // HELLO WORLD
System.out.println(text.toLowerCase());      // hello world
System.out.println(text.contains("World"));  // true
System.out.println(text.startsWith("Hello")); // true
System.out.println(text.endsWith("World"));  // true
System.out.println(text.charAt(0));           // H
System.out.println(text.indexOf("World"));    // 6
System.out.println(text.substring(0, 5));     // Hello
System.out.println(text.replace("World", "Java")); // Hello Java
```

---

# Quick Memory Tip

- **Size:** `length()`
    
- **Character:** `charAt()`
    
- **Change case:** `toUpperCase()`, `toLowerCase()`
    
- **Compare:** `equals()`, `equalsIgnoreCase()`
    
- **Search:** `contains()`, `indexOf()`, `lastIndexOf()`
    
- **Check beginning/end:** `startsWith()`, `endsWith()`
    
- **Extract:** `substring()`
    
- **Replace:** `replace()`, `replaceAll()`
    
- **Whitespace:** `trim()`, `strip()`
    
- **Empty/blank:** `isEmpty()`, `isBlank()`
    
- **Join:** `concat()`, `String.join()`
    
- **Split:** `split()`
    
- **Repeat:** `repeat()`
    
- **Convert:** `toCharArray()`, `getBytes()`
    
- **Sort/compare:** `compareTo()`
    

## Most Important to Learn First

If you're learning Java, focus on these first:

```text
length()
charAt()
equals()
equalsIgnoreCase()
contains()
startsWith()
endsWith()
indexOf()
substring()
replace()
isEmpty()
isBlank()
split()
```

Once those feel comfortable, learn:

```text
replaceAll()
strip()
String.join()
repeat()
compareTo()
toCharArray()
getBytes()
```