**Polymorphism** is a concept in Python object-oriented programming (OOP) that means “many forms.” It allows different classes to use the same method name, but each class can have its own way of performing that method.

In simple terms, polymorphism lets you write code that works with different objects in a similar way, even if those objects behave differently.

### Example 1: Different classes, same method name

```python
class Dog:
    def speak(self):
        return "Woof"

class Cat:
    def speak(self):
        return "Meow"

animals = [Dog(), Cat()]

for animal in animals:
    print(animal.speak())
```

Output:

```
Woof
Meow
```

Here, both `Dog` and `Cat` have a method called `speak()`, but they behave differently. The loop does not need to know what type of animal it is using.

### Example 2: Using inheritance (method overriding)

```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):
        return "Woof"

class Cat(Animal):
    def speak(self):
        return "Meow"

animals = [Animal(), Dog(), Cat()]

for animal in animals:
    print(animal.speak())
```

Output:

```
Some sound
Woof
Meow
```

In this example, `Dog` and `Cat` override the `speak()` method from the parent `Animal` class. This is another way polymorphism is used in Python.

### Why polymorphism is useful

Polymorphism makes your code:

- More flexible
    
- Easier to read
    
- Easier to extend
    

You can add new classes with the same method names, and your existing code will still work without changes.

---
