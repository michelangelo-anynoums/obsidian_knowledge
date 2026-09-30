## Python `@property` Decorator (Simple Explanation)

The `@property` decorator in Python lets you turn a method into something that behaves like an attribute (a variable). This means you can access it using dot notation, without parentheses.

### Why use `@property`?

It helps you:

- Control how attributes are accessed or modified
    
- Add logic (like validation or calculations)
    
- Keep your code clean and readable
    

---

## Basic Example

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    @property
    def diameter(self):
        return self.radius * 2
```

### How to use it:

```python
c = Circle(5)
print(c.diameter)  # 10 (no parentheses!)
```

Even though `diameter` is a method, you use it like an attribute.

---

## Adding a Setter

You can also control how a value is set using a setter:

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value
```

### Usage:

```python
c = Circle(5)
c.radius = 10   # works
c.radius = -3   # raises error
```

---

## Adding a Deleter

A deleter lets you define what happens when someone tries to delete the attribute using `del`.

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value

    @radius.deleter
    def radius(self):
        print("Deleting radius...")
        del self._radius
```

### Usage:

```python
c = Circle(5)
del c.radius  # prints "Deleting radius..."
```

After deletion, trying to access `c.radius` will raise an error because `_radius` no longer exists.

---
## Quick Summary

- Turns a method into an attribute
    
- Can add setter and deleter for full control
    
- Makes your code cleaner and safer
    

---
