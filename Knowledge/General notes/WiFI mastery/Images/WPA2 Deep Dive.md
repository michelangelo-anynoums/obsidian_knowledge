# WPA2 Deep Dive

## PSK (Pre-Shared Key)

- The **PSK** is the **Wi-Fi password** entered by the user.
    
- The client and the **Access Point (AP)** both know this password.
    
- The PSK is **not used directly** to encrypt data.
    
- Instead, it is used to create another key called the **PMK**.
    

---

## PMK (Pairwise Master Key)

- The **PMK** is generated from the **PSK**.
    
- It is the **master key** used during authentication.
    
- The PMK is **never sent over the network**.
    
- Both the client and the AP calculate the same PMK independently.
    

**Flow:**

```text
Wi-Fi Password (PSK)
        │
        ▼
Pairwise Master Key (PMK)
```

---

## PTK (Pairwise Transient Key)

- The **PTK** is created during the **Four-Way Handshake**.
    
- It is generated using:
    
    - **PMK**
        
    - **Client nonce (SNonce)**
        
    - **AP nonce (ANonce)**
        
    - **MAC address of the client**
        
    - **MAC address of the AP**
        
- The PTK is **unique for each connection**.
    
- It encrypts **unicast traffic** (communication between one client and the AP).
    

---

## GTK (Group Temporal Key)

- The **GTK** is created by the **AP**.
    
- It encrypts **broadcast** and **multicast** traffic.
    
- Every connected client receives the same GTK.
    
- The GTK is sent **securely** during the Four-Way Handshake.
    

---

# Four-Way Handshake

The **Four-Way Handshake** proves that both the client and the AP know the **PMK** without sending it over the network.

### Step 1

- The **AP** sends a random number called the **ANonce**.
    

### Step 2

- The **Client** creates its own random number called the **SNonce**.
    
- Using the **PMK**, **ANonce**, **SNonce**, and both **MAC addresses**, it creates the **PTK**.
    
- The client sends the **SNonce** to the AP.
    

### Step 3

- The **AP** now has all the same information.
    
- It creates the **same PTK**.
    
- The AP sends the **GTK**, encrypted with the PTK.
    

### Step 4

- The client confirms everything is correct.
    
- Both devices now share:
    
    - **PTK** → for **unicast** traffic.
        
    - **GTK** → for **broadcast/multicast** traffic.
        
- Secure communication begins.
    

---

# Key Flow

```text
Wi-Fi Password (PSK)
          │
          ▼
Pairwise Master Key (PMK)
          │
          ▼
Four-Way Handshake
          │
          ├────────► PTK (Unicast Traffic)
          │
          └────────► GTK (Broadcast & Multicast Traffic)
```

---

# Summary

| **Key**                | **Purpose**                                                          |
| ---------------------- | -------------------------------------------------------------------- |
| **PSK**                | Wi-Fi password entered by the user.                                  |
| **PMK**                | Master key derived from the PSK.                                     |
| **PTK**                | Session key used to encrypt **unicast** traffic.                     |
| **GTK**                | Key used to encrypt **broadcast** and **multicast** traffic.         |
| **Four-Way Handshake** | Creates the PTK and securely shares the GTK without sending the PMK. |

---
