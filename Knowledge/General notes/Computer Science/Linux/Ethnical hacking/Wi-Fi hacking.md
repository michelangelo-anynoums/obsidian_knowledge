# 📶 Ethical Wi-Fi Hacking

## 🌐 What is Ethical Wi-Fi Hacking?

Ethical Wi-Fi hacking is the process of learning how wireless networks work and how they are protected. By understanding Wi-Fi security, you can learn how to find weak points and understand how they can be fixed.

It is a great way to learn about networking, encryption, wireless communication, and computer security.

## 🛠️ Useful Tools

### 📡 Monitoring & Packet Capture

These tools are commonly used to observe Wi-Fi networks, capture wireless traffic, and learn how wireless communication works.

![[Pasted image 20260720130710.png|372]]

**Note reference:** [[Cybersecurity hands-on course]]
**Theory psychics:** [[Wireless Fundamentals]]
**Aicrack-ng Suite:** [[Aircrack-ng Suite]]
**mdk4 tool**: [[mdk4 tool]]

- **Wireshark** – Network packet analyzer.
    
- **Aircrack-ng Suite** – Collection of wireless security tools.
    
- **Kismet** – Wireless network detector and monitoring tool.
    


📖 Official links:

- Wireshark → [https://www.wireshark.org/](https://www.wireshark.org/)
    
- Aircrack-ng → [https://www.aircrack-ng.org/](https://www.aircrack-ng.org/)
    
- Kismet → [https://www.kismetwireless.net/](https://www.kismetwireless.net/)
    

---

### 🔍 Reconnaissance Tools

These tools help discover nearby wireless networks and collect information such as signal strength, channels, encryption type, and connected devices.

- **Kismet**
    
- **Airodump-ng**
    
- **arp-scan**

📖 Official links:

- Kismet → [https://www.kismetwireless.net/](https://www.kismetwireless.net/)
    
- Aircrack-ng → [https://www.aircrack-ng.org/](https://www.aircrack-ng.org/)
    
- Arp-scan → [https://www.kali.org/tools/arp-scan/](https://www.kali.org/tools/arp-scan/)

Reference for **arp-scan** tool: [[arp-scan]]

---

### 📶 Popular Alfa Wi-Fi Adapters

These Alfa adapters are popular because they support monitor mode and packet capture on Linux with compatible chipsets.

|Model|Chipset|
|---|---|
|Alfa AWUS036NHA|Atheros AR9271|
|Alfa AWUS036NH|Ralink RT3070|
|Alfa AWUS036ACH|Realtek RTL8812AU|
|Alfa AWUS036ACM|MediaTek MT7612U|
|Alfa AWUS1900|Realtek RTL8814AU|
|Alfa AWUS036AXML|MediaTek MT7921AU (Wi-Fi 6)|
![[Pasted image 20260720125925.png|383]]

---


## 🤝 The 4-Way Handshake

When you connect your phone or laptop to a Wi-Fi network, the device and the router must first make sure they both know the correct Wi-Fi password.

Instead of sending the password through the air, they use the password to create the same secret keys on both devices.

Think of it like two people solving the same puzzle. If both get the same answer, they know they both had the correct password, even though they never said the answer out loud.

The 4-Way Handshake is simply four messages that help both devices agree on new encryption keys.

![[Pasted image 20260720125011.png|449]]

---

## 🔑 The Master Key (PMK)

The **Pairwise Master Key (PMK)** is the main secret key.

It comes from the Wi-Fi password (or from another login method in business networks).

You can think of the PMK as a **master key** that is almost never used directly to lock or unlock data.

Instead, it is used to create other keys.

🏠 House example:

- 🗝️ Master key = stored safely.
    
- 🔑 Daily key = used every day to lock and unlock the door.
    

This makes the connection more secure because the master key stays protected.

![[Pasted image 20260720125048.png|453]]

---

## 🔒 The Temporal Key (PTK)

The **Pairwise Temporal Key (PTK)** is the working key.

It is created during the 4-Way Handshake using:

- 🔑 The PMK
    
- 🎲 Random numbers made by the router and the device (called _nonces_)
    
- 📡 The MAC address of both devices
    

Because these values are different every time you connect, a **new PTK is created for every connection**.

This means that even if you reconnect to the same Wi-Fi with the same password, the encryption key will be different.

The PTK is then used to encrypt and protect the Wi-Fi traffic.

---

## ⚙️ What Happens During the 4-Way Handshake?

Imagine your laptop wants to join the Wi-Fi.

### 📩 Message 1

The router creates a random number called **ANonce**.

It sends this random number to your laptop.

At this point:

- Router has the PMK ✅
    
- Laptop has the PMK ✅
    
- Both now know ANonce.
    

---

### 📩 Message 2

Your laptop creates its own random number called **SNonce**.

Now the laptop has:

- PMK
    
- ANonce
    
- SNonce
    
- Both MAC addresses
    

Using these values, it calculates the PTK.

It then sends SNonce back to the router.

---

### 📩 Message 3

The router now has everything it needs:

- PMK
    
- ANonce
    
- SNonce
    
- MAC addresses
    

It calculates exactly the same PTK.

If both devices used the correct password, they will create the **same PTK** without sending it over the air.

The router then sends a message telling the laptop that secure communication can begin.

---

### 📩 Message 4

The laptop confirms that everything worked correctly.

Now both sides have the same PTK.

From this point on, Wi-Fi data is encrypted before it is transmitted.

---

## 🧠 Why Use Random Numbers?

The random numbers (ANonce and SNonce) make every connection unique.

Even if:

- 📶 the Wi-Fi name stays the same,
    
- 🔑 the password stays the same,
    

the encryption keys will still be different every time a device connects.

This helps protect against replay attacks and ensures that each session has its own fresh encryption keys.

---

## 📦 Simple Flow

```text
Password
    │
    ▼
Pairwise Master Key (PMK)
    │
    │ + ANonce
    │ + SNonce
    │ + Router MAC
    │ + Device MAC
    ▼
Pairwise Temporal Key (PTK)
    │
    ▼
Encrypt Wi-Fi traffic
```

---

## 🎯 Summary

- 🔑 The Wi-Fi password is never sent through the air.
    
- 🗝️ The PMK is the master secret.
    
- 🎲 Random numbers make every connection different.
    
- 🔒 The PTK is created during the 4-Way Handshake.
    
- 📡 The PTK encrypts all Wi-Fi traffic after the handshake is complete.
    
- 🤝 The 4-Way Handshake lets both devices prove they know the same password and safely create fresh encryption keys.