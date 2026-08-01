# Authentication & Association

## Authentication Frames

- **Authentication** is the process of **proving the identity** of a device.
    
- The client asks to join the wireless network.
    
- The access point (**AP**) checks the request and replies.
    

---

## Association Frames

- **Association** happens **after authentication**.
    
- The client asks to connect to the **AP**.
    
- If accepted, the AP allows the client to **send and receive data**.
    

---

## Deauthentication

- **Deauthentication** ends the **authentication** between the client and the AP.
    
- The client must **authenticate again** before reconnecting.
    

---

## Disassociation

- **Disassociation** ends the **connection**, but not the authentication.
    
- The client disconnects from the AP.
    
- The client can **associate again** without repeating authentication (if still authenticated).
    

---

# Connection Process

```text
Client
   │
   ▼
**Authentication Request**
   │
   ▼
**Authentication Response**
   │
   ▼
**Association Request**
   │
   ▼
**Association Response**
   │
   ▼
✅ **Connected**
```