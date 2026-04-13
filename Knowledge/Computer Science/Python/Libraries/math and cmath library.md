## Python: math & cmath Modules – Essential Guide

**math** → Mathematical functions for **real numbers** (floats & integers). **cmath** → Same functions but for **complex numbers**.

**Key difference**:

```Python
math.sqrt(-1) → raises ValueError: math domain error
cmath.sqrt(-1) → returns 1j (always returns complex)
```

> Both are part of Python’s standard library — no installation needed.

## 1. Importing

```Python
import math
import cmath

# Common aliases (optional but popular)
import math as m
import cmath as cm
```

## 2. Constants

|Constant|Module|Value|Description|
|---|---|---|---|
|pi|both|3.141592653589793|π (pi)|
|e|both|2.718281828459045|Euler's number (e)|
|tau|math|2π ≈ 6.283185307179586|2 * pi|
|inf|math|inf|Positive infinity|
|nan|math|nan|Not a Number|


```Python
print(math.pi)      # 3.141592653589793
print(math.e)       # 2.718281828459045
print(math.tau)     # 6.283185307179586
```

## 3. Most Important Functions – math (Real Numbers)

### Number Theory & Rounding


```Python
math.ceil(3.7)      # 4          → smallest integer >= x
math.floor(3.7)     # 3          → largest integer <= x
math.trunc(3.7)     # 3
round(3.7)          # built-in, but math has more precision options

math.fabs(-5.3)     # 5.3        → absolute value (float)
abs(-5.3)           # 5.3        → built-in works too

math.factorial(5)   # 120
math.comb(5, 2)     # 10         → combinations C(n,k)  (Python 3.8+)
math.gcd(48, 18)    # 6          → greatest common divisor
math.lcm(12, 18)    # 36         → least common multiple (Python 3.9+)
math.isqrt(17)      # 4          → integer square root
```

### Power & Logarithmic


```Python
math.sqrt(16)       # 4.0
math.pow(2, 3)      # 8.0        → same as 2**3 but returns float
math.exp(2)         # 7.389...   → e^x

math.log(100)       # 4.605...   → natural log (base e)
math.log(100, 10)   # 2.0        → log base 10
math.log10(100)     # 2.0
math.log2(8)        # 3.0
```

### Trigonometric (input in **radians**)


```Python
math.sin(math.pi/2)   # 1.0
math.cos(0)           # 1.0
math.tan(math.pi/4)   # 1.0

math.asin(1)          # π/2
math.acos(0)          # π/2
math.atan(1)          # π/4
math.atan2(1, 1)      # π/4   → better than atan(y/x) for quadrants

math.degrees(math.pi) # 180.0
math.radians(180)     # 3.14159...
```

### Hyperbolic & Others


```Python
math.sinh(x), math.cosh(x), math.tanh(x)
math.asinh(x), math.acosh(x), math.atanh(x)
```

## 4. Most Important Functions – cmath (Complex Numbers)

All cmath functions return a **complex** number (even if imaginary part is 0).


```Python
z = complex(3, 4)      # 3+4j
z = 3 + 4j             # same

cmath.sqrt(-1)         # 1j
cmath.sqrt(z)          # complex square root

cmath.exp(z)
cmath.log(z)           # natural log (principal value)
cmath.log10(z)
cmath.pow(z, 2)

# Trigonometric
cmath.sin(z)
cmath.cos(z)
cmath.tan(z)

# Phase & Polar form
cmath.phase(z)         # argument (angle in radians) → 0.927...
abs(z)                 # magnitude → 5.0   (built-in abs works on complex)

r, phi = cmath.polar(z)   # (5.0, 0.927...) polar coordinates
cmath.rect(r, phi)        # back to rectangular (Cartesian)
```

**Common pattern**:


```Python
cmath.sqrt(-4 + 0j)    # (0+2j)   → always works
```

## 5. Practical Examples

### Basic math usage


```Python
import math

radius = 5
area = math.pi * radius ** 2
print(f"Circle area: {area:.2f}")   # 78.54

print(math.gcd(56, 98))             # 14
print(math.comb(10, 3))             # 120
```

### Complex numbers example


```Python
import cmath

z1 = 1 + 2j
z2 = 3 + 4j

print(z1 + z2)                    # (4+6j)
print(cmath.sqrt(-9))             # 3j
print(cmath.phase(1+1j))          # 0.785... (π/4)
```

### Solving quadratic equation (with complex support)


```Python
def quadratic(a, b, c):
    disc = b**2 - 4*a*c
    root1 = (-b + cmath.sqrt(disc)) / (2*a)
    root2 = (-b - cmath.sqrt(disc)) / (2*a)
    return root1, root2

print(quadratic(1, -3, 2))   # real roots
print(quadratic(1, 1, 1))    # complex roots
```

## 6. Quick Tips & Best Practices

- Use **built-ins** first: abs(), pow(), **, min(), max(), round()
- Prefer math for real numbers → faster and raises clear errors on domain issues
- Use cmath only when you need complex results (negative sqrt, logs of negative, etc.)
- Trigonometric functions expect **radians** (use math.radians() / math.degrees() for conversion)
- For heavy numerical work, consider **NumPy** (much faster vectorized operations)
- Always check Python version for newer functions (comb, lcm, isqrt)

## 7. Common Workflow

1. Simple calculations → use built-ins or math
2. Need square root / log of negative → switch to cmath
3. Working with angles → remember radians vs degrees
4. Scientific / engineering code → often mix math + cmath + numpy


---
