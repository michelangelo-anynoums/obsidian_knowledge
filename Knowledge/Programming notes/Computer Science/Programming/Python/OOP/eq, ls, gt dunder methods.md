## Python OOP Notes: `__eq__`, `__lt__`, `__gt__`

These special methods are called **dunder methods** ("double underscore" methods).  
They allow custom Python objects to behave like built-in types during comparisons.

---

# 1. `__eq__` → Equality (`==`)

The `__eq__` method defines how two objects are compared using `==`.

## Example

```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __eq__(self, other):
        return self.age == other.age


u1 = User("Alice", 25)
u2 = User("Bob", 25)

print(u1 == u2)   # True
```

## Explanation

- Python calls:
    

```python
u1.__eq__(u2)
```

- The comparison logic is fully customizable.
    
- In this example, users are considered equal if their ages are equal.
    

## Important Note

Without `__eq__`, objects are compared by memory address.

```python
class A:
    pass

x = A()
y = A()

print(x == y)   # False
```

---

# 2. `__lt__` → Less Than (`<`)

The `__lt__` method defines behavior for the `<` operator.

## Example

```python
class Product:
    def __init__(self, price):
        self.price = price

    def __lt__(self, other):
        return self.price < other.price


p1 = Product(50)
p2 = Product(100)

print(p1 < p2)   # True
```

## Explanation

Python internally calls:

```python
p1.__lt__(p2)
```

This is useful for:

- sorting
    
- ranking
    
- priority systems
    
- custom comparisons
    

## Sorting Example

```python
products = [Product(300), Product(100), Product(200)]

products.sort()

for p in products:
    print(p.price)
```

Output:

```python
100
200
300
```

---

# 3. `__gt__` → Greater Than (`>`)

The `__gt__` method defines behavior for the `>` operator.

## Example

```python
class Score:
    def __init__(self, points):
        self.points = points

    def __gt__(self, other):
        return self.points > other.points


s1 = Score(90)
s2 = Score(75)

print(s1 > s2)   # True
```

## Explanation

Python calls:

```python
s1.__gt__(s2)
```

This method is commonly used when comparing:

- scores
    
- prices
    
- priorities
    
- sizes
    
- dates
    

---

# Combined Example

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def __eq__(self, other):
        return self.grade == other.grade

    def __lt__(self, other):
        return self.grade < other.grade

    def __gt__(self, other):
        return self.grade > other.grade


a = Student("Anna", 80)
b = Student("Tom", 90)

print(a == b)   # False
print(a < b)    # True
print(a > b)    # False
```

---

# Quick Summary

|Method|Operator|Meaning|
|---|---|---|
|`__eq__`|`==`|Equal to|
|`__lt__`|`<`|Less than|
|`__gt__`|`>`|Greater than|

---

# Best Practice

When implementing comparison methods:

- compare the same type of objects
    
- use meaningful attributes
    
- return `True` or `False`
    
- keep logic simple and predictable
    

Often developers also use:

```python
from functools import total_ordering
```

to automatically generate missing comparison methods.