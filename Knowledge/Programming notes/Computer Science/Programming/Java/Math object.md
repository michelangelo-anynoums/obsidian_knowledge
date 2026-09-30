# Java Programming: Math Operations

In Java, mathematical operations and constants are handled by the built-in `java.lang.Math` class. Because it is part of the `lang` package, you don't need to import anything to use it.

## Common Math Methods

Here are some of the most frequently used methods in the `Math` class:

- **`Math.sqrt(x)`**: Returns the square root of $x$.
    
    Java
    
    ```Java
    double result = Math.sqrt(25); // Returns 5.0
    ```
    
- **`Math.pow(base, exponent)`**: Returns $base^{exponent}$ (base raised to the power of exponent).
    
    Java
    
    ```Java
    double result = Math.pow(2, 3); // Returns 8.0
    ```
    
- **`Math.abs(x)`**: Returns the absolute (positive) value of $x$.
    
    Java
    
    ```Java
    int result = Math.abs(-10); // Returns 10
    ```
    
- **`Math.max(a, b)`** and **`Math.min(a, b)`**: Returns the larger or smaller of two numbers.
    
    Java
    
    ```Java
    int higher = Math.max(5, 12); // Returns 12
    ```
    
- **`Math.random()`**: Returns a pseudo-random double greater than or equal to $0.0$ and less than $1.0$ ($0.0 \le x < 1.0$).
    
    Java
    
    ```Java
    double randomNum = Math.random(); 
    ```
    

## Commonly Used Constants

You can also access standard mathematical constants directly:

- **`Math.PI`**: Represents the mathematical constant $\pi$ ($\approx 3.14159$).
    
- **`Math.E`**: Represents Euler's number ($e \approx 2.718$).
    

> **Tip:** All methods in the `Math` class are `static`, meaning you call them directly using the class name (`Math.methodName()`) rather than creating an object instance.

---
