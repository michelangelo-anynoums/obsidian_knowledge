**Python Built-in Methods for Number Base Conversion**

Python provides several simple and efficient built-in functions to convert integers into different number bases such as binary, hexadecimal, and octal.

### 1. Binary Conversion

- Use the `bin()` function.
    
- Returns a string prefixed with `'0b'`.
    

```python
bin(10)   # Output: '0b1010'
```

- To remove the prefix:
    

```python
bin(10)[2:]   # Output: '1010'
```

### 2. Hexadecimal Conversion

- Use the `hex()` function.
    
- Returns a string prefixed with `'0x'`.
    

```python
hex(255)   # Output: '0xff'
```

- Without prefix:
    

```python
hex(255)[2:]   # Output: 'ff'
```

### 3. Octal Conversion

- Use the `oct()` function.
    
- Returns a string prefixed with `'0o'`.
    

```python
oct(8)   # Output: '0o10'
```

- Without prefix:
    

```python
oct(8)[2:]   # Output: '10'
```

### 4. Using `format()` Function

The `format()` function provides more control over output formatting:

```python
format(10, 'b')   # Binary → '1010'
format(255, 'x')  # Hex → 'ff'
format(8, 'o')    # Octal → '10'
```

- Uppercase hex:
    

```python
format(255, 'X')  # 'FF'
```

### 5. Using f-Strings (Python 3.6+)

A modern and readable way:

```python
f"{10:b}"   # '1010'
f"{255:x}"  # 'ff'
f"{8:o}"    # '10'
```

### 6. Converting Back to Integers

Use `int()` with a base:

```python
int('1010', 2)  # Binary → 10
int('ff', 16)   # Hex → 255
int('10', 8)    # Octal → 8
```

### Summary

- `bin()`, `hex()`, `oct()` → quick conversions with prefixes
    
- `format()` and f-strings → flexible formatting without prefixes
    
- `int(value, base)` → convert strings back to integers
    

These built-ins make base conversion in Python concise and readable, without needing external libraries.

