#### **For reference:** [[Wi-Fi hacking]]

# Handshake Analysis

### How handshakes work

A **Wi-Fi handshake** happens when a device connects to a protected wireless network. It helps the device and access point **verify each other** and create encryption keys.

### Why attackers target them

Attackers may capture a handshake because it contains information that can be used to **test password guesses offline**. The handshake itself does not directly reveal the Wi-Fi password.

### Detection methods

A captured handshake can be identified by looking for **EAPOL frames** in a packet capture. Unusual or repeated authentication attempts may also be useful signs to investigate.

### Use Wireshark captures

**Wireshark** can filter and inspect EAPOL traffic. Looking at the **4-way handshake** helps you understand the connection process and identify authentication events.