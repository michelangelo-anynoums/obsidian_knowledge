# **Introduction to ==atexit== Module**

The `atexit` module in Python allows you to register functions that will be executed when the Python interpreter is about to terminate. These functions are usually used to clean up resources, such as closing files or network connections, or logging final messages.

When Python finishes executing the main program or when the interpreter exits, all functions registered with `atexit` will be called in the reverse order that they were registered.

# **Key Concepts:**

1. **Registering Functions**: You can register functions to be executed upon program termination.
    
2. **Exit Status**: Registered functions are called regardless of how the program terminates (either normally or with an exception).
    
3. **Reverse Execution Order**: Functions are called in reverse order of registration (last registered function will be called first).
    

# **Important Methods:**

1. **atexit.register(func, *args, **kwargs)**
    
    - Registers a function `func` to be executed upon interpreter termination. You can also pass optional arguments (`*args` and `**kwargs`) to the registered function.
        
    - **Example:**
        
        ```Python
        import atexit
        def goodbye():     
			print("Goodbye, program is terminating.")
			
		atexit.register(goodbye)
        ```
        
2. **atexit._run_exitfuncs()**
    
    - This method is used internally by Python to execute all registered exit functions. You typically don’t need to call this yourself.
        
3. **atexit.unregister(func)**
    
    - Unregisters a function previously registered with `atexit.register()`. If `func` was not registered, nothing happens.
        
    - **Example:**
        
        `atexit.unregister(goodbye)`
        
4. **atexit._exitfuncs**
    
    - This is a list that holds all the functions registered for termination. You generally won't interact with it directly, but it's part of how the module works behind the scenes.
        

# **Example Code:**

```Python
import atexit
def cleanup():
	print("Cleanup activities before exit.")

atexit.register(cleanup)
  
print("Program is running...") # When the program finishes,
# 'cleanup()' will be executed automatically.
```

# **Usage Tips:**

- `atexit` is particularly useful for resources that need to be released or saved before the program ends.
    
- Functions registered via `atexit` can even handle exceptions that occur in the program, ensuring that important cleanup is done regardless of errors.

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]