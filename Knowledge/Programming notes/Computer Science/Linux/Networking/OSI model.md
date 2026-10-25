![[Pasted image 20261019062453.png|648]]

---

# 🌐 OSI Model

> [!abstract] Overview The **OSI (Open Systems Interconnection) model** explains how data travels between devices over a network by dividing communication into **7 layers**. Each layer has a specific job.

## 🧱 The 7 Layers

|Layer|Name|Main Function|Example|
|---|---|---|---|
|7|**Application**|Network services used by applications|HTTP, DNS, SMTP|
|6|**Presentation**|Data format, encryption, compression|TLS, UTF-8, JPEG|
|5|**Session**|Manages communication sessions|Session control|
|4|**Transport**|End-to-end delivery, ports, reliability|TCP, UDP|
|3|**Network**|Logical addressing and routing|IP, routers|
|2|**Data Link**|Local delivery using MAC addresses|Ethernet, switches|
|1|**Physical**|Transmits raw bits as signals|Cables, radio, hubs|

## 🧠 Easy Way to Remember

From Layer 7 down to Layer 1:

**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing.

- Application
- Presentation
- Session
- Transport
- Network
- Data Link
- Physical

> [!tip] Quick memory trick
> 
> - **L1:** Signals and bits
> - **L2:** MAC addresses
> - **L3:** IP addresses
> - **L4:** TCP/UDP and ports
> - **L5–L7:** Sessions, data representation, and application services

## 📦 Example: Opening a Website

When you visit `https://example.com`:

1. **Application (L7):** Your browser uses HTTP.
2. **Presentation (L6):** Data representation and encryption are handled here conceptually.
3. **Session (L5):** Communication sessions are managed conceptually.
4. **Transport (L4):** TCP or, with HTTP/3, UDP carries the transport traffic.
5. **Network (L3):** IP routes packets toward the destination.
6. **Data Link (L2):** Ethernet or Wi-Fi carries frames across the local link.
7. **Physical (L1):** Bits travel as electrical, optical, or radio signals.

The receiving device processes the data in reverse, from Layer 1 to Layer 7.

> [!note] Real-world clarification The OSI model is a conceptual framework. Real protocols do not always fit neatly into one layer, and modern networking commonly uses the TCP/IP model as well.

## 🔎 Useful Linux Commands

```bash
# Layer 2 — interfaces and MAC addresses
ip link show

# Layer 3 — IP addresses and interfaces
ip addr show

# Layer 3 — routing table
ip route

# Layer 4 — listening ports and connections
ss -tuln

# Test Layer 3 connectivity
ping -c 4 8.8.8.8

# Inspect packets and protocols
sudo tcpdump -i any
```

---
