## Python Dunder Methods for Containers and Iterables

## 1. `__len__`

Controls what happens when you call:

```python
len(obj)
```

### Example

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __len__(self):
        return len(self.songs)


p = Playlist(["Song A", "Song B", "Song C"])

print(len(p))
```

### Output

```python
3
```

### Why it matters

Without `__len__`, `len(p)` would fail.

This method tells Python:

> “Here is how many items this object contains.”

---

# 2. `__getitem__`

Controls access using square brackets:

```python
obj[index]
```

### Example

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __getitem__(self, index):
        return self.songs[index]


p = Playlist(["Song A", "Song B", "Song C"])

print(p[0])
print(p[1])
```

### Output

```python
Song A
Song B
```

### Why it matters

This makes your object behave like a list.

Python internally translates:

```python
p[0]
```

into:

```python
p.__getitem__(0)
```

---

# 3. `__setitem__`

Controls assignment using square brackets:

```python
obj[index] = value
```

### Example

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __setitem__(self, index, value):
        self.songs[index] = value


p = Playlist(["Song A", "Song B"])

p[1] = "New Song"

print(p.songs)
```

### Output

```python
['Song A', 'New Song']
```

### Why it matters

Python internally converts:

```python
p[1] = "New Song"
```

into:

```python
p.__setitem__(1, "New Song")
```

This lets your objects support item updates like lists or dictionaries.

---

# 4. `__iter__`

Makes your object iterable in loops.

This enables:

```python
for item in obj:
```

### Example

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __iter__(self):
        return iter(self.songs)


p = Playlist(["Song A", "Song B", "Song C"])

for song in p:
    print(song)
```

### Output

```python
Song A
Song B
Song C
```

### Why it matters

Without `__iter__`, a `for` loop would not know how to go through your object.

Python internally does something like:

```python
iterator = p.__iter__()
```

---

# Putting It All Together

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __len__(self):
        return len(self.songs)

    def __getitem__(self, index):
        return self.songs[index]

    def __setitem__(self, index, value):
        self.songs[index] = value

    def __iter__(self):
        return iter(self.songs)


p = Playlist(["A", "B", "C"])

print(len(p))      # 3
print(p[0])        # A

p[1] = "NEW"

for song in p:
    print(song)
```

---

# Mental Model

Think of these methods as hooks Python calls automatically.

|Syntax You Write|Python Actually Calls|
|---|---|
|`len(obj)`|`obj.__len__()`|
|`obj[0]`|`obj.__getitem__(0)`|
|`obj[0] = x`|`obj.__setitem__(0, x)`|
|`for x in obj`|`obj.__iter__()`|

---

# Real-World Use Cases

These methods are useful when building:

- custom collections
    
- caches
    
- database result wrappers
    
- tensor libraries
    
- data structures
    
- ORM models
    
- configuration containers
    

Examples:

- Pandas DataFrames
    
- NumPy arrays
    
- PyTorch tensors
    

all implement many dunder methods to feel “native” in Python.

---

# Bonus Tip

If a class implements both:

```python
__len__
__getitem__
```

Python can often iterate over it automatically even without `__iter__`.

Example:

```python
class Numbers:
    def __getitem__(self, index):
        if index < 5:
            return index
        raise IndexError


n = Numbers()

for x in n:
    print(x)
```

Output:

```python
0
1
2
3
4
```

Python keeps calling `__getitem__` with increasing indexes until `IndexError` happens.

---
