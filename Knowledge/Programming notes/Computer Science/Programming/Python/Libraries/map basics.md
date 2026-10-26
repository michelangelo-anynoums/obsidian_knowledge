### What is `map()`?

The `map()` function applies a given function to all the items in an iterable (like a list) and returns a map object (which is an iterator). You can think of it as a way to "transform" each element of an iterable using a function.

The syntax is:

```Python
map(function, iterable)
```

- **function**: A function that you want to apply to each element of the iterable.
    
- **iterable**: A collection of items (like a list, tuple, etc.) that you want to process.
    

### Simple Example:

Let's say we have a list of numbers, and we want to square each number.

```Python
# A simple function to square a number 
def square(x):     
	return x * x  
	
# A list of numbers 
numbers = [1, 2, 3, 4, 5]  

# Use map to apply the square function to each number 
squared_numbers = map(square, numbers)  

# Convert the map object to a list and print it 
print(list(squared_numbers))
```

### Output:

`[1, 4, 9, 16, 25]`

In this example:

- `map(square, numbers)` applies the `square()` function to each item in the `numbers` list.
    
- The result is a map object, which we convert to a list to print it.
    

### Why use `map()`?

- It’s great for applying a function to each element of an iterable without using a loop.
    
- It can make your code cleaner and more concise!

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]
