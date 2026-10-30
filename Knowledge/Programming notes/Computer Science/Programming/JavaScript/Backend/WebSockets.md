# 🔌 Node.js — WebSockets

> Real-time, two-way communication between client and server.

## 1. 📦 Setup & Installation

Install the `ws` library:


```bash
npm install ws
```

Import it:

```js
const WebSocket = require("ws");
```

## 2. ⚙️ Create a WebSocket Server

Create a server that accepts WebSocket connections.

```js
const WebSocket = require("ws");

const wss = new WebSocket.Server({
  port: 8080
});

wss.on("connection", (ws) => {
  console.log("Client connected");

  ws.send("Welcome to the server!");
});
```

## 3. 📩 Receive Messages

Listen for messages sent by clients.

```js
wss.on("connection", (ws) => {
  ws.on("message", (message) => {
    console.log(message.toString());
  });
});
```

## 4. 📤 Send Messages

Send data from server to client.

```js
ws.send("Hello client!");

ws.send(JSON.stringify({
  type: "notification",
  message: "New message!"
}));
```

## 5. 🔄 Broadcast Messages

Send a message to all connected clients.

```js
function broadcast(message) {
  wss.clients.forEach((client) => {
    if (client.readyState === WebSocket.OPEN) {
      client.send(message);
    }
  });
}
```

Useful for:

- Chat applications
- Live notifications
- Multiplayer games
- Real-time dashboards

## 6. 🌐 WebSocket Client

Connect from a browser using the native WebSocket API.

```js
const socket = new WebSocket("ws://localhost:8080");

socket.onopen = () => {
  socket.send("Hello server!");
};

socket.onmessage = (event) => {
  console.log(event.data);
};

socket.onclose = () => {
  console.log("Disconnected");
};

socket.onerror = (error) => {
  console.error(error);
};
```

## 7. 🔌 Connection Events

|Event|Purpose|
|---|---|
|`connection`|New client connects|
|`message`|Receive message|
|`close`|Connection closes|
|`error`|Connection error|

Client events:

|Event|Purpose|
|---|---|
|`open`|Connection established|
|`message`|Message received|
|`close`|Connection closed|
|`error`|Connection error|

## 8. ❤️ Heartbeat (Ping / Pong)

Detect disconnected clients.

```js
ws.on("pong", () => {
  ws.isAlive = true;
});
```

Server heartbeat example:

```js
const interval = setInterval(() => {
  wss.clients.forEach((client) => {
    if (!client.isAlive) {
      return client.terminate();
    }

    client.isAlive = false;
    client.ping();
  });
}, 30000);
```

## 9. 🔐 Security & Best Practices

- Use `wss://` in production (encrypted WebSockets).
- Authenticate connections.
- Validate incoming messages.
- Limit message size.
- Handle connection errors.
- Implement heartbeat checks.
- Control allowed origins.
- Clean up disconnected clients.

## 10. ⚡ WebSockets vs HTTP

|HTTP|WebSockets|
|---|---|
|Request / Response|Two-way communication|
|Usually separate requests|Persistent connection|
|Server responds to requests|Server can push messages|
|Traditional APIs|Real-time applications|

## 🧠 Quick Reference

|Method / Property|Purpose|
|---|---|
|`new WebSocket.Server()`|Create server|
|`connection`|Listen for clients|
|`ws.send()`|Send message|
|`message`|Receive message|
|`ws.close()`|Close connection|
|`ws.terminate()`|Force termination|
|`ws.ping()`|Send heartbeat|
|`WebSocket.OPEN`|Check open state|
|`wss.clients`|Connected clients|

---

# 🔌 Express.js + WebSockets

> Combine REST APIs and real-time communication in one Node.js server.

## 1. 📦 Installation

```bash
npm install express ws
```

## 2. ⚙️ Create the Server

Instead of starting Express directly with `app.listen()`, create an HTTP server and attach WebSockets to it.

**server.js**

```js
const express = require("express");
const http = require("http");
const WebSocket = require("ws");

const app = express();

// Create HTTP server
const server = http.createServer(app);

// Attach WebSocket server
const wss = new WebSocket.Server({ server });

// Start server
server.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

## 3. 🌐 Express Routes (HTTP)

Use Express for traditional API endpoints.

```js
app.use(express.json());

app.get("/api/users", (req, res) => {
  res.json([
    { id: 1, name: "Alex" },
    { id: 2, name: "John" }
  ]);
});
```

## 4. 🔄 WebSocket Connections

Use WebSockets for real-time communication.

```js
wss.on("connection", (ws) => {
  console.log("Client connected");

  ws.send("Welcome!");

  ws.on("message", (message) => {
    console.log(message.toString());
  });

  ws.on("close", () => {
    console.log("Client disconnected");
  });
});
```

## 5. 📡 Broadcast Messages

Send messages to every connected client.

```js
function broadcast(data) {
  wss.clients.forEach((client) => {
    if (client.readyState === WebSocket.OPEN) {
      client.send(data);
    }
  });
}
```

Example: broadcast a message when an API endpoint receives data.

```js
app.post("/api/message", (req, res) => {
  const { message } = req.body;

  broadcast(JSON.stringify({
    type: "message",
    content: message
  }));

  res.json({ success: true });
});
```

## 6. 💻 Frontend Connection

Connect your browser to the WebSocket server.

```js
const socket = new WebSocket("ws://localhost:3000");

socket.onopen = () => {
  console.log("Connected!");
};

socket.onmessage = (event) => {
  console.log("Server:", event.data);
};

socket.onclose = () => {
  console.log("Disconnected");
};

// Send message
socket.send("Hello server!");
```

## 7. 📂 Suggested Project Structure

```js
project/
│
├── server.js
│
├── routes/
│   └── users.js
│
├── sockets/
│   └── index.js
│
├── controllers/
│   └── userController.js
│
└── package.json
```

## 🧠 HTTP vs WebSockets

|Express (HTTP)|WebSockets|
|---|---|
|REST APIs|Real-time communication|
|GET / POST / PUT / DELETE|Send / Receive|
|Request → Response|Two-way connection|
|User authentication|Live updates|
|Database operations|Notifications / Chat|

---
