**Encapsulation in Python is the idea of combining data** (attributes) and the methods that operate on that data into a single unit, usually a class. It also involves restricting direct access to some of an object's components, which helps protect its internal state and **ensures that it is only modified in controlled ways.**

Here is a **simple** example:

```Python
class Person:  
def __init__(self, name, age):  
self.name = name # public attribute  
self._age = age # "protected" (convention)


def display(self):
    return f"{self.name} is {self._age} years old"


p = Person("Alice", 30)  
print(p.name) # accessible  
print(p._age) # accessible, but intended for internal use
```

A more **encapsulated version** uses a private attribute and controlled access:

```Python
class BankAccount:  
def __init__(self, balance):  
self.__balance = balance # private attribute

def deposit(self, amount):
    if amount > 0:
        self.__balance += amount

def withdraw(self, amount):
    if 0 < amount <= self.__balance:
        self.__balance -= amount

def get_balance(self):
    return self.__balance

account = BankAccount(1000)  
account.deposit(500)  
account.withdraw(200)

print(account.get_balance()) # correct way to access balance


 
print(account.__balance) # would raise an AttributeErro=r
```

In this second example, the balance **cannot be accessed or modified directly from outside the class.** Instead, it must go through methods like deposit() and withdraw(), which enforce rules (e.g., no negative deposits, no overdrawing).

**Encapsulation** improves code reliability and maintainability by preventing **unintended changes** to an object’s data and by clearly defining how that data should be accessed and modified.

---
