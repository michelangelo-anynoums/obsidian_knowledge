# **Python ==sys== Module — Short Summary**


> The **sys** module provides access to variables and functions that interact with the **Python interpreter** itself.  
It lets you manage the runtime environment, control program execution, and work with system-level information.

---
# **Main Functions & Attributes**

### **1. sys.argv**

List of command‑line ==arguments passed to the script.==
Useful for CLI tools and argument parsing.

 **Example:**

```Python
import sys
print(sys.argv)   # ['script.py', 'arg1', 'arg2']
```

### **2. sys.exit()**

==Stop program execution== and optionally return an exit code.

 **Example:**

```Python
import sys
sys.exit("Stopping program")
```

### **3. sys.path**

List of directories where ==Python looks for modules.== 
Can be modified to load custom modules.

 **Example:**

```Python
import sys
print(sys.path)
sys.path.append("/my/custom/path")
```

### **4. sys.version**

String showing the ==Python version== currently running.

 **Example:**

```Python
import sys
print(sys.version)
```

### **5. sys.platform**

Identifies the ==operating system== (e.g., `"win32"`, `"linux"`).

 **Example:**

```Python
import sys
print(sys.platform)   # e.g. 'linux', 'win32'
```

### **6. sys.stdin, sys.stdout, sys.stderr**

==Standard input/output/error streams.==
Useful for low‑level console apps and redirects.

 **Example:**

```Python
import sys
data = sys.stdin.read(1)      # read input. Pass an argument to read()
sys.stdout.write("Hello\n")  # print manually
sys.stderr.write("Error!\n") # error output
```

### **7. sys.getsizeof()**

Returns ==the size== (in bytes) of an object in memory.

 **Example:**

```Python
import sys
print(sys.getsizeof("text"))  # size in bytes
```

### **8. sys.modules**

Dictionary of ==loaded modules;== useful for debugging or dynamic imports.

 **Example:**

```Python
import sys
import math
print("math" in sys.modules)  # True
```

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]