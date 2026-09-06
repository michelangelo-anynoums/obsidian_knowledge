**JavaScript** is a versatile, high-level programming language used primarily for web development. It's often referred to as the _language of the web_, as it enables interactivity in web pages.

One of the key features of **JavaJavaScript** is the use of **variables**. You can store values in variables using `let`, `const`, or `var`. For example, `let age = 15;` stores the number 15 in a variable called `age`. If you use `const` instead, like `const name = "Alice";`, the value cannot be reassigned later.

Another important concept is **functions**. Functions are blocks of code that you define to perform a specific task. You define a function with the **function** keyword, like this:

```JavaScript
function greet(){   
console.log("Hello, world!"); 
}
```

You can then call the function by simply writing `greet();`.

**Arrays** and **objects** are key data structures in **JavaScript**. An array is an ordered list of values, such as:

```JavaScript
let fruits = ["apple", "banana", "cherry"];
```

An object stores key-value pairs, like:

```JavaScript
let person = { name: "Alice", age: 15 };
```

Here, `"name"` and `"age"` are the keys, and `"Alice"` and `15` are the corresponding values.

To repeat code, you can use **loops**. A common loop in **JavaScript** is the **`for`** loop. Here's an example:

```JavaScript
for (let i = 0; i < 5; i++) {   
console.log(i);  // Prints numbers 0 to 4 
}
```

This loop will execute the code inside it five times, printing the numbers 0 through 4.

**JavaScript** is also widely used to handle **events**, such as clicks or key presses. For example, you can set up an event listener like this:

```JavaScript
document.getElementById("myButton").addEventListener("click", function() {   
alert("Button clicked!"); });
```

When the user clicks the button with the ID `"myButton"`, the message `"Button clicked!"` will appear in an alert.

Finally, **JavaScript** handles **asynchronous code** with **Promises** and the **async/await** syntax. For example, to fetch data from an API, you might write:

```JavaScript
async function fetchData(){   

let response = await fetch('https://api.example.com');   
let data = await response.json();   
console.log(data); 

}
```

Here, `fetchData` fetches the data, waits for the response (`await`), and then logs the data to the console.

**JavaScript** is a powerful tool that makes websites dynamic and interactive, and it's used for both **front-end** and **back-end** development.

![[JavaScript_logo.png]]

# **What You Will Learn:**

- **==LocalStorage==**: is a part of the Web Storage API in JavaScript that allows web applications to store data as key-value pairs directly in the user's browser. [[LocalStorage browser]]
    
- **==Playing audio files==**: with JavaScript refers to the process of controlling audio playback on a web page using JavaScript code. [[Audio]]
    
- **==Node.js==**: is a free, open-source, cross-platform JavaScript runtime environment that allows developers to execute JavaScript code outside of a web browser. [[Node.js introduction]]
- **DOMpurify:** is an open-source JavaScript library which sanitizes malicious code. For example, user input. [[DOMpurify]]

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  