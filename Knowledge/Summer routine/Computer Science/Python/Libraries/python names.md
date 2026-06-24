**# Python Built-in Variables & Constants**

**Obsidian Note** – Essentials for quick reference

---

## Core Built-in Constants

|Variable|Type|Value / Description|Common Use|
|---|---|---|---|
|True|bool|True|Boolean logic, flags|
|False|bool|False|Boolean logic, flags|
|None|NoneType|None (null / no value)|Default returns, optional values|
|__debug__|bool|True in normal mode, False with -O flag|Debug assertions|

---

## Special Module-Level Variables (Dunders)

These are automatically available in every module.

| Variable      | Description                                         |
| ------------- | --------------------------------------------------- |
| `__name__`    | Name of current module ('__main__' if run directly) |
| `__doc__`     | Module / function / class docstring                 |
| `__file__`    | Path to the current Python file                     |
| `__package__` | Package name the module belongs to                  |
| `__path__`    | List of directories for packages                    |
| `__version__` | Conventional variable for library version           |
| `__author__`  | Common metadata variable                            |

---

## Most Useful Built-in Special Variables (Inside Functions/Classes)

| Variable          | Context           | Meaning                                        |
| ----------------- | ----------------- | ---------------------------------------------- |
| `__dict__`        | objects           | Dictionary of writable attributes              |
| `__class__`       | instances         | Class the instance belongs to                  |
| `__name__`        | functions/classes | Name of the function/class                     |
| `__qualname__`    | functions/classes | Qualified name (with class path)               |
| `__module__`      | classes/functions | Module where defined                           |
| `__annotations__` | functions/classes | Type hints dictionary                          |
| `__slots__`       | classes           | Memory optimization (tuple of attribute names) |

---

## Top Built-in Functions You Treat Like Variables

(Technically functions, but used constantly)

Python

```Python
dir()          # list attributes
vars()         # __dict__ equivalent
locals()       # local variables dict
globals()      # global variables dict
type(obj)      # get type
id(obj)        # memory address
len(obj)       # length
repr(obj)      # official string representation
```

---

## Quick Usage Examples (Obsidian-friendly)

Python

```Python
# 1. Entry point check (most common)
if __name__ == "__main__":
    main()

# 2. None as default
def get_user(user_id: int = None):
    return None if user_id is None else fetch(user_id)

# 3. Debug guard
if __debug__:
    assert some_condition, "This should never happen"
```

---
