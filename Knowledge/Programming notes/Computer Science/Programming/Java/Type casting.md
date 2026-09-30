## Understanding Type Casting in Java

### What is Type Casting?

In Java, type casting is the process of converting a variable from one data type to another. This is often necessary when you want to perform operations that require different data types or when you want to store a value in a variable of a different type.

### How `(int)` Works in This Context

In the code snippet `final float height = (int)scanner.nextFloat();`, the `(int)` is a type cast that converts the float value obtained from `scanner.nextFloat()` into an integer. Here’s how it functions:

- Input from Scanner: The method `scanner.nextFloat()` reads a floating-point number from user input.
- Casting to Integer: The `(int)` before `scanner.nextFloat()` truncates the decimal part of the float. This means that any fractional digits are discarded, and only the whole number part is retained.
- Final Assignment: The resulting integer value is then assigned to the variable `height`, which is declared as a float. However, since `height` is a float, the integer value will be implicitly converted back to a float for storage.

### Example

If the user inputs `5.75`, the casting will work as follows:

- `scanner.nextFloat()` returns `5.75`.
- `(int)5.75` results in `5` (the decimal part is discarded).
- `height` will then hold the value `5.0` as a float.

### Summary

The `(int)` cast effectively removes any decimal portion from the float value, allowing for the storage of only the whole number in the variable. This is useful when you need to ensure that only integer values are processed or stored.

---
