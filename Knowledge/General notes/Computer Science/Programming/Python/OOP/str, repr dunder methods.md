## Python Dunder Methods: `__str__` and `__repr__`

## What are Dunder Methods?

"Dunder" means **double underscore**.

Examples:

```python
__str__
__repr__
__init__
```

These are special Python methods that change how objects behave.

---

# `__str__`

## Purpose

`__str__` returns a **human-friendly** string.

It is used when we print an object.

```python
print(obj)
```

Python calls:

```python
obj.__str__()
```

---

## Example

```python
class User:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"User: {self.name}"

user = User("Alice")

print(user)
```

## Output

```python
User: Alice
```

---

## Use `__str__` for

- readable text
    
- user-friendly messages
    
- logging
    
- debugging output
    

---

# `__repr__`

## Purpose

`__repr__` returns a **developer-friendly** string.

It should clearly describe the object.

Python uses it in:

```python
repr(obj)
```

and often inside lists, dictionaries, and debugging tools.

---

## Example

```python
class User:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"User(name='{self.name}')"

user = User("Alice")

print(repr(user))
```

## Output

```python
User(name='Alice')
```

---

## Use `__repr__` for

- debugging
    
- development
    
- object inspection
    
- detailed object information
    

---

# Difference Between `__str__` and `__repr__`

|Method|For|Style|
|---|---|---|
|`__str__`|Users|Readable|
|`__repr__`|Developers|Detailed|

---

# Using Both Together

```python
class User:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"User: {self.name}"

    def __repr__(self):
        return f"User(name='{self.name}')"

user = User("Alice")

print(user)
print(repr(user))
```

## Output

```python
User: Alice
User(name='Alice')
```

---

# Important Note

If `__str__` is missing, Python will use `__repr__` instead.

But if `__repr__` is missing, Python uses the default object representation like:

```python
<__main__.User object at 0x000001>
```

---

# Simple Rule

- `__str__` → for humans
    
- `__repr__` → for developers