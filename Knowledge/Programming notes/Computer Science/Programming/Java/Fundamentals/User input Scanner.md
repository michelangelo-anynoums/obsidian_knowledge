## 📌 Java Scanner Object

> **Purpose:** The `Scanner` class is used to get user input. It is part of the `java.util` package. 🔍

### 🛠️ Setup & Import

To use the scanner, you first need to import it at the top of your Java file:


```Java
import java.util.Scanner;
```

### 💻 Code Example

Here is a quick example showing how to read a user's name and age:


```Java
import java.util.Scanner;

public class UserInputExample {
    public static void main(String[] args) {
        // Create a Scanner object to read from standard input (keyboard)
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine(); // Reads a full line of text

        System.out.print("Enter your age: ");
        int age = scanner.nextInt(); // Reads an integer

        System.out.println("Hello, " + name + "! You are " + age + " years old. 🎉");

        // Good practice: close the scanner when done
        scanner.close();
    }
}
```

### 📋 Common Scanner Methods

| **Method**      | **What it does**                       | **💡 Example**                             |
| --------------- | -------------------------------------- | ------------------------------------------ |
| `next()`        | Reads a single word (stops at space)   | `String word = scanner.next();`            |
| `nextLine()`    | Reads an entire line of text           | `String sentence = scanner.nextLine();`    |
| `nextInt()`     | Reads an integer value                 | `int number = scanner.nextInt();`          |
| `nextDouble()`  | Reads a floating-point number          | `double price = scanner.nextDouble();`     |
| `nextBoolean()` | Reads a boolean value (`true`/`false`) | `boolean isReady = scanner.nextBoolean();` |

### ⚠️ Quick Tips

- **Memory Management:** It's a good habit to call `scanner.close()` when you're finished with it to prevent resource leaks. 🧹
    
- **Input Mismatch:** If a user types letters when `nextInt()` is expecting a number, Java will throw an `InputMismatchException`.-

---
