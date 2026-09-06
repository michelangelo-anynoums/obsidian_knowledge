## Python classes and `super()` (simple explanation)

In Python, a **class** is like a blueprint for creating objects. It lets you bundle data (variables) and behavior (functions) together.

When you use **inheritance**, one class can “inherit” from another class. This means the new class can reuse and extend the old one.

### What is `super()`?

`super()` is a built-in function that lets you call methods from the **parent class** (the class you inherit from).

It is often used to:

- reuse the parent class’s code
    
- avoid rewriting the same code
    
- extend behavior instead of replacing it
    

---

## Simple example without `super()`

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed
```

Here, we repeat `self.name = name`, which is not ideal.

---

## Same example using `super()`

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # call parent class constructor
        self.breed = breed
```

### What happens here?

- `super().__init__(name)` calls the `Animal` constructor
    
- so we don’t repeat code for `self.name`
    
- then we add extra behavior (`breed`) in `Dog`
    

---

## Another example with methods

```python
class Animal:
    def speak(self):
        return "Some sound"

class Cat(Animal):
    def speak(self):
        return super().speak() + " ... meow"
```

### Result:

- Parent gives: `"Some sound"`
    
- Child adds: `" ... meow"`
    

So calling:

```python
c = Cat()
print(c.speak())
```

Output:

```
Some sound ... meow
```

---

## In short

- `super()` means: “use the parent class version of this method”
    
- It helps you **reuse code**
    
- It makes your code cleaner and easier to maintain