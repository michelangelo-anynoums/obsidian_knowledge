Here’s a concise Obsidian-style note about `@classmethod` in Python.

# `@classmethod` in Python

## What is `@classmethod`?

`@classmethod` is a decorator used to define a method that belongs to the **class itself**, not to a specific instance of the class.

Instead of receiving `self`, a class method receives `cls` as its first parameter.

---

## Basic Syntax

```python
class MyClass:

    @classmethod
    def my_method(cls):
        print(cls)
```

- `cls` → reference to the class
    
- Can access and modify **class variables**
    
- Can create alternative constructors
    

---

## Example 1 — Accessing Class Variables

```python
class User:
    platform = "Python App"

    @classmethod
    def show_platform(cls):
        print(cls.platform)

User.show_platform()
```

### Output

```python
Python App
```

---

## Example 2 — Alternative Constructor

A common use of `@classmethod` is creating objects in different ways.

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, data):
        name, age = data.split(",")
        return cls(name, int(age))


p1 = Person.from_string("Alice,25")

print(p1.name)
print(p1.age)
```

### Output

```python
Alice
25
```

---

# Important Concepts

## `self` vs `cls`

|Keyword|Refers To|
|---|---|
|`self`|Object instance|
|`cls`|The class itself|

---

## When to Use `@classmethod`

Use it when you need to:

- Work with class-level data
    
- Create factory methods
    
- Build alternative constructors
    
- Modify shared class state
    

---

## Difference from `@staticmethod`

|Feature|`@classmethod`|`@staticmethod`|
|---|---|---|
|Receives class reference|Yes (`cls`)|No|
|Can access class variables|Yes|No|
|Can modify class state|Yes|No|

---

## Key Idea

- Instance methods → work with objects (`self`)
    
- Class methods → work with the class (`cls`)
    
- Static methods → utility functions inside a class
    

---