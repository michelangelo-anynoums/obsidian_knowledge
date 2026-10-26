**Class vs Instance Attributes**

_Attributes_ are variables inside a class.

- _Class attributes_ belong to the whole class (shared by all objects).
    
- _Instance attributes_ belong to each individual object.
    

Example:

```python
class Dog:
    species = "Canine"   # class attribute

    def __init__(self, name):
        self.name = name   # instance attribute

dog1 = Dog("Max")
dog2 = Dog("Bella")
```

Both dogs share `species`, but each has its own `name`.

---
