**Cybersecurity hand-on youtube course:** https://youtu.be/ug8W0sFiVJo

---

## Cybersecurity Fundamentals – Linux & Wireless Notes

## ===== FILE & DIRECTORY NAVIGATION =====

`pwd` — Display the current working directory.

`ls` — List files and directories.

`ls -a` — List all files, including hidden ones.

`ls -l` — Display files in detailed (long) format.

`ls -lh` — Display detailed file information with human-readable sizes.

`cd` — Change the current directory.

`mkdir -p` — Create directory/directories, including parent directories if needed.

---

## ===== FILE MANAGEMENT =====

`cat -n` — Display a file with line numbers.

`cp` — Copy a file.

`cp -r` — Copy a directory and its contents recursively.

`rm` — Delete a file.

`rm -r` — Delete a directory and its contents recursively.

`rm -f` — Force delete a file without confirmation.

---

## ===== TEXT PROCESSING =====

`grep -n` — Search for text and show matching line numbers.

`wc -w` — Count the number of words in a file.

`head -n [lines]` — Display the first specified number of lines.

---

## ===== SYSTEM INFORMATION =====

`whoami` — Display the current username.

`hostname` — Display the system hostname.

`id` — Show user and group IDs.

`history` — Display previously executed commands.

`clear` — Clear the terminal screen.

`exit` — Exit the current terminal session.

`man` — Open the manual page for a command.

---

## ===== NETWORKING =====

`ip` — Display or configure network settings.

`ip addr show` — Show detailed network interface information.

`ip a` — Short version of `ip addr show`.

`iwconfig` — Display or configure wireless network interfaces.

`sudo ifconfig [interface] up` — Enable a network interface.

`sudo systemctl restart NetworkManager` — Restart the NetworkManager service.

---

## ===== PACKAGE MANAGEMENT =====

`sudo apt remove` — Remove an installed package.

`sudo apt autoremove` — Remove unused packages and dependencies.

---

## ===== NMAP =====

`nmap --help` — Display Nmap help and available options.

`nmap -sP` — Ping scan to discover active hosts (legacy syntax; modern equivalent is `-sn`).

---

# ===== AIRCRACK-NG SUITE =====

## General

`aircrack-ng` — Crack captured Wi-Fi handshakes using a wordlist.

`airodump-ng` — Capture Wi-Fi packets and display nearby wireless networks.

`airmon-ng` — Enable or disable monitor mode on wireless interfaces.

---

## Monitor Mode

`sudo airmon-ng check` — Show processes that may interfere with monitor mode.

`sudo airmon-ng check kill` — Stop interfering network processes.

`sudo airmon-ng start [interface]` — Enable monitor mode on the selected interface.

`sudo airmon-ng stop [interface]` — Disable monitor mode.

`sudo systemctl restart NetworkManager` — Restore normal networking after monitor mode.

---

## Packet Capture

`sudo airodump-ng [interface monitor]` — Capture nearby wireless traffic.

`sudo airodump-ng [interface monitor] --write [directory]` — Save captured packets to files.

`sudo airodump-ng --band a|b|g|ag [interface monitor]` — Scan selected Wi-Fi frequency bands.

`sudo airodump-ng --bssid [MAC] -c [channel] --write [directory] [interface monitor]` — Capture packets from one specific access point.

---

## Channel Selection

`sudo iwconfig [interface monitor] channel [channel]` — Lock the interface to a specific Wi-Fi channel.

---

## Deauthentication

`sudo aireplay-ng --deauth [packets] -a [AP MAC] -c [Client MAC] [interface monitor]` — Send deauthentication packets to a client or access point.

`sudo mdk4 [interface monitor] d -c [channel]` — Perform a deauthentication attack on a selected channel.

---

## Password Cracking

`sudo aircrack-ng [handshake file] -w [wordlist]` — Attempt to crack a captured WPA/WPA2 handshake.

`cd /usr/share/wordlists/` — Navigate to the default Linux wordlist directory.

`sudo gunzip [file.gz]` — Extract a compressed wordlist (e.g., `rockyou.txt.gz`).

---

# ===== WIRESHARK =====

`wireshark` — Launch Wireshark.

`wireshark [capture.cap]` — Open a saved capture file.

---

## Useful Display Filters

`wlan.fc.type_subtype == 12` — Show only deauthentication packets.

`wlan.fc.type_subtype == 11` — Show only authentication packets.

---

# ===== IMPORTANT TERMS =====

**EAPoL (Extensible Authentication Protocol over LAN)** — Protocol used to exchange authentication messages during WPA/WPA2/WPA3 handshakes.

**4-Way Handshake** — Authentication process between a client and an access point used to establish encryption keys. Capturing this exchange allows password testing against a wordlist.

**Monitor Mode** — Wireless interface mode that captures all nearby Wi-Fi traffic instead of only traffic intended for the device.

**Deauthentication Packet** — A management frame that disconnects a client from a Wi-Fi network. Often used during wireless security testing to force a client to reconnect and generate a new handshake.



































