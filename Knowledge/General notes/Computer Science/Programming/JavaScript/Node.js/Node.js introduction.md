**Node.js** is a runtime environment built on Chrome's _V8 JavaScript engine_ that allows you to run JavaScript on the server side. It’s **asynchronous** and **event-driven**, which makes it ideal for building fast, scalable network applications. Unlike traditional server-side languages, Node.js uses a **single-threaded** event loop to handle multiple concurrent connections, which is great for I/O-heavy applications (like web servers).

![[nodejs_logo.svg]]

Key **concepts** in Node.js:

- **Event Loop**: A non-blocking mechanism that enables Node.js to handle many operations concurrently without slowing down.
    
- **Callback functions**: Used for handling asynchronous operations. Instead of blocking the program, callbacks are called once a task is completed.
    
- **Modules**: Node.js uses a **modular architecture**, where you can import functionality from different modules using `require()`.
    

---

**Express.js** is a minimalist web framework for Node.js that simplifies building web applications and APIs. It provides a set of tools to handle **routing**, **middleware**, and **requests/responses** in a more structured way than raw Node.js.

Key features of Express.js:

- **Routing**: Simplifies defining application routes like GET, POST, PUT, and DELETE.
    
- **Middleware**: Allows you to add functionality (like logging, authentication, or error handling) between the request and response cycle.
    
- **Template engines**: Integrates easily with view engines like **EJS** or **Pug** to render dynamic content.
    

Together, Node.js and Express.js are powerful for building fast, scalable backend systems.

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  