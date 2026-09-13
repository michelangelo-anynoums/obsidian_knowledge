# Real-World Wireless Threats

## KRACK

**KRACK** is an attack against the **WPA2 Wi-Fi security protocol**.  
It can allow an attacker to **intercept or manipulate Wi-Fi traffic**.  
It mainly works by exploiting weaknesses in the **WPA2 handshake**.

## Weak Passwords

A **weak Wi-Fi password** is easy to guess or crack.  
Attackers can use **password lists** or **brute-force attacks** to gain access.  
Use a **long, unique password** to improve security.

## Captive Portal Abuse

A **captive portal** is a web page that asks users to log in before using a network.  
Attackers can create **fake portals** to steal **passwords or personal information**.  
Always check that the login page is **trusted and secure**.

## Rogue Clients

A **rogue client** is an **unauthorized device** connected to a wireless network.  
It may be used to **steal data**, spread malware, or attack other devices.  
Network administrators should **monitor connected devices** and remove unknown ones.

---

## KRACK Attack

**KRACK** stands for **Key Reinstallation Attack**. It is a security attack against **WPA2**, a protocol widely used to protect Wi-Fi networks.

When a device connects to a Wi-Fi network, it performs a **4-way handshake** with the access point. This handshake helps both sides create a **temporary encryption key** for protecting the connection.

The problem is that, during this handshake, an attacker can trick the victim device into **reinstalling an encryption key that is already being used**. This is why the attack is called a _Key Reinstallation Attack_.

### How it works

1. The victim connects to a **Wi-Fi network**.
2. The attacker needs to be **close enough to communicate with the Wi-Fi connection**.
3. The attacker interferes with messages from the **4-way handshake**.
4. The victim is tricked into **reinstalling the same encryption key**.
5. This can cause some security information, such as the **encryption counter**, to be reset.
6. The attacker may then be able to **read or manipulate some network traffic**.

### Why is KRACK dangerous?

KRACK does **not simply reveal the Wi-Fi password**. Instead, it attacks the **process used to establish secure communication**.

Depending on the device and configuration, an attacker could potentially **read sensitive data**, such as information sent over an unprotected application protocol, or **modify network traffic**.

### How to protect against KRACK

The main solution is to **update the operating system and Wi-Fi devices**. Manufacturers released **security patches** to fix the vulnerable implementations.

> **Key idea:** KRACK attacks the **WPA2 key-installation process**, not the Wi-Fi password itself.