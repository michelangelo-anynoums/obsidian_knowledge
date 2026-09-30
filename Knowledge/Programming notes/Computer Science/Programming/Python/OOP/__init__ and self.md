## **init** and **self**

`__init__` is a special method that runs when a new object is created. It is used to set up the object.

`self` refers to the current object. It lets you access its data and methods.

Example:

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def say_name(self):
        print(self.name)

dog = Dog("Rocky")
dog.say_name()
```

Here, `self.name` stores the name for that specific dog.

---
