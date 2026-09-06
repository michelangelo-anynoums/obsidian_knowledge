# **Introduction to the ==time== Library**

The **==time==** module in Python provides various time-related functions that allow you to work with time and dates, measure time intervals, and even pause your program for specific amounts of time.

This library is particularly useful for tasks like:

- Tracking how long code execution takes.
    
- Pausing the program (e.g., sleeping).
    
- Formatting and converting dates and times.
    

# **Key Concepts and Functions**

Here are some of the most important functions from the `time` library:

1. ==**time.time()**==
    
    - Returns the current time in seconds since the "epoch" (usually January 1, 1970). It’s a floating point number where the decimal part represents fractions of a second.
        
    - **Example**:
        
      ```Python
         import time 
         print(time.time())  
         # Output might be something like: 1671219205.356724
         ```
        
1. ==**time.sleep(seconds)**==
    
    - Pauses the execution of your program for a given number of seconds.
        
    - Useful when you want to delay something, like waiting between actions or making your program wait for user input.
        
    - **Example**:
        
        ```Python
        import time 
        print("Start") 
        time.sleep(2)  
        # Pauses for 2 seconds 
        print("End")
        ```
        
        
1. ==**time.localtime([seconds])**==
    
    - Converts a time expressed in seconds since the epoch to a struct_time in local time. If no argument is given, it uses the current time.
        
    - **Example**:
        
        ```Python
        import time
        local_time = time.localtime()
        # Get the current local time 
        print(local_time)
        ```
        
1. ==**time.strftime(format, [t])**==
    
    - Converts a `struct_time` or a timestamp to a string according to a given format.
        
    - You can use this to format the current time or any `struct_time` into a human-readable string.
        
    - **Example**:
        
        ```Python
        import time
        current_time = time.localtime()  
        # Get current local time 
        formatted_time = time.strftime("%Y-%m-%d %H:%M:%S", current_time) 
        print(formatted_time)  
        # Example output: '2023-12-23 15:42:50'
        ```
        
1. ==**time.perf_counter()**==
    
    - Returns the value (in seconds) of a performance counter, which is the highest resolution timer available. This is useful for measuring short time intervals.
        
    - **Example**:
        
        ```Python
        import time 
        start = time.perf_counter() 
        # Do something you want to measure 
        end = time.perf_counter() 
        print(f"Time taken: {end - start} seconds")
        ```
        
1. ==**time.gmtime([seconds])**==
    
    - Converts a time expressed in seconds since the epoch to UTC (Coordinated Universal Time) as a `struct_time` object.
        
    - **Example**:
        
        ```Python
        import time
        utc_time = time.gmtime()  
        # Get current UTC time print(utc_time)
        ```
        

# **Common Formatting Options for ==strftime()==**

When formatting dates and times, you can use several placeholders like:

- `%Y`: Year with century (e.g., 2023)
    
- `%m`: Month as a zero-padded decimal number (e.g., 12)
    
- `%d`: Day of the month as a zero-padded decimal number (e.g., 23)
    
- `%H`: Hour (24-hour clock) as a zero-padded decimal number (e.g., 15)
    
- `%M`: Minute as a zero-padded decimal number (e.g., 42)
    
- `%S`: Second as a zero-padded decimal number (e.g., 50)
    

For example:

```Python
import time
formatted_time = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) 
print(formatted_time)
```

# **Summary**

The `time` module is great for handling time in your programs, whether it's for measuring performance, formatting dates, or adding delays. The most commonly used functions are `time.time()`, `time.sleep()`, `time.localtime()`, and `time.strftime()`. Once you're familiar with these, you'll be able to work with time effectively in Python!

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]