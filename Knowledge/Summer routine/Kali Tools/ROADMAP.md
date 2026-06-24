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

### Nessus / OpenVAS

Purpose: Vulnerability scanning  
Key concepts:

- CVE detection
- CVSS risk scoring
- Automated reporting

Notes:  
Identifies known vulnerabilities in systems and services.

---

### Nikto

Purpose: Web server scanning  
Key concepts:

- Misconfigurations
- Outdated software detection
- CGI vulnerabilities

Notes:  
Fast, lightweight web server scanner.

---

## 3. Web Application Testing

### Burp Suite

Purpose: Web application security testing  
Key concepts:

- Intercepting proxy
- Request/response manipulation
- Repeater (manual testing)
- Intruder (automated attacks)

Notes:  
Industry-standard tool for web security testing.

---

### OWASP ZAP

Purpose: Web vulnerability scanner  
Key concepts:

- Passive scanning
- Active scanning
- Spidering applications
- OWASP Top 10 mapping

Notes:  
Good free alternative to Burp Suite.

---

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

### Aircrack-ng Suite

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

## 6. Exploitation

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

### Wireshark

Purpose: Packet analysis tool  
Key concepts:

- PCAP analysis
- Protocol decoding
- Filtering (display/capture filters)

Notes:  
Essential for understanding network traffic.

---

### tcpdump

Purpose: CLI packet capture  
Key concepts:

- Lightweight sniffing
- Filtering by IP/port
- Capture file generation

Notes:  
Useful when GUI tools are unavailable.

---

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

## 10. Privilege Escalation

### LinPEAS / WinPEAS

Purpose: System enumeration  
Key concepts:

- Misconfiguration detection
- Credential discovery
- Privilege escalation paths

Notes:  
Automates post-exploitation analysis.

---

### Linux Exploit Suggester

Purpose: Kernel exploit mapping  
Key concepts:

- Kernel version analysis
- CVE matching
- Exploit suggestions

Notes:  
Helps identify potential escalation opportunities.

---

## 11. Wordlists & Generation Tools

### Crunch

Purpose: Wordlist generation  
Key concepts:

- Pattern-based generation
- Charset selection
- Length constraints

Notes:  
Used for custom brute-force lists.

---

### SecLists

Purpose: Security wordlist collection  
Key concepts:

- Password lists
- Directory brute-force lists
- User enumeration lists

Notes:  
Essential resource for penetration testing.