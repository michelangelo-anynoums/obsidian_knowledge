# ☕ Java – Log4j2 Setup

> [!tip] Purpose Simple logging setup for Java applications using Apache Log4j 2.

## 1. Dependencies – Maven

Add to `pom.xml`:

```xml
<properties>
    <log4j.version>2.25.3</log4j.version>
</properties>

<dependencies>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>${log4j.version}</version>
    </dependency>

    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>${log4j.version}</version>
    </dependency>
</dependencies>
```

## 2. Project structure

```text
src/
 └── main/
     ├── java/
     │   └── app/log4j2/
     │       └── Log4j2.java
     │
     └── resources/
         └── log4j2.xml
logs/
 └── application.log
pom.xml
```

## 3. Java Logger – Log4j2.java

```java
package app.log4j2;

import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

public class Log4j2 {

    private static final Logger logger =
        LogManager.getLogger(Log4j2.class);

    public static void main(String[] args) {

        logger.info("Application starting...");

        try {
            initializeApplication();

            logger.info("Application started successfully.");

        } catch (Exception e) {

            logger.error("Startup failed!", e);

            System.exit(1);
        }
    }

    private static void initializeApplication() {

        logger.info("Loading configuration...");
        logger.info("Initializing services...");
        logger.info("Initialization completed.");
    }
}
```

> [!important] Remember Always use your actual class name in `LogManager.getLogger(ClassName.class)`.

## 4. Configuration – log4j2.xml

Location: `src/main/resources/log4j2.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>

<Configuration status="WARN">

    <Properties>
        <Property name="LOG_DIR">logs</Property>
        <Property name="PATTERN">
            %d{yyyy-MM-dd HH:mm:ss} [%t] %-5level %logger{36} - %msg%n
        </Property>
    </Properties>

    <Appenders>

        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout pattern="${PATTERN}"/>
        </Console>

        <RollingFile name="FileLogger"
            fileName="${LOG_DIR}/application.log"
            filePattern="${LOG_DIR}/application-%d{yyyy-MM-dd}-%i.log.gz">

            <PatternLayout pattern="${PATTERN}"/>

            <Policies>
                <TimeBasedTriggeringPolicy/>
                <SizeBasedTriggeringPolicy size="10 MB"/>
            </Policies>

            <DefaultRolloverStrategy max="10"/>

        </RollingFile>

    </Appenders>

    <Loggers>
        <Root level="info">
            <AppenderRef ref="Console"/>
            <AppenderRef ref="FileLogger"/>
        </Root>
    </Loggers>

</Configuration>
```

## 5. Logging levels

|Level|Usage|
|---|---|
|`TRACE`|Detailed tracing|
|`DEBUG`|Debugging|
|`INFO`|Normal events|
|`WARN`|Warnings|
|`ERROR`|Errors|
|`FATAL`|Critical failures|

### Examples

```java
logger.trace("Trace message");
logger.debug("Debug message");
logger.info("Application running");
logger.warn("Something needs attention");
logger.error("An error occurred");
logger.fatal("Critical failure");
```

### Exception logging

```java
try {
    // Your application logic

} catch (Exception e) {
    logger.error("Operation failed!", e);
}
```

## 6. Build and run

```bash
mvn clean install
```

Run from your IDE or Maven-configured application launcher.

## 7. Expected output

```bash
2026-11-02 18:00:00 [main] INFO  Log4j2 - Application starting...
2026-11-02 18:00:00 [main] INFO  Log4j2 - Loading configuration...
2026-11-02 18:00:00 [main] INFO  Log4j2 - Initializing services...
2026-11-02 18:00:00 [main] INFO  Log4j2 - Application started successfully.
```

---

# ☕ Log4j2 – Properties Setup

> [!info] Purpose Configure Apache Log4j2 using a simple `.properties` file instead of XML.

## 1. File location

```bash
src/main/resources/log4j2.properties
```

## 2. Basic configuration

```bash
# Configuration
status = warn
name = PropertiesConfig

# Log directory
property.logDir = logs

# Console
appender.console.type = Console
appender.console.name = Console
appender.console.layout.type = PatternLayout
appender.console.layout.pattern = %d{HH:mm:ss} %-5level %logger - %msg%n

# File
appender.file.type = File
appender.file.name = FileLogger
appender.file.fileName = ${logDir}/application.log
appender.file.layout.type = PatternLayout
appender.file.layout.pattern = %d{yyyy-MM-dd HH:mm:ss} %-5level %logger - %msg%n

# Root logger
rootLogger.level = info
rootLogger.appenderRefs = console, file
rootLogger.appenderRef.console.ref = Console
rootLogger.appenderRef.file.ref = FileLogger
```

## 3. Java implementation

```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

private static final Logger logger =
    LogManager.getLogger(Log4j2.class);

logger.info("Application started!");
logger.warn("Warning message");
logger.error("Error message");
```

## 4. Logging levels

|Level|Purpose|
|---|---|
|TRACE|Detailed tracing|
|DEBUG|Debugging|
|INFO|General information|
|WARN|Warnings|
|ERROR|Errors|
|FATAL|Critical errors|

## 5. Important commands

```bash
mvn clean install
```

**Log output:**

```log
logs/application.log
```

> [!tip] Remember
> 
> - Use `log4j2.properties` inside `src/main/resources`.
> - No Java code changes are needed when switching from XML.
> - Keep only one active Log4j2 configuration file.
> - Use `File` for simple logging or `RollingFile` for automatic log rotation.

**Documentation:** https://logging.apache.org/log4j/2.x/

---
