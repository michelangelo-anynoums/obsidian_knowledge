## Python OOP Notes: `__add__`, `__sub__`, `__mul__`

These dunder methods allow custom Python objects to work with mathematical operators such as:

- `+`
    
- `-`
    
- `*`
    

They are part of **operator overloading** in Python.

---

# 1. `__add__` → Addition (`+`)

The `__add__` method defines behavior for the `+` operator.

## Example

```python
class Wallet:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        return Wallet(self.amount + other.amount)


w1 = Wallet(100)
w2 = Wallet(50)

result = w1 + w2

print(result.amount)   # 150
```

## Explanation

Python internally calls:

```python
w1.__add__(w2)
```

The method returns a new object with the combined value.

## Important Note

Usually, `__add__` should return:

- a new object
    
- not modify the original object
    

---

# 2. `__sub__` → Subtraction (`-`)

The `__sub__` method defines behavior for the `-` operator.

## Example

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def __sub__(self, other):
        return BankAccount(self.balance - other.balance)


a1 = BankAccount(500)
a2 = BankAccount(120)

result = a1 - a2

print(result.balance)   # 380
```

## Explanation

Python calls:

```python
a1.__sub__(a2)
```

This method is useful for:

- balances
    
- points
    
- vectors
    
- measurements
    

---

# 3. `__mul__` → Multiplication (`*`)

The `__mul__` method defines behavior for the `*` operator.

## Example

```python
class Box:
    def __init__(self, value):
        self.value = value

    def __mul__(self, other):
        return Box(self.value * other.value)


b1 = Box(4)
b2 = Box(5)

result = b1 * b2

print(result.value)   # 20
```

## Explanation

Python internally calls:

```python
b1.__mul__(b2)
```

This method can represent:

- scaling
    
- repeated values
    
- vector math
    
- matrix operations
    

---

# Combined Example

```python
class Vector:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return Vector(self.value + other.value)

    def __sub__(self, other):
        return Vector(self.value - other.value)

    def __mul__(self, other):
        return Vector(self.value * other.value)


v1 = Vector(10)
v2 = Vector(3)

print((v1 + v2).value)   # 13
print((v1 - v2).value)   # 7
print((v1 * v2).value)   # 30
```

---

# Quick Summary

|Method|Operator|Meaning|
|---|---|---|
|`__add__`|`+`|Addition|
|`__sub__`|`-`|Subtraction|
|`__mul__`|`*`|Multiplication|

---

# Best Practice

When implementing arithmetic dunder methods:

- return a new object
    
- avoid modifying existing objects
    
- validate input types if needed
    
- keep operations predictable
    

Example with type checking:

```python
def __add__(self, other):
    if not isinstance(other, Wallet):
        return NotImplemented

    return Wallet(self.amount + other.amount)
```

Returning `NotImplemented` allows Python to handle unsupported operations correctly.