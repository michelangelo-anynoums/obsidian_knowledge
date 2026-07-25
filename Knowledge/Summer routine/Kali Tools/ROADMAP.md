# Kali Linux Essential Tools — Learning Notes

## 1. Reconnaissance / Information Gathering

### Nmap

Purpose: Network discovery and port scanning  
Key concepts:

- Host discovery (`-sn`)
- Port scanning (TCP/UDP)
- Service and version detection (`-sV`)
- OS fingerprinting (`-O`)

Notes:  
Nmap is a foundational tool for mapping networks and identifying exposed services.

---

### theHarvester

Purpose: Open-source intelligence (OSINT) gathering  
Key concepts:

- Email and domain enumeration
- Metadata collection
- Passive data gathering

Notes:  
Used for early-stage reconnaissance without direct interaction with targets.

---

### Recon-ng

Purpose: OSINT framework  
Key concepts:

- Modular architecture
- API integrations
- Automated reconnaissance workflows

Notes:  
Best for structured and repeatable intelligence gathering.

---

## 2. Vulnerability Analysis

### Nikto

Purpose: Web server scanning  
Key concepts:

- Misconfigurations
- Outdated software detection
- CGI vulnerabilities

Notes:  
Fast, lightweight web server scanner.


---

## 3. Directory brute force
### Dirb

Purpose: Web directory brute-forcing  
Key concepts:

- Wordlist-based directory discovery
- Hidden file enumeration
- HTTP response analysis

Notes:  
Used to find hidden directories and files on web servers.

---

### DirBuster

Purpose: GUI-based directory brute force tool  
Key concepts:

- Multi-threaded scanning
- Large wordlist support
- Recursive scanning

Notes:  
Similar to Dirb but with a graphical interface and deeper scanning options.

---

## 4. Password Attacks

### Hydra

Purpose: Login brute-force tool  
Key concepts:

- Dictionary attacks
- Multiple protocols (SSH, FTP, HTTP, etc.)
- Parallel login attempts

Notes:  
Used against weak authentication systems.

---

### John the Ripper

Purpose: Password hash cracking  
Key concepts:

- Offline cracking
- Wordlist attacks
- Rule-based mutations

Notes:  
Common tool for testing password strength.

---

### Hashcat

Purpose: GPU-accelerated password cracking  
Key concepts:

- Hash type selection
- Mask attacks
- GPU optimization

Notes:  
One of the fastest password cracking tools available.

---

## 5. Wireless Attacks

### Aircrack-ng Suite [[Aircrack-ng Suite]]

Purpose: Wi-Fi security testing  
Key concepts:

- Monitor mode
- Packet capture
- WPA/WPA2 handshake cracking

Notes:  
Used for analyzing wireless network security.

---

### Wifite

Purpose: Automated wireless attack tool  
Key concepts:

- Automated scanning
- Handshake capture
- Aircrack integration

Notes:  
Simplifies wireless penetration testing.

---

### Arp-scan [[arp-scan]]

Purpose: Reconnaissance tool
Key concepts:

- Automated scanning
- MAC address identifying

Notes:  
Simplifies wireless penetration testing. Gathers information about connected devices to a local network

---

### mdk4 [[mdk4 tool]]

Purpose: Wi-Fi packets injection / testing
Key concepts:

- Automated scanning
- Packets injection (deauth)

Notes:  
Simplifies wireless penetration testing.

---

## 6. Exploitation

### SQLmap [[SQLmap]]

Purpose: SQL injection
Key concepts:

- Web SQL injection
- Injection commands
- Automation

Notes:
Must know tool for web vulnerability exploitation
### Metasploit Framework

Purpose: Exploitation framework  
Key concepts:

- Exploit modules
- Payload generation
- Meterpreter sessions
- Post-exploitation tools

Notes:  
Core framework for vulnerability exploitation.

---

## 7. Sniffing & Traffic Analysis
### Scapy

Purpose: Packet crafting and network manipulation  
Key concepts:

- Packet creation and modification
- Network scanning
- Custom packet injection
- Protocol-level control

Notes:  
Very powerful for advanced network testing and custom packet analysis.

---

## 8. Remote Access / Authentication

### SSH (Secure Shell)

Purpose: Secure remote system access  
Key concepts:

- Encrypted remote login
- Key-based authentication
- Port forwarding (tunneling)
- Secure file transfer (SCP/SFTP)

Notes:  
One of the most important protocols for secure remote administration.

---

## 9. Social Engineering

### Social-Engineer Toolkit (SET)

Purpose: Human-based attack simulation  
Key concepts:

- Phishing page creation
- Credential harvesting
- Attack vector simulation

Notes:  
Focuses on exploiting human behavior rather than systems.

---

## 10. Wordlists & Generation Tools

### Crunch

Purpose: Wordlist generation  
Key concepts:

- Pattern-based generation
- Charset selection
- Length constraints

Notes:  
Used for custom brute-force lists.

---
