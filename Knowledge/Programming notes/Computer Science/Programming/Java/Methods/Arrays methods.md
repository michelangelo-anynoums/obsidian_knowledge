# Java Arrays – Declaration, Usage and Methods

## 1. Introduction

> [!important] In Java, arrays are used to store multiple values of the same data type in a single variable.
Arrays have a fixed size once created, and their indexes start at `0`.

---
## 2. Declaring Arrays (Classic Way)

### A. Declare first, initialise later

```java
int[] numbers;
numbers = new int[5];
```

### B. Declare and initialise at the same time


```java
int[] numbers = {10, 20, 30, 40, 50};
```

### C. Using classic syntax



```java
int numbers[] = {10, 20, 30, 40, 50};
```

Both `int[] numbers` and `int numbers[]` are valid, but `int[] numbers` is preferred.

### D. Using new int[]


```java
int[] numbers = new int[3];
```

This creates an array with 3 elements, automatically initialised to `0`.

You can assign values later:


```java
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
```

## 3. First Way: Working with Arrays Using Indexes

You can access and modify individual elements using their indexes.

```java
int[] numbers = {10, 20, 30, 40};

// Access an element
System.out.println(numbers[0]); // 10

// Change an element
numbers[1] = 25;

// Get array length
System.out.println(numbers.length); // 4
```

### Using a for loop

```java
int[] numbers = {10, 20, 30, 40};

for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

### Using an enhanced for loop (for-each)

```java
int[] numbers = {10, 20, 30, 40};

for (int number : numbers) {
    System.out.println(number);
}
```

The enhanced for loop is useful when you want to read every element without using indexes.

# Common Arrays Methods

Java provides the `Arrays` utility class with useful methods.

First, import it:

```java
import java.util.Arrays;
```


|Method|Description|
|---|---|
|`Arrays.toString()`|Converts an array into a readable String|
|`Arrays.sort()`|Sorts elements in ascending order|
|`Arrays.binarySearch()`|Searches for an element in a sorted array|
|`Arrays.equals()`|Compares two arrays|
|`Arrays.fill()`|Fills an array with the same value|
|`Arrays.copyOf()`|Creates a copy of an array|
|`Arrays.copyOfRange()`|Copies a specific range|
|`Arrays.stream()`|Creates a stream from an array|
|`Arrays.compare()`|Lexicographically compares two arrays|
|`Arrays.mismatch()`|Finds the first different position|

## 5. Examples of Arrays Methods

### 1. toString()

Prints the contents of an array.

```java
int[] numbers = {3, 1, 5};

System.out.println(Arrays.toString(numbers));

// [3, 1, 5]
```

### 2. sort()

Sorts elements in ascending order.

```java
int[] numbers = {5, 2, 8, 1};

Arrays.sort(numbers);

System.out.println(Arrays.toString(numbers));

// [1, 2, 5, 8]
```

### 3. binarySearch()

Searches for an element in a sorted array.

```java
int[] numbers = {1, 2, 5, 8};

int result = Arrays.binarySearch(numbers, 5);

System.out.println(result);

// 2 (index of element 5)
```

Important: The array should be sorted before using `binarySearch()`.

### 4. equals()

Checks whether two arrays contain the same elements in the same order.

```java
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};

System.out.println(Arrays.equals(a, b));

// true
```

### 5. fill()

Fills all elements with the same value.


```java
int[] numbers = new int[4];

Arrays.fill(numbers, 10);

System.out.println(Arrays.toString(numbers));

// [10, 10, 10, 10]
```

### 6. copyOf()

Creates a copy of an array.

```java
int[] original = {1, 2, 3};

int[] copy = Arrays.copyOf(original, 5);

System.out.println(Arrays.toString(copy));

// [1, 2, 3, 0, 0]
```

### 7. copyOfRange()

Copies a specific range of elements.

```java
int[] numbers = {10, 20, 30, 40, 50};

int[] copy = Arrays.copyOfRange(numbers, 1, 4);

System.out.println(Arrays.toString(copy));

// [20, 30, 40]
```

The ending index (4) is excluded.

## 6. Reversing an Array

### Example: Reverse using a for loop



```java
int[] numbers = {1, 2, 3, 4, 5};

for (int i = 0; i < numbers.length / 2; i++) {

    int temp = numbers[i];

    numbers[i] = numbers[numbers.length - 1 - i];

    numbers[numbers.length - 1 - i] = temp;
}

System.out.println(Arrays.toString(numbers));

// [5, 4, 3, 2, 1]
```

> This technique is called swapping.

## Quick Summary

|Operation|Syntax|
|---|---|
|Declare array|`int[] numbers;`|
|Create array|`new int[5]`|
|Access element|`numbers[0]`|
|Change element|`numbers[0] = 10;`|
|Get array size|`numbers.length`|
|Print array|`Arrays.toString(numbers)`|
|Sort|`Arrays.sort(numbers)`|
|Search|`Arrays.binarySearch(numbers, 5)`|
|Compare|`Arrays.equals(a, b)`|
|Fill|`Arrays.fill(numbers, 10)`|
|Copy|`Arrays.copyOf(numbers, 5)`|
|Reverse|Use a loop and swap elements|

**Remember:** Practice accessing, sorting, searching, copying and reversing arrays. These operations are very common in Java programming exercises.

---
