# 🐉 Kali Linux — Essential Tools

> [!abstract] Overview A quick-reference guide to essential Kali Linux tools for reconnaissance, vulnerability analysis, penetration testing, password auditing, wireless security, and network analysis.

## 1. 🔎 Reconnaissance & Information Gathering

### Nmap

**Purpose:** Network discovery and port scanning.

- Host discovery: `-sn`
- TCP/UDP port scanning
- Service and version detection: `-sV`
- OS detection: `-O`

**Notes:** Maps networks, identifies open ports, and discovers exposed services.

---

### theHarvester

**Purpose:** Open-source intelligence (OSINT).

- Email and domain enumeration
- Metadata collection
- Passive information gathering

**Notes:** Collects publicly available information during early-stage reconnaissance.

---

### Recon-ng

**Purpose:** Modular OSINT framework.

- Modular architecture
- API integrations
- Automated reconnaissance workflows

**Notes:** Supports structured, repeatable intelligence gathering.

---

### arp-scan [[arp-scan]]

**Purpose:** Local network discovery.

- Discovers devices on a local network
- Identifies MAC addresses
- Helps map connected hosts

**Notes:** Useful for identifying devices on a local network, particularly on Ethernet and compatible local segments.

---

## 2. 🛡️ Vulnerability Analysis

### Nikto

**Purpose:** Web server security scanning.

- Detects common misconfigurations
- Identifies outdated software
- Checks for potentially dangerous files and CGI issues

**Notes:** A lightweight scanner for identifying common web server weaknesses.

---

## 3. 📂 Web Content & Directory Discovery

### Dirb

**Purpose:** Web directory and file discovery.

- Wordlist-based enumeration
- Hidden directory and file discovery
- HTTP response analysis

**Notes:** Uses wordlists to discover web paths that may not be linked publicly.

---

### DirBuster

**Purpose:** GUI-based web content discovery.

- Multi-threaded scanning
- Large wordlist support
- Recursive scanning

**Notes:** A graphical alternative for discovering directories and files on web servers.

---

### cURL [[cURL]]

**Purpose:** Command-line tool for transferring data using URLs.

- Sends HTTP requests: `GET`, `POST`, and others
- Inspects response headers
- Submits form data and JSON
- Supports cookies, authentication, and redirects
- Works with HTTP, HTTPS, FTP, and other protocols

**Notes:** Essential for testing web endpoints, inspecting HTTP behavior, debugging APIs, and understanding client-server communication.

---

## 4. 🔑 Password Auditing

### Hydra

**Purpose:** Online login security testing.

- Dictionary-based authentication testing
- Supports protocols such as SSH, FTP, and HTTP
- Parallel login attempts

**Notes:** Evaluates authentication security in authorized testing environments.

---

### John the Ripper

**Purpose:** Password hash auditing.

- Offline password recovery
- Wordlist-based attacks
- Rule-based password mutations

**Notes:** Helps evaluate password strength by testing captured password hashes.

---

### Hashcat [[Hashcat]]

**Purpose:** High-performance password hash recovery.

- Hash type selection
- Mask and wordlist attacks
- GPU acceleration

**Notes:** A powerful tool for testing password strength and recovering passwords from supported hashes.

---

### Crunch [[Crunch]]

**Purpose:** Custom wordlist generation.

- Pattern-based generation
- Character set selection
- Minimum and maximum length constraints

**Notes:** Generates wordlists for password auditing and controlled security testing.

---

## 5. 📡 Wireless Security

### Aircrack-ng Suite [[Aircrack-ng Suite]]

**Purpose:** Wi-Fi security auditing.

- Monitor mode
- Wireless packet capture
- WPA/WPA2 handshake analysis

**Notes:** A collection of tools for analyzing wireless networks and assessing Wi-Fi security.

---

### mdk4 [[mdk4 tool]]

**Purpose:** Wireless network stress testing.

- Wireless frame injection
- Network resilience testing
- Deauthentication and other supported test modes

**Notes:** Used to evaluate wireless network resilience in authorized test environments.

---

## 6. 💥 Exploitation & Web Security

### SQLmap [[SQLmap]]

**Purpose:** Automated SQL injection testing.

- SQL injection detection
- Database fingerprinting
- Supported injection techniques
- Automated testing workflows

**Notes:** Helps identify and assess SQL injection vulnerabilities in web applications.

---

### Metasploit Framework

**Purpose:** Vulnerability validation and exploitation.

- Exploit modules
- Payload generation
- Meterpreter sessions
- Post-exploitation modules

**Notes:** A modular framework for validating vulnerabilities and conducting authorized penetration tests.

---

## 7. 🕵️ Packet Crafting & Traffic Analysis

### Scapy

**Purpose:** Packet crafting and network analysis.

- Creates and modifies packets
- Supports network scanning
- Enables custom packet transmission
- Provides protocol-level control

**Notes:** Useful for advanced network troubleshooting, protocol analysis, and custom security testing.

---

## 8. 🔐 Remote Access & Authentication

### SSH — Secure Shell [[SSH (Secure Shell)]]

**Purpose:** Secure remote system administration.

- Encrypted remote login
- Public-key authentication
- Port forwarding and tunneling
- Secure file transfer with SCP and SFTP

**Notes:** A fundamental protocol for securely administering remote systems.

---

## 9. 🎭 Social Engineering

### Social-Engineer Toolkit (SET)

**Purpose:** Authorized social engineering simulations.

- Phishing scenario creation
- Credential-harvesting simulations
- Attack-vector testing

**Notes:** Helps assess human-focused security risks through controlled security awareness exercises.

---

## 10. 🧭 Quick Reference

|Category|Tools|
|---|---|
|Reconnaissance|Nmap, theHarvester, Recon-ng, arp-scan|
|Vulnerability analysis|Nikto|
|Web discovery|Dirb, DirBuster, cURL|
|Password auditing|Hydra, John the Ripper, Hashcat, Crunch|
|Wireless security|Aircrack-ng, Wifite, mdk4|
|Exploitation|SQLmap, Metasploit|
|Network analysis|Scapy|
|Remote access|SSH|
|Social engineering|SET|

---
