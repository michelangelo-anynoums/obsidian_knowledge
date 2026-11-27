# ⚙️ Program Execution Across Operating Systems

> [!abstract] 💡 Core idea A program needs the correct **binary format, system calls, and libraries** to run on an operating system.

## 1. 📦 Binary Formats

An OS expects a specific executable file format.

- 🪟 **Windows** → PE (`.exe`)
- 🐧 **Linux** → ELF
- 🍎 **macOS** → Mach-O

```text
Windows  → PE
Linux    → ELF
macOS    → Mach-O
```

❌ A Linux kernel cannot directly load a standard Windows PE executable.

## 2. 🔌 System Calls

Programs use **system calls** to request services from the OS.

Examples:

- Read or write files
- Create processes
- Access networking
- Communicate with hardware

```js
// Node.js: request a file operation
const fs = require('node:fs');

fs.writeFileSync('hello.txt', 'Hello OS!');
```

Node.js provides a common API, but internally the OS uses its own system calls.

```
Node.js API
    ↓
Operating System
    ↓
System Calls
    ↓
Hardware / Resources
```

## 3. 📚 Library Dependencies

An executable may depend on libraries provided by its target OS.

```
Application
    ↓
Required Libraries
    ↓
Operating System
```

If a required library is missing or incompatible:

```
❌ Missing library
       ↓
❌ Program fails to launch
```

For example:

- Windows → DLL files
- Linux → Shared libraries (`.so`)
- macOS → Dynamic libraries (`.dylib`)

## 🎯 The Big Picture

For a program to execute correctly, three things must work together:

|Requirement|Purpose|
|---|---|
|📦 Binary format|OS can load the executable|
|🔌 System calls|Program can request OS services|
|📚 Libraries|Required dependencies are available|

**Remember:**

```
Source Code
    ↓
Compilation
    ↓
Executable Binary
    ↓
OS Loader
    ↓
Libraries + System Calls
    ↓
🚀 Program Execution
```

💡 **Key takeaway:** Code portability doesn't automatically mean executable portability. Node.js helps make applications cross-platform, but native dependencies and OS-specific behavior can still create compatibility issues.

---

## 🖥️ Windows vs Linux: Execution Example

Imagine we have a simple C program:

```c
#include <stdio.h>

int main() {
    printf("Hello World!\n");
    return 0;
}
```

### 🪟 Windows

Compile using GCC:

```bash
gcc hello.c -o hello.exe
```

Execute:

```powershell
.\hello.exe
```

**Result:** Windows loads the PE executable and runs it.

### 🐧 Linux

Compile on Linux:

```bash
gcc hello.c -o hello
```

Execute:

```bash
./hello
```

**Result:** Linux loads the ELF executable and runs it.

### ⚠️ What if we transfer the executable?

```
Windows hello.exe → Linux ❌
Linux hello       → Windows ❌
```

Neither executable runs natively in the other OS.

Why?

- 📦 Different binary formats (PE vs ELF).
- 🔌 Different system call interfaces.
- 📚 Different native libraries.

### 💡 Important Exception

Compatibility layers can help:

- **Wine:** Runs many Windows applications on Linux.
- **WSL:** Allows Linux environments to run on Windows.

**Remember:** Compile for your target OS, or use a compatibility layer when necessary.

---
