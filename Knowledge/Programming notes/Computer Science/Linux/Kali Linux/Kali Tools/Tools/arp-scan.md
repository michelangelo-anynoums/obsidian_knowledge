# 🕵️ arp-scan Tool — Network Device Discovery

## 📌 What is arp-scan?

**arp-scan** is a network discovery tool used to find devices connected to a local network (LAN). 🌐

It works by sending **ARP requests** and checking which devices reply.

You can use it to discover:

✅ IP addresses  
✅ MAC addresses  
✅ Device manufacturers (vendor names)  
✅ Number of devices connected to the network

⚠️ Use arp-scan only on networks you own or have permission to test.

---

# 🔧 Installing arp-scan

Kali Linux usually includes it, but if it is missing:

```bash
sudo apt update
sudo apt install arp-scan
```

---

# 🚀 Basic Command

## 1️⃣ Scan your local network

```bash
sudo arp-scan --localnet
```

Example output:

```
192.168.1.1    AA:BB:CC:11:22:33    TP-Link
192.168.1.20   44:55:66:77:88:99    Apple
192.168.1.35   10:20:30:40:50:60    Samsung
```

What you see:

📍 IP address → device network address  
🔗 MAC address → device hardware address  
🏷️ Vendor → possible manufacturer

---

# 🌍 Scan a Specific Network

If your network is:

```
192.168.1.0/24
```

Run:

```bash
sudo arp-scan 192.168.1.0/24
```

Example:

```
sudo arp-scan 192.168.0.0/24
```

This checks devices from:

```
192.168.0.1
to
192.168.0.254
```

---

# 📡 Find Your Network Range

Before scanning, check your IP:

```bash
ip addr
```

Example:

```
inet 192.168.1.45/24
```

The `/24` usually means your network is:

```
192.168.1.0/24
```

---

# 🔄 Scan Through a Specific Interface

If you have multiple network cards:

```bash
sudo arp-scan --interface=wlan0 --localnet
```

Example:

```
wlan0 = Wi-Fi adapter
eth0  = Ethernet cable
```

---

# 🏭 Show More Vendor Information

Update the MAC vendor database:

```bash
sudo arp-scan --update
```

Then scan again:

```bash
sudo arp-scan --localnet
```

This can help identify:

📱 Apple → iPhone/iPad/Mac  
📺 Samsung/LG → possible TV or phone  
🖨️ HP → possible printer  
🎮 Sony → possible PlayStation

---

# 💾 Save Scan Results

Save results to a file:

```bash
sudo arp-scan --localnet > devices.txt
```

Example:

```
devices.txt

192.168.1.1   Router
192.168.1.15  Phone
192.168.1.25  TV
```

---

# ⭐ Most Useful Commands Summary

|Command|Purpose|
|---|---|
|`sudo arp-scan --localnet`|Scan your current LAN|
|`sudo arp-scan 192.168.1.0/24`|Scan a specific network|
|`ip addr`|Find your IP and network|
|`sudo arp-scan --interface=wlan0 --localnet`|Scan using Wi-Fi|
|`sudo arp-scan --update`|Update vendor database|
|`sudo arp-scan --localnet > file.txt`|Save results|

---

# 🧪 Simple Example Scenario

You connect to your home Wi-Fi and want to know what devices are connected.

Step 1:

```bash
ip addr
```

You discover:

```
192.168.1.50/24
```

Step 2:

```bash
sudo arp-scan --localnet
```

You get:

```
192.168.1.1    Router
192.168.1.12   Apple
192.168.1.18   Samsung
192.168.1.30   HP
```

Possible result:

📱 Apple → phone/tablet/computer  
📺 Samsung → phone or smart TV  
🖨️ HP → printer

---

# 🧠 Remember

arp-scan is great for:

✅ "Who is connected?"  
✅ "What devices exist?"  
✅ "Who made this device?"

But it usually **cannot guarantee the exact model**. For deeper identification, combine it with tools like **Nmap** or **Wireshark**. 🔍