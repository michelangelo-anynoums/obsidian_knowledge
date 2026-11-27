![[Pasted image 20261127130504.png|473]]

# ☕ Java Execution Process

> [!abstract] 💡 Overview Java uses a combination of compilation and interpretation to execute programs. Source code is compiled into **bytecode**, which runs on the Java Virtual Machine (JVM).

## ⚙️ Execution Flow

```
📄 Main.java
     |
     ▼
⚙️ Java Compiler (javac)
     |
     ▼
📦 Main.class (Bytecode)
     |
     ▼
☕ JVM (Java Virtual Machine)
     |
     ├── Class Loader
     ├── Bytecode Verifier
     ├── Runtime Memory
     └── Execution Engine
              |
              ▼
       🖥️ Machine Code
              |
              ▼
          🚀 Output
```

## 🧩 Step-by-Step

1. **Source Code** – Write Java code in a `.java` file.
2. **Compilation** – `javac` converts source code into bytecode (`.class`).
3. **Class Loading** – JVM loads the required classes.
4. **Verification** – JVM checks bytecode for validity and safety.
5. **Execution** – Execution Engine interprets bytecode and uses JIT compilation to optimize frequently executed code.
6. **Output** – The program runs on the operating system.

## 💻 Example

**1. Create Java file**

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Java!");
    }
}
```

**2. Compile**

```bash
javac Main.java
```

**3. Execute**

```bash
java Main
```

**Output:**

```text
Hello Java!
```

## 🔑 Important Components

|Component|Function|
|---|---|
|JDK|Development tools, including compiler|
|JRE|Runtime environment and libraries|
|JVM|Executes Java bytecode|
|JIT|Compiles frequently executed bytecode into native machine code|
|Bytecode|Platform-independent intermediate code|

> [!tip] 🧠 Remember **Write → Compile → Load → Verify → Execute**
> 
> Java's bytecode makes the same compiled program portable across different platforms, provided a compatible JVM is available.

---
