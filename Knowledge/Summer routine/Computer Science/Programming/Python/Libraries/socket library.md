## Python `socket` Library

## 📌 What is it?

The `socket` module enables **network communication** between programs using sockets (communication endpoints).

---

## 🧩 Key Concepts

- **Socket** → endpoint for communication
    
- **IP Address + Port** → identifies a process
    
- **Client / Server model**
    
- **Protocols**:
    
    - TCP → reliable, connection-based
        
    - UDP → fast, connectionless
        

---

## 🔧 Creating a Socket

```python
socket.socket(family, type)
```

Common values:

- `AF_INET` → IPv4
    
- `SOCK_STREAM` → TCP
    
- `SOCK_DGRAM` → UDP
    

---

## 🔁 Communication Flow

1. Server:
    - `bind()` → attach to address/port
    - `listen()` → wait for connections
    - `accept()` → establish connection
2. Client:
    - `connect()` → connect to server
3. Both:
    - `send()` / `sendall()` → send data
    - `recv()` → receive data

---

## 📡 Example (TCP)

### Server

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(("localhost", 5000))
s.listen()

conn, addr = s.accept()
conn.sendall(b"Hello")
conn.close()
```

### Client

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("localhost", 5000))
print(s.recv(1024))
s.close()
```

---

## ⚠️ Notes

- Use `.encode()` / `.decode()` for strings
    
- Always close sockets
    
- Ports must be available
    
- Use `localhost` for local testing
    

---

## 🚀 Extras

- UDP: `SOCK_DGRAM`
    
- Non-blocking sockets
    
- `select()` for multiple connections
    
- SSL with `ssl` module
    

---

## 🧠 Mental Model

Socket = **pipe between two programs over a network**