### ⚙️ What is `@staticmethod`?

A **static method** is a function inside a class that:

- does NOT use `self`
- does NOT use the object or class data
- works like a normal function, but stays inside the class

#### Example:

```Python
class MathTools:
    @staticmethod
    def add(a, b):
        return a + b
```

Use it like this:

```Python
result = MathTools.add(3, 5)
print(result)
```

Output:

```Python
8
```

👉 Notice: We did NOT create an object  
👉 We used the class name directly

---

### 🤔 Why use `@staticmethod`?

Use it when:

- The function is related to the class
- But it does NOT need object data (`self`)
- You want to keep your code organized

---

### 📍 Simple Real-Life Example

```Python
class Temperature:
    @staticmethod
    def celsius_to_fahrenheit(c):
        return (c * 9/5) + 32
```

Usage:

```Python
print(Temperature.celsius_to_fahrenheit(0))
```

Output:

```Python
32.0
```

👉 This function does not need any object  
👉 It just does a calculation

---

### ✅ When to Use It

Use `@staticmethod` when:

- You don’t need `self` or `cls`
- The function is helper/utility logic
- It logically belongs to the class

---

### ❌ When NOT to Use It

Do NOT use it when:

- You need to access object data → use `self`
- You need class data → use `@classmethod`

---
