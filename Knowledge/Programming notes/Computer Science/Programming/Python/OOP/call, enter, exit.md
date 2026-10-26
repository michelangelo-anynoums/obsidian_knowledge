## Python Dunder Methods: `__call__`, `__enter__`, `__exit__`

# 1. `__call__`

Makes an object behave like a function.

This allows:

```python
obj()
```

---

## Basic Example

```python
class Greeter:
    def __call__(self, name):
        return f"Hello {name}!"


g = Greeter()

print(g("Alice"))
```

### Output

```python
Hello Alice!
```

---

## What Python Actually Does

When you write:

```python
g("Alice")
```

Python internally calls:

```python
g.__call__("Alice")
```

---

## Why It’s Useful

You can create objects that:

- remember state
    
- behave like functions
    
- carry configuration
    
- cache results
    

---

## Real Example: Counter

```python
class Counter:
    def __init__(self):
        self.count = 0

    def __call__(self):
        self.count += 1
        return self.count


c = Counter()

print(c())
print(c())
print(c())
```

### Output

```python
1
2
3
```

The object acts like a function, but it also stores internal state.

---

# 2. `__enter__` and `__exit__`

These power the `with` statement.

Example:

```python
with something as value:
    ...
```

This is called a **context manager**.

---

# Why Context Managers Exist

They help safely manage resources such as:

- files
    
- database connections
    
- network sockets
    
- locks
    
- transactions
    

Python guarantees cleanup happens correctly.

---

# Simple File Example

```python
with open("data.txt") as f:
    content = f.read()
```

When the block finishes:

- the file is automatically closed
    
- even if an error occurs
    

---

# How `with` Works Internally

Python roughly transforms:

```python
with obj as value:
    print(value)
```

into something like:

```python
value = obj.__enter__()

try:
    print(value)
finally:
    obj.__exit__()
```

---

# 3. `__enter__`

Runs at the start of a `with` block.

It usually:

- opens a resource
    
- prepares something
    
- returns the object to use inside the block
    

---

## Example

```python
class DatabaseConnection:
    def __enter__(self):
        print("Opening database connection")
        return self

    def query(self):
        print("Running query")

    def __exit__(self, exc_type, exc_value, traceback):
        print("Closing database connection")


with DatabaseConnection() as db:
    db.query()
```

### Output

```python
Opening database connection
Running query
Closing database connection
```

---

# 4. `__exit__`

Runs when leaving the `with` block.

It usually:

- closes resources
    
- cleans up
    
- handles exceptions
    

---

## Parameters of `__exit__`

```python
def __exit__(self, exc_type, exc_value, traceback):
```

These contain exception information if an error happened inside the block.

---

# Example with Error Handling

```python
class SafeRunner:
    def __enter__(self):
        print("Start")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Cleanup")

        if exc_type:
            print("An error occurred:", exc_value)

        return True


with SafeRunner():
    1 / 0

print("Program continues")
```

### Output

```python
Start
Cleanup
An error occurred: division by zero
Program continues
```

---

# Important Detail

Returning:

```python
True
```

from `__exit__` tells Python:

> “I handled the exception.”

So the program does not crash.

If you return `False` or nothing, the exception continues normally.

---

# Mental Model

|Syntax You Write|Python Internally Calls|
|---|---|
|`obj()`|`obj.__call__()`|
|`with obj:`|`obj.__enter__()` then `obj.__exit__()`|

---

# Real-World Examples

## `__call__`

Used in:

- decorators
    
- machine learning models
    
- FastAPI dependency objects
    
- callable services
    
- validators
    

PyTorch models often work like this:

```python
prediction = model(data)
```

even though `model` is actually an object.

---

## `__enter__` / `__exit__`

Used in:

- `open()`
    
- database transactions
    
- thread locks
    
- testing frameworks
    
- temporary files
    

Example:

```python
with lock:
    critical_code()
```

---

# Tiny Summary

|Dunder Method|Purpose|
|---|---|
|`__call__`|Makes objects callable like functions|
|`__enter__`|Runs at start of `with`|
|`__exit__`|Runs at end of `with`|

These methods help make Python APIs feel clean and natural.

---
