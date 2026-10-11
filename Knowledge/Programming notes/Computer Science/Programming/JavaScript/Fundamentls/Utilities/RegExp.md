# 🔎 JavaScript — Regular Expressions (RegExp)

> [!abstract] Overview **Regular Expressions (RegExp)** are patterns used to search, match, validate, and replace text in JavaScript.

## 🧩 1. Creating a Pattern

There are two main ways to create a regular expression.

### Method 1 — Literal notation

```js
const pattern = /hello/;
```

### Method 2 — Constructor notation

```js
const pattern = new RegExp("hello");
```

Both create a pattern that matches the text `hello`.

## ✅ 2. The `test()` Method

The `test()` method checks whether a string matches a pattern.

**Returns:** `true` or `false`.

```js
const pattern = /hello/;

console.log(pattern.test("hello world")); // true
console.log(pattern.test("good morning")); // false
```

> [!tip] Remember `pattern.test(string)` → Checks for a match.

## 🔤 3. Common Pattern Characters

|Pattern|Meaning|
|---|---|
|`abc`|Matches the text `abc`|
|`.`|Matches almost any single character except line terminators by default|
|`\d`|A digit (`0–9`)|
|`\D`|A non-digit|
|`\w`|A word character: letters, digits or underscore|
|`\W`|A non-word character|
|`\s`|A whitespace character|
|`\S`|A non-whitespace character|
|`[abc]`|Any one of `a`, `b` or `c`|
|`[a-z]`|Any lowercase ASCII letter|
|`[A-Z]`|Any uppercase ASCII letter|
|`[0-9]`|Any digit|
|`[^abc]`|Any character except `a`, `b` or `c`|

## 🎯 4. Special Symbols

|Symbol|Meaning|
|---|---|
|`^`|Start of input|
|`$`|End of input|
|`*`|Zero or more repetitions|
|`+`|One or more repetitions|
|`?`|Zero or one repetition|
|`{n}`|Exactly `n` repetitions|
|`{n,}`|At least `n` repetitions|
|`{n,m}`|Between `n` and `m` repetitions|
|`\`|Escapes a special character or introduces a character class|
|`()`|Groups an expression|
|`|`|

### Examples

```js
/^\d+$/       // Only digits, at least one
/^[a-z]+$/i   // Only letters, case-insensitive
/^hello/      // Starts with "hello"
/world$/      // Ends with "world"
/colou?r/     // Matches "color" or "colour"
/cat|dog/     // Matches "cat" or "dog"
```

## 🚩 5. RegExp Flags

Flags change how a pattern behaves.

|Flag|Meaning|
|---|---|
|`i`|Case-insensitive matching|
|`g`|Find all matches rather than stopping at the first|
|`m`|Make `^` and `$` work at line boundaries|
|`s`|Let `.` also match line terminators|
|`u`|Enable Unicode-aware pattern interpretation|
|`y`|Match at the current `lastIndex` position|
|`d`|Include match indices in the result|

Example:

```js
const pattern = /hello/i;

console.log(pattern.test("HELLO")); // true
console.log(pattern.test("Hello")); // true
```

The `i` flag ignores differences between uppercase and lowercase letters.

## 🔍 6. Useful RegExp Methods

|Method|Purpose|
|---|---|
|`test()`|Returns `true` or `false`|
|`exec()`|Returns match details or `null`|
|`String.match()`|Retrieves matching text|
|`String.matchAll()`|Retrieves all matches and their details|
|`String.search()`|Returns the index of a match, or `-1`|
|`String.replace()`|Replaces matching text|
|`String.replaceAll()`|Replaces all matching occurrences|
|`String.split()`|Splits a string using a pattern|

### `test()` — Check for a match

```js
const pattern = /JavaScript/i;

console.log(pattern.test("I love JavaScript"));
// true
```

### `exec()` — Get match details

```js
const pattern = /\d+/;

console.log(pattern.exec("Age: 25"));
// ["25"]
```

### `match()` — Find matching text

```js
console.log("Room 123".match(/\d+/));
// ["123"]
```

### `replace()` — Replace matching text

```js
console.log("Hello world".replace(/world/, "JavaScript"));
// "Hello JavaScript"
```

### `search()` — Find the position

```js
console.log("Hello world".search(/world/));
// 6
```

### `split()` — Split text using a pattern

```js
console.log("red,green;blue".split(/[,;]/));
// ["red", "green", "blue"]
```

## 🧪 7. Practical Examples

### Check whether a string contains a digit

```js
const pattern = /\d/;

console.log(pattern.test("hello"));   // false
console.log(pattern.test("hello5"));  // true
```

### Check a simple username format

```js
const username = "John123";
const pattern = /^[a-z0-9_]{3,16}$/i;

console.log(pattern.test(username)); // true
```

This example accepts 3–16 characters consisting of letters, digits and underscores.

### Check a basic email format

```js
const email = "user@example.com";
const pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

console.log(pattern.test(email)); // true
```

> [!warning] Important This email pattern is a simple check, not a complete implementation of email validation. Real email addresses have more complex rules.

## ⚠️ 8. Important Things to Remember

- Regular expressions are objects used to match text.
- `test()` returns a Boolean value.
- `^` and `$` help check the beginning and end of input.
- Flags modify matching behavior.
- `g` and `y` can make repeated calls to `test()` stateful because they use `lastIndex`.
- Use `String()` methods when you want to search, extract, replace or split text.
- Complex regular expressions can become difficult to read, so keep patterns simple and test them carefully.

## 🧠 9. Quick Revision

|Question|Answer|
|---|---|
|What is RegExp?|A pattern for matching text|
|How do you create one?|`/pattern/` or `new RegExp()`|
|What does `test()` return?|`true` or `false`|
|Which flag ignores case?|`i`|
|Which character matches a digit?|`\d`|
|Which symbol means one or more?|`+`|
|Which symbol means zero or more?|`*`|
|Which symbol means the start?|`^`|
|Which symbol means the end?|`$`|
|Which method replaces text?|`replace()`|

---
