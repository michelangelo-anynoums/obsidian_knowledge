## Python `random` Module

## What is `random`?

The `random` module is used to generate random values.

You can use it for:

- games
    
- passwords
    
- simulations
    
- random choices
    
- testing
    

---

# Importing the Module

```python
import random
```

---

# `random.random()`

## Purpose

Returns a random float between `0` and `1`.

## Example

```python
import random

print(random.random())
```

## Output Example

```python
0.48372
```

---

# `random.randint()`

## Purpose

Returns a random integer between two numbers.

Both numbers are included.

## Example

```python
import random

print(random.randint(1, 10))
```

## Output Example

```python
7
```

---

# `random.randrange()`

## Purpose

Returns a random number from a range.

Works like `range()`.

## Example

```python
import random

print(random.randrange(0, 20, 2))
```

## Output Example

```python
14
```

---

# `random.choice()`

## Purpose

Returns one random item from a list.

## Example

```python
import random

colors = ["red", "blue", "green"]

print(random.choice(colors))
```

## Output Example

```python
blue
```

---

# `random.choices()`

## Purpose

Returns multiple random items.

## Example

```python
import random

names = ["Alice", "Bob", "Charlie"]

print(random.choices(names, k=2))
```

## Output Example

```python
['Bob', 'Alice']
```

---

# `random.shuffle()`

## Purpose

Shuffles a list in place.

## Example

```python
import random

numbers = [1, 2, 3, 4, 5]

random.shuffle(numbers)

print(numbers)
```

## Output Example

```python
[3, 1, 5, 2, 4]
```

---

# `random.uniform()`

## Purpose

Returns a random float between two numbers.

## Example

```python
import random

print(random.uniform(1, 5))
```

## Output Example

```python
3.67
```

---

# `random.seed()`

## Purpose

Makes random results repeatable.

Useful for testing.

## Example

```python
import random

random.seed(1)

print(random.randint(1, 10))
```

## Output

```python
3
```

Running the code again gives the same result.

---

# Common Methods Summary

|Method|Description|
|---|---|
|`random()`|Random float from `0` to `1`|
|`randint(a, b)`|Random integer|
|`randrange()`|Random number from range|
|`choice()`|One random item|
|`choices()`|Multiple random items|
|`shuffle()`|Shuffle a list|
|`uniform()`|Random float in range|
|`seed()`|Repeatable randomness|

---

# Simple Notes

- `choice()` → one item
    
- `choices()` → multiple items
    
- `shuffle()` changes the original list
    
- `seed()` is useful for testing