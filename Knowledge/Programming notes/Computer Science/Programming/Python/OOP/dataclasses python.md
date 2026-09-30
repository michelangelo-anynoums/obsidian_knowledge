# Python Dataclasses

## What Are Dataclasses?

A **dataclass** is a special type of class introduced in Python 3.7 through the `dataclasses` module.

Dataclasses are designed to make classes that mainly store data:

- shorter
    
- cleaner
    
- easier to read
    
- easier to maintain
    

Instead of writing repetitive boilerplate code like:

- `__init__`
    
- `__repr__`
    
- `__eq__`
    

Python can generate them automatically.

---

# Why Python Provides `dataclasses`

Before dataclasses, simple classes often required lots of repetitive code.

Example without dataclass:

```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"User(name={self.name}, age={self.age})"

    def __eq__(self, other):
        return self.name == other.name and self.age == other.age
```

This becomes repetitive quickly.

Dataclasses solve this problem.

---

# Creating Your First Dataclass

Import the decorator:

```python
from dataclasses import dataclass
```

Basic example:

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
```

Usage:

```python
user = User("Alice", 25)

print(user)
```

Output:

```python
User(name='Alice', age=25)
```

Very little code, but Python automatically created useful methods.

---

# Automatic Method Generation

When using `@dataclass`, Python automatically creates several methods.

---

## `__init__`

Creates the constructor automatically.

You can do:

```python
user = User("Alice", 25)
```

instead of manually writing:

```python
def __init__(self, name, age):
    self.name = name
    self.age = age
```

---

## `__repr__`

Provides a readable string representation.

```python
print(user)
```

Output:

```python
User(name='Alice', age=25)
```

Helpful for:

- debugging
    
- logging
    
- inspecting objects
    

---

## `__eq__`

Allows object comparison.

Example:

```python
u1 = User("Alice", 25)
u2 = User("Alice", 25)

print(u1 == u2)
```

Output:

```python
True
```

Without dataclasses, objects compare by memory address by default.

---

# Dataclass Options

---

## `frozen=True`

Makes the object immutable (read-only).

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Point:
    x: int
    y: int
```

Usage:

```python
p = Point(1, 2)

p.x = 10
```

Output:

```python
FrozenInstanceError
```

Useful for:

- constants
    
- configuration objects
    
- safe immutable data
    

---

## `order=True`

Automatically creates comparison methods.

```python
from dataclasses import dataclass

@dataclass(order=True)
class Product:
    price: float
    name: str
```

Example:

```python
p1 = Product(10.0, "Book")
p2 = Product(20.0, "Laptop")

print(p1 < p2)
```

Output:

```python
True
```

Python generates:

- `__lt__`
    
- `__le__`
    
- `__gt__`
    
- `__ge__`
    

---

## `slots=True`

Reduces memory usage and improves performance.

```python
from dataclasses import dataclass

@dataclass(slots=True)
class Player:
    name: str
    level: int
```

Benefits:

- less memory
    
- faster attribute access
    
- prevents accidental new attributes
    

Example:

```python
p = Player("Hero", 10)

p.health = 100
```

Output:

```python
AttributeError
```

Use `slots=True` when creating many objects.

---

# Default Values

You can provide default values directly.

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    active: bool = True
```

Usage:

```python
u = User("Alice")

print(u)
```

Output:

```python
User(name='Alice', active=True)
```

---

# Using `field()`

`field()` gives more control over dataclass fields.

Import:

```python
from dataclasses import field
```

Example:

```python
from dataclasses import dataclass, field

@dataclass
class Product:
    name: str
    price: float
    tags: list = field(default_factory=list)
```

`field()` is commonly used for:

- `default_factory`
    
- excluding fields from comparisons
    
- metadata
    
- controlling initialization
    

---

# `default_factory`

Never use mutable objects like lists or dictionaries directly as defaults.

Bad example:

```python
@dataclass
class BadExample:
    items: list = []
```

This can create shared data between objects.

Correct approach:

```python
from dataclasses import dataclass, field

@dataclass
class GoodExample:
    items: list = field(default_factory=list)
```

Each object gets its own list.

Example:

```python
a = GoodExample()
b = GoodExample()

a.items.append("apple")

print(a.items)
print(b.items)
```

Output:

```python
['apple']
[]
```

---

# Type Hints in Dataclasses

Dataclasses work closely with type hints.

Example:

```python
@dataclass
class Book:
    title: str
    pages: int
    price: float
```

Common types:

```python
str
int
float
bool
list
dict
tuple
```

Using `typing`:

```python
from typing import List

@dataclass
class Inventory:
    items: List[str]
```

Benefits:

- better readability
    
- IDE support
    
- autocomplete
    
- static type checking
    

---

# Converting Dataclasses to Dictionaries

Use `asdict()`.

```python
from dataclasses import dataclass, asdict

@dataclass
class User:
    name: str
    age: int

u = User("Alice", 25)

data = asdict(u)

print(data)
```

Output:

```python
{
    'name': 'Alice',
    'age': 25
}
```

Useful for:

- JSON conversion
    
- APIs
    
- serialization
    
- configuration export
    

---

# When To Use What?

---

## Normal Classes

Use when:

- you need complex behavior
    
- many custom methods
    
- heavy logic
    
- advanced inheritance
    
- custom property management
    

Example:

```python
class BankAccount:
    def deposit(self):
        pass

    def withdraw(self):
        pass
```

---

## Dataclasses

Use when:

- storing structured data
    
- you want cleaner code
    
- you still need methods
    
- readability matters
    

Great balance between simplicity and flexibility.

---

## Namedtuples

Use when:

- data is very small/simple
    
- immutability is desired
    
- minimal functionality is needed
    

Example:

```python
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])
```

Good for lightweight data containers.

---

# Practice Project 1 — Inventory System

```python
from dataclasses import dataclass

@dataclass
class Item:
    name: str
    price: float
    quantity: int

    def total_value(self):
        return self.price * self.quantity


item = Item("Keyboard", 50.0, 3)

print(item.total_value())
```

Output:

```python
150.0
```

---

# Practice Project 2 — Game Character Stats

```python
from dataclasses import dataclass

@dataclass
class Character:
    name: str
    health: int
    mana: int
    level: int = 1

    def level_up(self):
        self.level += 1
        self.health += 10
        self.mana += 5


hero = Character("Knight", 100, 50)

hero.level_up()

print(hero)
```

Output:

```python
Character(name='Knight', health=110, mana=55, level=2)
```

---

# Practice Project 3 — Banking Model

```python
from dataclasses import dataclass

@dataclass
class BankAccount:
    owner: str
    balance: float = 0

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient funds")
            return

        self.balance -= amount


account = BankAccount("Alice")

account.deposit(100)
account.withdraw(30)

print(account.balance)
```

Output:

```python
70
```

---

# Practice Project 4 — Configuration Object

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class AppConfig:
    app_name: str
    version: str
    debug: bool = False


config = AppConfig(
    app_name="MyApp",
    version="1.0"
)

print(config)
```

Configuration objects are often immutable.

---

# Important Notes

- Dataclasses reduce boilerplate code.
    
- They are best for data-focused classes.
    
- Type hints are strongly recommended.
    
- Use `default_factory` for mutable defaults.
    
- `frozen=True` creates immutable objects.
    
- `slots=True` can improve memory efficiency.
    
- Dataclasses can still contain methods.
    

---

# Common Beginner Mistakes

## Forgetting Type Hints

Wrong:

```python
@dataclass
class User:
    name = ""
```

Correct:

```python
@dataclass
class User:
    name: str
```

---

## Using Mutable Defaults Incorrectly

Wrong:

```python
items: list = []
```

Correct:

```python
items: list = field(default_factory=list)
```

---

## Thinking Dataclasses Replace All Classes

Dataclasses are excellent for storing data, but normal classes are still better for complex behavior-heavy systems.

---

# Summary

Dataclasses are one of Python’s most useful modern features.

They help you:

- write less code
    
- create cleaner classes
    
- improve readability
    
- automatically generate common methods
    

Core concepts to remember:

- `@dataclass`
    
- automatic `__init__`
    
- automatic `__repr__`
    
- automatic `__eq__`
    
- `frozen=True`
    
- `order=True`
    
- `slots=True`
    
- `field()`
    
- `default_factory`
    
- `asdict()`
    

Dataclasses are widely used in:

- backend systems
    
- APIs
    
- game development
    
- configuration systems
    
- data models
    
- automation scripts
    
- machine learning pipelines
    

They are an essential Python tool worth mastering.