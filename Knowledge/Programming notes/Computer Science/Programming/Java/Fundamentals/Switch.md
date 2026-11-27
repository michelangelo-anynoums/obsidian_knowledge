# ☕ Java `switch`

A `switch` statement is used when you want to choose **one action from several possible options** based on the value of an expression.

### Basic structure

```java
switch (expression) {
    case value1:
        // code
        break;

    case value2:
        // code
        break;

    default:
        // code if no case matches
}
```

### Simple example

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;

    case 2:
        System.out.println("Tuesday");
        break;

    case 3:
        System.out.println("Wednesday");
        break;

    default:
        System.out.println("Invalid day");
}
```

**Output:**

```text
Tuesday
```

### 🧠 Remember

- `switch` → checks a value.
    
- `case` → defines a possible value.
    
- `break` → stops the switch after a match.
    
- `default` → runs when no case matches.
    
- Without `break`, Java can continue into the next case (**fall-through**).
    

### ✨ Modern Java

Modern Java also supports the cleaner **switch expression**:

```java
String result = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Invalid day";
};
```

**In one sentence:**

> Use `switch` when you have **one value and several possible choices**.