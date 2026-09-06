# **Introduction to Python's ==threading== Library**

The `threading` library in Python allows you to run multiple tasks (threads) simultaneously. This is especially useful for tasks that involve I/O operations (e.g., reading files, network requests) or when you want to make your program more responsive without waiting for a task to finish.

#### **Key Concepts:**

1. **Thread**: A thread is the smallest unit of execution in a program. A program can have multiple threads running concurrently.
    
2. **Main Thread**: The first thread that is executed when a Python program starts.
    
3. **Concurrency vs. Parallelism**:
    
    - **Concurrency**: Threads run seemingly at the same time but might not actually be executed simultaneously (due to Global Interpreter Lock in CPython).
        
    - **Parallelism**: Multiple threads or processes are executed simultaneously on different cores.
        
4. **Global Interpreter Lock (GIL)**: In CPython (the default Python implementation), only one thread can execute Python bytecode at a time. This makes threading less effective for CPU-bound tasks but useful for I/O-bound tasks.
    

#### **Important Classes and Functions**:

- **Thread**: The main class to create and manage threads.
    
    - `threading.Thread(target=your_function)`: Creates a new thread that will run the function passed as `target`.
        
    - `start()`: Starts the thread.
        
    - `join()`: Waits for the thread to finish before continuing with the main thread.
        
- **Lock**: A synchronization primitive that can be used to prevent race conditions when multiple threads try to access shared resources.
    
    - `threading.Lock()`: Creates a lock object.
        
    - `acquire()`: Acquires the lock.
        
    - `release()`: Releases the lock.
        
- **Event**: A simple way to signal between threads.
    
    - `threading.Event()`: Creates an event object.
        
    - `set()`: Signals all threads waiting on this event.
        
    - `clear()`: Resets the event.
        
- **Condition**: Used for more complex synchronization between threads.
    
    - `threading.Condition()`: Creates a condition variable.
        
    - `wait()`: Makes the thread wait until it’s notified.
        
    - `notify()`: Notifies one waiting thread.
        
    - `notify_all()`: Notifies all waiting threads.
        

#### **Simple Examples**:

1. **Basic Thread Example**:
    

```Python
import threading
import time  

def print_hello():     
	print("Hello from thread!")  # Create a new thread 
	
thread = threading.Thread(target=print_hello)  # Start the thread 
thread.start()  # Wait for the thread to complete thread.join()
	  
print("Main thread ends.")
```

2. **Using Multiple Threads**:
    

```Python
import threading
import time  

def print_hello(name):     
	time.sleep(1)     
	print(f"Hello, {name}!")  # Create two threads 
	
thread1 = threading.Thread(target=print_hello, args=("Alice",)) 
thread2 = threading.Thread(target=print_hello, args=("Bob",))  
	
# Start the threads 	
thread1.start() 
thread2.start()  
	
# Wait for both threads to complete
thread1.join() 
thread2.join()  
print("Main thread ends.")
```

3. **Using Locks to Prevent Race Conditions**:
    

```Python
import threading  
# Shared resource 
counter = 0 
lock = threading.Lock()  

def increment():     
	global counter     
	with lock:
		counter += 1         
		print(f"Counter: {counter}")  
		
# Create multiple threads 
threads = [threading.Thread(target=increment) for _ in range(5)]  

# Start the threads
for thread in threads:
	thread.start()  

# Wait for all threads to complete 
for thread in threads:     
	thread.join()  
				
	print(f"Final counter value: {counter}")
```

4. **Event Example**:
    

```Python
import threading
import time

event = threading.Event()  

def wait_for_event():
     print("Waiting for event...")     
     event.wait()  # This blocks until the event is set     
     print("Event received!")  
     
def trigger_event():     
	time.sleep(2)     
	event.set()  # This signals all waiting threads  
	
# Start the threads 
thread1 = threading.Thread(target=wait_for_event) 
thread2 = threading.Thread(target=trigger_event)  

thread1.start() 
thread2.start()  

thread1.join() 
thread2.join()
```

#### **When to Use Threading:**

- **I/O-bound tasks**: Tasks like downloading files, network requests, reading from a database, etc., are perfect candidates for threading. The threads can run concurrently without much CPU overhead.
    
- **Not ideal for CPU-bound tasks**: If your task involves heavy computations (e.g., processing data), threading might not provide a performance boost due to the GIL in CPython.

---

### **Introduction to Threading & ThreadPoolExecutor**

In Python, **threading** allows you to run multiple tasks at the same time (concurrently) in separate threads. This can be useful for I/O-bound tasks (like downloading files or interacting with a database) where the program has to wait on external resources. Instead of just waiting idly, you can have other tasks run in parallel, making the program more efficient.

`ThreadPoolExecutor` is a high-level interface for managing threads in Python. It simplifies the process of creating and managing threads, so you don't have to worry about the low-level details like manually starting, stopping, or joining threads.

### **How it Works**

- You create a `ThreadPoolExecutor` and specify how many threads it should manage.
    
- You can submit tasks (functions) to the executor, and it will run them in parallel using the available threads.
    

###  **Easy Example**

Let’s say you want to download some files, and each download can happen in parallel.

```Python
import concurrent.futures 
import time  
# A simple function that simulates downloading by sleeping for a few seconds 

def download_file(file_name):     
	print(f"Starting download of {file_name}...")     
	time.sleep(2)  # Simulates the download process by pausing the program for 2 seconds     
	print(f"Finished downloading {file_name}.")  

# Create a ThreadPoolExecutor with 3 threads 
with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:      
	# Submit multiple download tasks to the executor     
	file_names = ["file1.txt", "file2.txt", "file3.txt", "file4.txt"] 
	executor.map(download_file, file_names)
	# variable = executor.submit(function, argument optional)
	
print("All downloads complete!")
```

### **Explanation**

1. **Function**: `download_file()` simulates downloading by printing a message and sleeping for 2 seconds.
    
2. **Executor**: `ThreadPoolExecutor(max_workers=3)` creates a pool of 3 threads.
    
3. **Executor.map()**: It submits all the download tasks (one for each file) to the executor. The `map` function runs the `download_file` function on all the items in the `file_names` list, using multiple threads.
    

### **What happens when you run the code?**

- The first three downloads start simultaneously (because we have 3 threads in the pool).
    
- Once a thread finishes its download, it picks up the next task (in this case, the 4th file).
    
- The program prints "All downloads complete!" when all tasks have been finished.
    

### **Advantages of ThreadPoolExecutor**

1. **Simplicity**: It handles a lot of the complexity of working directly with threads, like starting and stopping threads.
    
2. **Efficiency**: It reuses threads instead of creating new ones for each task, which reduces overhead.
    
3. **Scalability**: You can control the number of threads based on the system's capability (e.g., `max_workers=5`).
    

### **Resume**

- **Threading**: Helps run tasks concurrently to improve efficiency, especially for I/O-bound operations.
    
- **ThreadPoolExecutor**: A simple, high-level tool in Python to manage a pool of threads for concurrent tasks.
    
- **Basic Use**: You create the executor, submit tasks (functions), and it runs them in parallel using available threads.

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]