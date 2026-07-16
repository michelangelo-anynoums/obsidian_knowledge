## Python Object Lifecycle — `__new__`, `__init__`, and `__del__`

#python #oop #dunder-methods #memory-management #notes

---

# Python Object Lifecycle

When you create an object in Python:

```python
obj = MyClass()
```

Python internally performs several steps:

1. Allocate memory for the object
    
2. Create the object instance
    
3. Initialize the object
    
4. Eventually destroy the object
    

Three important dunder methods participate in this lifecycle:

|Method|Purpose|
|---|---|
|`__new__`|Creates the object|
|`__init__`|Initializes the object|
|`__del__`|Cleanup before destruction|

---

# `__new__` — Object Creation

## Purpose

`__new__` is responsible for **creating and returning a new instance** of a class.

It is called **before** `__init__`.

---

## Signature

```python
def __new__(cls, *args, **kwargs):
    ...
```

- `cls` → class itself (not instance)
    
- Must return an object instance
    
- Usually returns `super().__new__(cls)`
    

---

## Basic Example

```python
class User:
    def __new__(cls):
        print("Creating instance...")
        return super().__new__(cls)

    def __init__(self):
        print("Initializing instance...")


u = User()
```

## Output

```python
Creating instance...
Initializing instance...
```

---

# Important Difference

|Method|Receives|Responsibility|
|---|---|---|
|`__new__`|class (`cls`)|Create object|
|`__init__`|instance (`self`)|Configure object|

---

# Why Use `__new__`?

Most Python developers rarely override `__new__`.

It becomes useful when:

- Creating immutable objects
    
- Implementing Singleton pattern
    
- Custom object creation logic
    
- Subclassing immutable built-ins (`str`, `tuple`, `int`)
    
- Object caching/flyweight patterns
    

---

# Example — Immutable Type

Since `str` is immutable, customization must happen in `__new__`.

```python
class UpperString(str):
    def __new__(cls, value):
        value = value.upper()
        return super().__new__(cls, value)


s = UpperString("hello")

print(s)
```

## Output

```python
HELLO
```

---

# Example — Singleton Pattern

```python
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            print("Creating new instance")
            cls._instance = super().__new__(cls)

        return cls._instance


db1 = Database()
db2 = Database()

print(db1 is db2)
```

## Output

```python
Creating new instance
True
```

---

# `__init__` — Object Initialization

## Purpose

`__init__` initializes an already-created object.

This is where you typically:

- assign attributes
    
- validate data
    
- prepare state
    
- inject dependencies
    

---

## Signature

```python
def __init__(self, *args, **kwargs):
    ...
```

- `self` is the instance
    
- Must return `None`
    
- Returning anything else raises an error
    

---

# Basic Example

```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age


u = User("Alice", 30)

print(u.name)
print(u.age)
```

## Output

```python
Alice
30
```

---

# Common Mistake

## ❌ Returning a value from `__init__`

```python
class Bad:
    def __init__(self):
        return {}
```

## Error

```python
TypeError: __init__() should return None, not 'dict'
```

---

# Flow Between `__new__` and `__init__`

## Internal Process

```python
obj = MyClass()
```

Roughly becomes:

```python
obj = MyClass.__new__(MyClass)

if isinstance(obj, MyClass):
    MyClass.__init__(obj)
```

---

# Important Behavior

If `__new__` does NOT return an instance of the class:

- `__init__` is never called
    

Example:

```python
class Example:
    def __new__(cls):
        return "not an object"

    def __init__(self):
        print("Will never run")


e = Example()

print(e)
```

## Output

```python
not an object
```

---

# `__del__` — Object Destruction

## Purpose

`__del__` is called when an object is about to be destroyed by the garbage collector.

Think of it as a finalizer/destructor.

---

## Signature

```python
def __del__(self):
    ...
```

---

# Basic Example

```python
class FileHandler:
    def __init__(self, filename):
        self.file = open(filename, "w")

    def __del__(self):
        print("Closing file")
        self.file.close()


f = FileHandler("demo.txt")
del f
```

---

# Important Reality About `__del__`

`__del__` is NOT deterministic.

You cannot reliably predict when it runs.

Reasons:

- Garbage collection timing
    
- Circular references
    
- Interpreter shutdown
    
- Different Python implementations
    

---

# Why `__del__` Is Often Avoided

Using `__del__` can create subtle bugs:

- resource leaks
    
- deadlocks
    
- shutdown errors
    
- circular-reference issues
    

---

# Recommended Alternative

Use context managers (`with` statement).

## Better Approach

```python
with open("demo.txt", "w") as f:
    f.write("hello")
```

This guarantees cleanup.

---

# Object Lifecycle Visualization

```text
Class() call
    │
    ▼
__new__()
    │
    ▼
object created
    │
    ▼
__init__()
    │
    ▼
object usable
    │
    ▼
garbage collection
    │
    ▼
__del__()
```

---

# Practical Rules

## Use `__init__` for:

- normal attribute setup
    
- dependency injection
    
- validation
    
- configuration
    

---

## Use `__new__` only when:

- subclassing immutable types
    
- implementing Singleton/factory patterns
    
- controlling instance creation
    

---

## Avoid `__del__` unless:

- absolutely necessary
    
- dealing with low-level resources
    
- integrating with external systems
    

Prefer:

- context managers
    
- `weakref.finalize`
    
- explicit cleanup methods
    

---

# Real-World Example Combining `__new__` and `__init__`

```python
class Logger:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            print("Allocating logger")
            cls._instance = super().__new__(cls)

        return cls._instance

    def __init__(self):
        print("Initializing logger")


l1 = Logger()
l2 = Logger()
```

## Output

```python
Allocating logger
Initializing logger
Initializing logger
```

---

# Important Observation

Even though only ONE instance exists:

```python
__init__()
```

still runs every time the class is called.

This is a common Singleton pitfall.

---

# Prevent Reinitialization

```python
class Logger:
    _instance = None
    _initialized = False

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)

        return cls._instance

    def __init__(self):
        if not self._initialized:
            print("Run once")
            self._initialized = True
```

---

# Interview-Style Summary

## `__new__`

- creates object
    
- static-like behavior
    
- returns instance
    
- runs before `__init__`
    

---

## `__init__`

- initializes object
    
- receives instance
    
- returns `None`
    
- runs after `__new__`
    

---

## `__del__`

- cleanup hook
    
- called before destruction
    
- unreliable timing
    
- avoid for critical cleanup
    

---

# TL;DR

|Method|Main Job|Returns|
|---|---|---|
|`__new__`|Create instance|object|
|`__init__`|Initialize instance|`None`|
|`__del__`|Cleanup before deletion|`None`|

---
