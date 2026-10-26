# 🌐 ARP Command — Windows

> [!abstract] Overview **ARP (Address Resolution Protocol)** maps an **IPv4 address** to a **MAC address** on a local network.
> 
> In simple terms, ARP helps your computer discover which physical network device corresponds to a local IP address.

## 🧠 How It Works

When your computer needs to communicate with another device on the local network, it may use ARP to find that device's MAC address.

**Example:**

`192.168.1.10` → `AA-BB-CC-11-22-33`

- **IP address:** Identifies the device at the network layer.
- **MAC address:** Identifies the network interface at the link layer.
- **ARP cache:** Stores recently learned IP-to-MAC mappings.

> [!tip] Remember ARP is used for **IPv4**, not IPv6. IPv6 uses Neighbor Discovery Protocol (NDP).

## ⚡ Basic Syntax

```
arp [-a] [-d] [-s] [inet_addr] [if_addr]
```

Run these commands in **Command Prompt (CMD)** or **PowerShell** on Windows.

## 🛠️ Common ARP Commands

### 1. Display the ARP Cache

```
arp -a
```

Displays cached IP-to-MAC address mappings.

**Use it when:** You want to see which local IPv4 addresses your computer has recently resolved.

### 2. Display the Cache for a Specific Interface

```
arp -a -N 192.168.1.10
```

Displays ARP entries associated with the interface using the specified local IPv4 address.

**Use it when:** Your computer has multiple network interfaces.

### 3. Display the ARP Cache for All Interfaces

```
arp -a
```

Lists entries for the available interfaces, including their interface addresses.

### 4. Delete an ARP Cache Entry

```
arp -d 192.168.1.1
```

Deletes the cached entry for the specified IP address, where supported by the interface and permissions.

**Use it when:** Troubleshooting a stale or incorrect ARP mapping.

> [!warning] Administrator privileges Deleting entries may require an elevated terminal. Windows may also reject deletion of permanent entries.

### 5. Add a Static ARP Entry

```
arp -s 192.168.1.50 AA-BB-CC-11-22-33
```

Adds a static mapping between an IPv4 address and a MAC address.

**Use it when:** A specific troubleshooting or network configuration task requires a fixed mapping.

> [!caution] Be careful Static entries can interfere with connectivity if configured incorrectly. Use a valid MAC address for the intended device.

## 🔍 Practical Example

Suppose your router has the IP address `192.168.1.1`.

**Step 1 — Check the ARP cache**

```
arp -a
```

**Step 2 — Look for the router's IP address**

```
Internet Address      Physical Address      Type
192.168.1.1           AA-BB-CC-11-22-33     dynamic
```

**Step 3 — Understand the result**

- `192.168.1.1` — the router's IPv4 address.
- `AA-BB-CC-11-22-33` — the corresponding MAC address.
- `dynamic` — the mapping was learned automatically.

If the router's entry is missing, your computer may not have recently needed to resolve that address. You can try communicating with the router and then check `arp -a` again.

## 🧰 Quick Reference

|Command|Purpose|
|---|---|
|`arp -a`|Display ARP cache entries|
|`arp -a -N <IP>`|Show entries for a specific interface|
|`arp -d <IP>`|Delete a cached mapping|
|`arp -d *`|Delete dynamic ARP cache entries, subject to permissions and Windows behavior|
|`arp -s <IP> <MAC>`|Add a static mapping|

## 📝 Important Notes

- ARP resolves addresses on the **local network segment**; it does not discover every device on the internet.
- When contacting a remote IP address, your computer normally resolves the MAC address of its **next-hop router**, not the remote server.
- The ARP cache may contain only devices your computer has recently communicated with.
- An ARP entry does not necessarily prove that a device is currently online.
- `arp` displays IPv4 mappings; use other tools for IPv6 neighbor information.

## 🔗 Related Commands

- `ipconfig` — View IP configuration.
- `ping` — Test connectivity to an IP address.
- `getmac` — Display local network adapter MAC addresses.
- `route print` — View the Windows routing table.
- `netstat -ano` — Inspect network connections and listening ports.

---
