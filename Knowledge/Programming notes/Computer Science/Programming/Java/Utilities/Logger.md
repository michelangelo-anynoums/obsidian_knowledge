# ☕ Java Logger

> [!abstract] 💡 What is a Logger? A **Logger** records application events, errors, warnings, and debugging information. It helps you understand what your application is doing without using `System.out.println()` everywhere.

## 🛠️ 1. Basic Setup

Java's built-in logging utility is `java.util.logging` (JUL).

```java
import java.util.logging.Logger;
import java.util.logging.Level;

public class Main {
    private static final Logger logger =
            Logger.getLogger(Main.class.getName());

    public static void main(String[] args) {
        logger.info("Application started!");
        logger.warning("Something looks suspicious.");
        logger.severe("Something went wrong!");
    }
}
```

📌 **Tip:** Create one `static final Logger` per class.

## 🎚️ 2. Logging Levels

|Level|Purpose|
|---|---|
|`SEVERE` 🚨|Serious errors|
|`WARNING` ⚠️|Potential problems|
|`INFO` ℹ️|Important application events|
|`CONFIG` ⚙️|Configuration details|
|`FINE` 🔍|Debugging information|
|`FINER` 🧩|More detailed debugging|
|`FINEST` 🔬|Very detailed tracing|

```java
logger.severe("Database connection failed");
logger.warning("Retrying connection...");
logger.info("User logged in");
logger.fine("Processing user ID: 42");
```

💡 `FINE`, `FINER`, and `FINEST` are usually hidden by default.

## 🎛️ 3. Set the Logging Level

Only messages enabled by the logger's level are processed.

```java
logger.setLevel(Level.FINE);

logger.info("Application running");
logger.fine("Debug details");
```

⚠️ Setting the logger level alone may not be enough. The console handler must also allow `FINE` messages.

```java
import java.util.logging.ConsoleHandler;
import java.util.logging.Level;
import java.util.logging.Logger;

Logger logger = Logger.getLogger(Main.class.getName());

logger.setLevel(Level.FINE);

ConsoleHandler handler = new ConsoleHandler();
handler.setLevel(Level.FINE);

logger.addHandler(handler);
```

📌 For a real application, configure handlers centrally to avoid duplicate messages.

## 🧩 4. Log Exceptions Properly

Use `log()` to include the exception and its stack trace.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    logger.log(Level.SEVERE, "Calculation failed", e);
}
```

✅ Includes the exception details and stack trace.

❌ Avoid logging only `e.getMessage()` when you need to diagnose the cause.

## 📝 5. Parameterized Messages

Use `{0}`, `{1}`, etc. instead of building strings manually.

```java
logger.log(Level.INFO, "User {0} logged in", username);
```

Multiple parameters:

```java
logger.log(
    Level.INFO,
    "User {0} purchased {1} items",
    new Object[]{username, quantity}
);
```

💡 Avoid unnecessary string concatenation in frequently executed logging statements.

## 🏷️ 6. Log Levels with Conditions

```java
if (logger.isLoggable(Level.FINE)) {
    logger.fine("Expensive debug data: " + calculateDetails());
}
```

🔍 Useful when preparing a log message is expensive. The condition avoids doing that work when `FINE` logging is disabled.

---

## 7. 📁 File Logging in Java

Java provides the `FileHandler` class in `java.util.logging` to write log messages into a file.

### 7.1 📝 Write logs to a file


```java
import java.io.IOException;
import java.util.logging.*;

public class Main {
    private static final Logger logger =
            Logger.getLogger(Main.class.getName());

    public static void main(String[] args) {
        try (FileHandler handler =
                     new FileHandler("application.log")) {

            handler.setFormatter(new SimpleFormatter());
            logger.addHandler(handler);

            try {
                logger.info("Application started");
                logger.warning("This is a warning");
                logger.severe("An error occurred");
            } finally {
                logger.removeHandler(handler);
            }

        } catch (IOException e) {
            System.err.println("Logging failed: " + e.getMessage());
        }
    }
}
```

**🔍 Explanation:**

- 📄 `FileHandler("application.log")` creates a handler that writes logs to the specified file. By default, an existing file may be overwritten.
- ✍️ `setFormatter(new SimpleFormatter())` formats log records as readable text.
- 🔗 `logger.addHandler(handler)` connects the handler to the logger.
- 🔌 `logger.removeHandler(handler)` disconnects the handler when it is no longer needed.
- ✅ `try-with-resources` automatically closes the handler, even if an exception occurs.

### 7.2 ➕ Append new logs to an existing file

> [!important] To preserve previous logs and add new ones, pass `true` as the second argument to the `FileHandler` constructor:

```java
new FileHandler("application.log", true);
```

For example:

```java
try (FileHandler handler =
         new FileHandler("application.log", true)) {

    handler.setFormatter(new SimpleFormatter());
    logger.addHandler(handler);

    try {
        logger.info("A new application session started");
        logger.info("Processing a task");
    } finally {
        logger.removeHandler(handler);
    }

} catch (IOException e) {
    System.err.println("Could not write logs: " + e.getMessage());
}
```

🔄 When the program runs again, new log records are appended to the existing file instead of replacing its contents.

### 7.3 🔒 How to close a FileHandler properly

A `FileHandler` should be closed when you finish logging to release resources and ensure pending log data is written.

**✅ Option 1: Try-with-resources (recommended)**

> [!fire] Java automatically closes the handler when the `try` block finishes.

```java
try (FileHandler handler =
         new FileHandler("application.log", true)) {

    logger.addHandler(handler);
    try {
        logger.info("Application started");
    } finally {
        logger.removeHandler(handler);
    }

} catch (IOException e) {
    System.err.println(e.getMessage());
}
```

**🧹 Option 2: Finally block**

> [!fire] Close the handler manually, even if an exception occurs.

```java
FileHandler handler = null;

try {
    handler = new FileHandler("application.log", true);
    logger.addHandler(handler);
    logger.info("Application started");

} catch (IOException e) {
    System.err.println(e.getMessage());

} finally {
    if (handler != null) {
        logger.removeHandler(handler);
        handler.close();
    }
}
```

💡 **Best practice:** Use try-with-resources for short tasks. For long-running applications, keep the handler open and close it during application shutdown.

## ⚙️ 8. Configure Logging with `logging.properties`

Example configuration:

```java
.level=INFO
java.util.logging.ConsoleHandler.level=INFO
java.util.logging.ConsoleHandler.formatter=java.util.logging.SimpleFormatter
```

Load it when starting Java:

```java
java -Djava.util.logging.config.file=logging.properties Main
```

💡 Centralized configuration is cleaner than configuring every logger in code.

## ✅ 9. Best Practices

- ✅ Use meaningful messages: `"Payment failed"` instead of `"Error"`.
- ✅ Use the correct level for each event.
- ✅ Include exceptions with `logger.log(level, message, exception)`.
- ✅ Prefer parameterized messages.
- ❌ Never log passwords, tokens, or sensitive personal data.
- ❌ Don't log the same exception repeatedly at every layer.
- ❌ Avoid `System.out.println()` for application logging.
- 📌 Keep logs useful, searchable, and concise.

## 🚀 Quick Reference

```java
logger.info("General information");
logger.warning("Potential problem");
logger.severe("Critical failure");

logger.fine("Debug details");
logger.log(Level.SEVERE, "Operation failed", exception);

logger.log(Level.INFO, "Hello, {0}", username);
```

> [!tip] 🧠 Remember **Logger = record events. Level = importance. Handler = destination. Formatter = output format.**
