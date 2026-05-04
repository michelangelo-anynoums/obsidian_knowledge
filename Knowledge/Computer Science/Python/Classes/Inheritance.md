**Inheritance**

_Inheritance_ means one class can use code from another class. This helps avoid repeating code.

The new class (child) gets features from the existing class (parent).

Example:

```python
class Animal:
    def speak(self):
        print("Some sound")

class Dog(Animal):   # Dog inherits from Animal
    def bark(self):
        print("Woof")

my_dog = Dog()
my_dog.speak()  # inherited method
my_dog.bark()   # its own method
```

`Dog` can use both its own methods and those from `Animal`.

---
