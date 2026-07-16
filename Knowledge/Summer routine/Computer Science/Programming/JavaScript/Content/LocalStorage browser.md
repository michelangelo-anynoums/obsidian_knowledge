`localStorage` is a way to store data in the browser that persists even after the browser is closed. It's part of the **Web Storage API** and allows you to save key-value pairs in the user's browser. The data is saved locally, meaning it doesn't get sent to the server, and is available to your website as long as the user doesn't clear their browser data.

### Key points:

- **Data persists** even after page reloads or browser restarts.
    
- Storage is limited to **5-10MB** (depending on the browser).
    
- Data is **stored as strings**, so you might need to convert objects to strings (JSON.stringify) and back (JSON.parse).
    
- You can access and modify it with simple methods:
    
    - `localStorage.setItem('key', 'value')` – store data.
        
    - `localStorage.getItem('key')` – retrieve data.
        
    - `localStorage.removeItem('key')` – remove data.
        
    - `localStorage.clear()` – clear all data.
        

Example:

```JavaScript
localStorage.setItem('username', 'Alice'); // Store a username 
let user = localStorage.getItem('username');  // Retrieve the username 
console.log(user);  // Outputs: Alice
```

It’s useful for saving preferences or other small bits of data across sessions. Just keep in mind that it’s accessible to anyone using the browser, so don't store sensitive information!

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[JavaScript introduction]]