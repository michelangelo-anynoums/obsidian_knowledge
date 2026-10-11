# Java `Math` Class

Java’s **Math class** provides ready-made methods for common mathematical calculations. Its methods are **static**, so you can use them directly:

```java
Math.methodName()
```

## 🔢 Basic Methods

|Method|What it does|Example → Result|
|---|---|---|
|`Math.abs(x)`|Absolute value|`Math.abs(-5)` → `5`|
|`Math.max(x, y)`|Larger value|`Math.max(4, 9)` → `9`|
|`Math.min(x, y)`|Smaller value|`Math.min(4, 9)` → `4`|
|`Math.signum(x)`|Gives the sign of a number|`Math.signum(-8)` → `-1.0`|

## 📐 Powers & Roots

|Method|What it does|Example → Result|
|---|---|---|
|`Math.pow(x, y)`|Raises x to power y|`Math.pow(2, 3)` → `8.0`|
|`Math.sqrt(x)`|Square root|`Math.sqrt(25)` → `5.0`|
|`Math.cbrt(x)`|Cube root|`Math.cbrt(27)` → `3.0`|
|`Math.hypot(x, y)`|√(x² + y²)|`Math.hypot(3, 4)` → `5.0`|

## 🔄 Rounding Methods

|Method|What it does|Example → Result|
|---|---|---|
|`Math.round(x)`|Rounds to nearest integer|`Math.round(4.6)` → `5`|
|`Math.floor(x)`|Rounds down|`Math.floor(4.9)` → `4.0`|
|`Math.ceil(x)`|Rounds up|`Math.ceil(4.1)` → `5.0`|
|`Math.rint(x)`|Rounds to nearest integer value|`Math.rint(4.6)` → `5.0`|

## 🎲 Random Numbers

```java
Math.random()
```

Returns a random `double` from **0.0 (inclusive) to 1.0 (exclusive)**.

For a random integer from **1 to 10**:

```java
int n = (int)(Math.random() * 10) + 1;
```

## 📐 Trigonometry

These methods use **radians**.

|Method|Purpose|
|---|---|
|`Math.sin(x)`|Sine|
|`Math.cos(x)`|Cosine|
|`Math.tan(x)`|Tangent|
|`Math.asin(x)`|Inverse sine|
|`Math.acos(x)`|Inverse cosine|
|`Math.atan(x)`|Inverse tangent|
|`Math.atan2(y, x)`|Angle from x/y coordinates|

Example:

```java
double angle = Math.toRadians(90);

System.out.println(Math.sin(angle));  // 1.0
```

## 🔄 Angle Conversion

```java
Math.toRadians(180);   // 3.14159...
Math.toDegrees(Math.PI); // 180.0
```

## 📈 Logarithms & Exponents

|Method|Purpose|
|---|---|
|`Math.exp(x)`|eˣ|
|`Math.log(x)`|Natural logarithm (ln)|
|`Math.log10(x)`|Base-10 logarithm|
|`Math.expm1(x)`|eˣ − 1|
|`Math.log1p(x)`|ln(1 + x)|

Example:

```java
Math.log10(100);  // 2.0
Math.exp(1);      // e
```

## 🔢 Useful Constants

Java also provides some important mathematical constants:

```java
Math.PI   // π ≈ 3.14159
Math.E    // e ≈ 2.71828
```

### ⭐ Quick Reminder

The most commonly used methods are:

```text
abs()       → absolute value
max()       → largest
min()       → smallest
pow()       → power
sqrt()      → square root
cbrt()      → cube root
round()     → nearest integer
floor()     → down
ceil()       → up
random()    → random number
sin()       → sine
cos()       → cosine
tan()       → tangent
```

**Key point:** You normally use these as `Math.method()`, for example `Math.sqrt(49)`.

---
