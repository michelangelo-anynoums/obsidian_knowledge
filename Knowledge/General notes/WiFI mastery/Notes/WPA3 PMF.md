# WPA3 + PMF

## **WPA3 Improvements**

**WPA3** is the newest **Wi-Fi security protocol**. It improves security compared to **WPA2** by providing stronger authentication and better protection against attacks.

### **Improvements**

- Uses **SAE** instead of **Pre-Shared Key (PSK)**.
- Better protection against **password guessing (dictionary attacks)**.
- Uses **stronger encryption**.
- Requires **Protected Management Frames (PMF)**.
- Provides better security on **public Wi-Fi networks**.

### **Flow**

1. A client wants to join a WPA3 Wi-Fi network.
2. The client and Access Point perform **SAE authentication**.
3. Both devices create a **shared secret key**.
4. A secure encrypted connection is established.
5. **PMF** protects important Wi-Fi management messages.
6. The client can now safely use the network.

> **WPA3 makes Wi-Fi authentication and communication much more secure than WPA2.**

---

## **SAE (Simultaneous Authentication of Equals)**

**SAE** is the authentication method used in **WPA3**. It securely verifies that both the client and the Access Point know the **same Wi-Fi password**, without sending the password over the network.

### **Why is SAE better than WPA2-PSK?**

- The password is **never transmitted**.
- Captured authentication messages **cannot be reused** to guess the password offline.
- Every connection creates a **new session key**.
- Provides **forward secrecy** (old sessions stay secure even if the password is discovered later).

### **Flow**

1. The client enters the Wi-Fi password.
2. The client and Access Point each use the password to perform a **cryptographic exchange**.
3. Both independently calculate the **same shared secret**.
4. They verify that both know the correct password.
5. A unique **session key** is created.
6. Secure encrypted communication begins.

> **SAE proves both sides know the password without revealing it.**

---

## **Protected Management Frames (PMF) (802.11w)**

**PMF** protects important **Wi-Fi management frames** from being changed or forged by attackers.

### **What are management frames?**

Management frames control the Wi-Fi connection, such as:

- Connecting to the network.
- Disconnecting from the network.
- Maintaining the Wi-Fi connection.

Without PMF, an attacker could **fake** these messages.

### **What does PMF protect?**

- **Deauthentication frames**
- **Disassociation frames**
- Other important management messages

### **Flow**

1. The client successfully connects to the Wi-Fi network.
2. The client and Access Point enable **PMF**.
3. Management frames are **authenticated and protected**.
4. If an attacker sends a fake deauthentication message, the client checks its protection.
5. Invalid or modified frames are **rejected**.
6. The Wi-Fi connection remains secure.

> **PMF prevents attackers from disconnecting users by sending fake management messages.**

---

# **Complete WPA3 Authentication Flow**

1. The client selects a **WPA3 Wi-Fi network**.
2. The client and Access Point perform **SAE authentication**.
3. A **shared secret** and **session keys** are created.
4. The encrypted Wi-Fi connection is established.
5. **PMF** protects management frames during the session.
6. The client securely communicates on the network.

### **Remember**

- **WPA3** = Stronger Wi-Fi security than WPA2.
- **SAE** = Secure password authentication without sending the password.
- **PMF (802.11w)** = Protects Wi-Fi management frames from spoofing and disconnection attacks.

---
