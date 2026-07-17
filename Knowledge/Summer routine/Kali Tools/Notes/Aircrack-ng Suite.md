# 🔐 Aircrack-ng (Simple Notes)

## 📌 What is Aircrack-ng?

**Aircrack-ng** is a free tool used to **test Wi-Fi security**. It helps security professionals check whether a wireless network is secure.

---

## 🛠️ What can Aircrack-ng do?

📡 **Capture Wi-Fi traffic** — Collect packets from nearby wireless networks.

👀 **Monitor networks** — Show Wi-Fi names (SSID), MAC addresses, channels, and connected devices.

📁 **Save captured packets** — Store network traffic in `.cap` files for later analysis.

🔑 **Test Wi-Fi passwords** — Try passwords from a **wordlist** against a captured WPA/WPA2 handshake.

📶 **Enable Monitor Mode** — Allow the wireless adapter to listen to all nearby Wi-Fi traffic.

📤 **Send deauthentication packets** — Disconnect a device so it reconnects and creates a new handshake (used during authorized security testing).

---

## 📦 Main Tools

🔹 **airmon-ng** — Enable or disable Monitor Mode.

🔹 **airodump-ng** — Capture Wi-Fi packets and collect information about networks.

🔹 **aireplay-ng** — Send packets, such as deauthentication packets.

🔹 **aircrack-ng** — Test a captured WPA/WPA2 handshake using a wordlist.

---

# 🛠️ Main Tools & Commands

**Detailed notes:** [[Notes_1]]

## 📡 Enable Monitor Mode

`sudo airmon-ng check` — Show processes that may cause problems.

`sudo airmon-ng check kill` — Stop interfering processes.

`sudo airmon-ng start wlan0` — Enable Monitor Mode.

`sudo airmon-ng stop wlan0mon` — Disable Monitor Mode.

`sudo systemctl restart NetworkManager` — Restore normal Wi-Fi after testing.

---

## 📶 Scan Wi-Fi Networks

`sudo airodump-ng wlan0mon` — Display nearby Wi-Fi networks.

`sudo airodump-ng --band ag wlan0mon` — Scan both 2.4 GHz and 5 GHz networks.

`sudo airodump-ng wlan0mon --write capture` — Save captured packets to files.

---

## 🎯 Capture One Wi-Fi Network

`sudo airodump-ng --bssid AA:BB:CC:DD:EE:FF -c 6 --write handshake wlan0mon`

➡️ Capture packets from one access point on channel **6** and save the capture.

---

## 📤 Send Deauthentication Packets

`sudo aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon`

➡️ Send **10 deauthentication packets** to the selected access point.

---

## 🔑 Test a Captured Handshake

`sudo aircrack-ng handshake.cap -w /usr/share/wordlists/rockyou.txt`

➡️ Test passwords from the **rockyou.txt** wordlist against the captured WPA/WPA2 handshake.

---

## 📂 Wordlists

`cd /usr/share/wordlists/`

➡️ Open the default wordlist directory.

`sudo gunzip rockyou.txt.gz`

➡️ Unzip the **rockyou.txt** wordlist.

---

# 📋 Typical Workflow


1️⃣ Enable **Monitor Mode** (`airmon-ng`).

2️⃣ Scan nearby Wi-Fi networks (`airodump-ng`).

3️⃣ Choose the target **BSSID** and **channel**.

4️⃣ Capture the **4-Way Handshake**.

5️⃣ (Optional) Send **deauthentication packets** (`aireplay-ng`) to make a client reconnect.

6️⃣ Test the captured handshake using a **wordlist** (`aircrack-ng`).

---


## 💡 Important Terms

📡 **Monitor Mode** — Listen to all nearby Wi-Fi traffic.

🤝 **4-Way Handshake** — Authentication process used when a device connects to a WPA/WPA2 Wi-Fi network.

📖 **Wordlist** — A file that contains many possible passwords (for example, `rockyou.txt`).

📁 **.cap file** — A file that stores captured network packets.

---

## ✅ Remember

- 🆓 Aircrack-ng is **free and open-source**.
    
- 🐧 It is commonly used on **Linux**.
    
- 🛡️ Use it **only on networks you own or have permission to test**.
    
- 🎓 It is a popular tool for learning **wireless cybersecurity** and **ethical hacking**.

---
