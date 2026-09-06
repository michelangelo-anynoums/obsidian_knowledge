
## Python `subprocess` Module – Quick Reference

## Overview

The `subprocess` module allows you to **spawn new processes**, **connect to their input/output/error pipes**, and **obtain their return codes**. It is preferred over older modules like `os.system` for better control and security.

---

## 1. Importing

```Python
import subprocess
```

---

## 2. Running External Commands

### **subprocess.run()**

- Recommended for **simple use cases** (Python 3.5+)
- Returns a `CompletedProcess` object

```Python
result = subprocess.run(["ls", "-l"], capture_output=True, text=True) 
print(result.stdout)   # Command output  
print(result.returncode)  # Exit code
```

**Key arguments:**

- `args` – list of command + arguments
- `capture_output=True` – capture stdout and stderr
- `text=True` – decode bytes to string
- `check=True` – raise `CalledProcessError` on non-zero exit

---

### **subprocess.Popen()**

- For **advanced use cases**: streaming input/output, asynchronous execution

proc = subprocess.Popen(  
    ["ping", "-c", "4", "example.com"],  
    stdout=subprocess.PIPE,  
    stderr=subprocess.PIPE,  
    text=True  
)  
stdout, stderr = proc.communicate()  
print(stdout)

**Key attributes & methods:**

- `proc.communicate(input=None)` – interact with process
- `proc.wait()` – wait for completion
- `proc.terminate()` / `proc.kill()` – stop process
- `proc.returncode` – get exit status

---

## 3. Capturing Output

## **Using run()**  
result = subprocess.run(["echo", "Hello"], capture_output=True, text=True)  
print(result.stdout.strip())  # "Hello"  
  
## **Using Popen()**

```Python
proc = subprocess.Popen(["echo", "Hello"], stdout=subprocess.PIPE, text=True)  
output, _ = proc.communicate()  
print(output.strip())  # "Hello"
```

---

## 4. Handling Errors

```Python
try:  
    subprocess.run(["false"], check=True)  
except subprocess.CalledProcessError as e:  
    print(f"Error: {e.returncode}")
```

---

## 5. Advanced Options

- `cwd="path"` – set working directory for the command
- `env={"VAR": "value"}` – set environment variables
- `shell=True` – run command through shell (**caution: security risk**)
- Piping between processes:

```Python
p1 = subprocess.Popen(["ls"], stdout=subprocess.PIPE)  
p2 = subprocess.Popen(["grep", "py"], stdin=p1.stdout, stdout=subprocess.PIPE, text=True)  
output, _ = p2.communicate()  
print(output)
```

---

## 6. Notes / Best Practices

- Prefer `subprocess.run()` for simplicity.
- Avoid `shell=True` unless necessary.
- Always handle exceptions (`CalledProcessError`) for robustness.
- Use lists (`["command", "arg"]`) rather than strings to prevent shell injection.