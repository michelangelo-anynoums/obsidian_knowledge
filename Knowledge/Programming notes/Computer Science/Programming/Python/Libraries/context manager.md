# **Why use ==with==?**

Normally, when you open a file, you would need to manually close it when you're done, like this:

```Python
file = open("example.txt", "r") 
# do something with the file 
file.close()  
# you need to remember to do this!
```

But if you forget to close the file, it can lead to memory leaks or other issues. This is where the `with` statement comes in handy. It ensures that resources like files are automatically cleaned up (closed) when you're done with them, even if an error happens during your code execution.

# **How it works:**

The `with` statement is used with something called a **context manager**. A context manager handles the setup and teardown of resources (like opening/closing files), so you don’t have to worry about doing it yourself.

The basic syntax looks like this:

```Python
with open("example.txt", "r") as file:     
# do something with the file 
# no need to explicitly call file.close() - it's done for you
```

Here’s what happens:

1. The `open("example.txt", "r")` part opens the file.
    
2. The `as file` assigns the file object to the variable `file`.
    
3. When the code block under the `with` statement is done, the file is automatically closed for you.
    

# **Key points about ==with==:**

1. **Automatic cleanup**: After the block of code is executed, Python will automatically call the `__exit__()` method of the context manager (e.g., `file.close()` for files), even if there was an error inside the block.
    
2. **Better readability and less chance of errors**: You don't have to manually call cleanup functions, so the code is cleaner and safer.
    

# **Examples of using ==with==:**

# **Opening and reading a file:**

```Python
with open("example.txt", "r") as file:     
	content = file.read()     
	print(content)  # the file is automatically closed after this block
```

# **Writing to a file:**

```Python
with open("example.txt", "w") as file:     
	file.write("Hello, Python!")
```

# **Using ==with== for other resources (e.g., locks or database connections):**

If you're using things like a **lock** in a multi-threaded environment, the `with` statement ensures that the lock is released once you're done with it.

```Python
import threading  
lock = threading.Lock()  

with lock:     
	# critical section of code that needs to be synchronized     
	print("This is a thread-safe operation")
```

### **Creating your own context manager:**

You can also create your own custom context manager using the `contextlib` module or by defining `__enter__` and `__exit__` methods in a class.

For example, using `contextlib`:

```Python
from contextlib import contextmanager  

@contextmanager def my_resource():     
	print("Setting up resource")     
	yield "Resource ready"     
	print("Cleaning up resource")  
	
with my_resource() as resource:     
	print(resource)  # "Resource ready"
```
# **In summary:**

- `with` makes sure resources are properly cleaned up.
    
- It's commonly used with files, but can be used for other resources too (like database connections or locks).
    
- It's safer, cleaner, and less error-prone compared to manually managing resources.
---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]