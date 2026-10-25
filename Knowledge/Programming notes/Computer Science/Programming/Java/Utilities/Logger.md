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

## 📂 7. Write Logs to a File

Configure a `FileHandler` to save logs.

```java
import java.io.IOException;
import java.util.logging.FileHandler;
import java.util.logging.SimpleFormatter;

try {
    FileHandler fileHandler =
            new FileHandler("application.log", true);

    fileHandler.setFormatter(new SimpleFormatter());
    logger.addHandler(fileHandler);

} catch (IOException e) {
    logger.log(Level.SEVERE, "Could not create log file", e);
}
```

📌 `true` appends to the existing file instead of overwriting it.

⚠️ Remember to close handlers when they are no longer needed. For production, consider file rotation and centralized configuration.

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
