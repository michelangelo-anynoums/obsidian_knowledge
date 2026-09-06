# Wireless Security History

https://www.youtube.com/watch?v=r_At4vSoVI4


![[Pasted image 20260730112912.png|495]]
## WEP (Wired Equivalent Privacy)

- **WEP** was the **first Wi-Fi security protocol** (1997).
    
- It used the **RC4 encryption algorithm** to protect data.
    
- Each packet was encrypted with a **shared secret key** and a **24-bit Initialization Vector (IV)**.
    
- The IV was sent **without encryption**, so attackers could capture it.
    
- Because the IV was **very short**, it was reused often, making the key easier to discover.
    

### Why WEP Failed

- **Weak RC4 implementation**.
    
- **24-bit IV** repeated frequently.
    
- Attackers could collect many packets and **recover the encryption key**.
    
- It offered **poor security** and was replaced by **WPA**.
    

---

## WPA (Wi-Fi Protected Access)

- **WPA** was created as a **temporary replacement** for WEP.
    
- It still used **RC4**, but in a much safer way.
    
- It introduced **TKIP (Temporal Key Integrity Protocol)**.
    
- **TKIP** created a **new encryption key for every packet**, making attacks much harder.
    
- It also added **message integrity checks** to detect if data had been changed.
    

### How it worked

1. The client connected to the Wi-Fi network.
    
2. The client and AP generated **temporary encryption keys**.
    
3. Every packet used a **different key**.
    
4. The receiver checked that the packet had not been modified.
    

---

## WPA2 (Wi-Fi Protected Access 2)

- **WPA2** replaced WPA in **2004**.
    
- It uses **AES (Advanced Encryption Standard)** instead of RC4.
    
- AES is **faster, stronger, and more secure**.
    
- WPA2 uses **CCMP (Counter Mode with CBC-MAC Protocol)** for encryption and integrity.
    

### How it worked

1. The client authenticated with the AP.
    
2. Both devices created **shared encryption keys**.
    
3. All data was encrypted using **AES**.
    
4. The receiver verified that the data had not been changed.
    

- **WPA2** became the **standard Wi-Fi security protocol** for many years.
    

---

## WPA3 (Wi-Fi Protected Access 3)

- **WPA3** is the newest Wi-Fi security standard.
    
- It replaces the old password exchange with **SAE (Simultaneous Authentication of Equals)**.
    
- SAE makes it **much harder** to guess passwords, even if someone captures Wi-Fi traffic.
    
- It also provides **forward secrecy**, meaning that if the password is discovered later, **old captured data cannot be decrypted**.
    

### How it worked

1. The client and AP perform the **SAE handshake**.
    
2. They securely create **session keys**.
    
3. Data is encrypted with **strong encryption**.
    
4. Every new connection creates **new session keys**.
    

- **WPA3** gives the **best protection** against password guessing and modern attacks.
    

---

# Quick Comparison

|**Protocol**|**Encryption**|**Main Improvement**|
|---|---|---|
|**WEP**|RC4|First Wi-Fi security, but very weak.|
|**WPA**|RC4 + TKIP|New key for every packet and better integrity.|
|**WPA2**|AES + CCMP|Strong encryption and high security.|
|**WPA3**|AES + SAE|Strong authentication and protection against password attacks.|

This version explains **how each protocol works** while staying concise enough for class notes.

---
