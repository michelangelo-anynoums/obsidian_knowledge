# 🕸️ ARP Spoofing · Bettercap · Wireshark

> [!info] 🎯 Purpose Quick reference for **Kali Linux network analysis**, ARP inspection, Bettercap configuration, and Wireshark filters.

## What is `arp`?

`arp` **(Address Resolution Protocol)** maps IPv4 addresses to MAC addresses on a local network.

![[Pasted image 20261020065831.png|565]]

## 🧭 01 · ARP Basics

**ARP** maps IPv4 addresses to MAC addresses on a local network.

```bash
ip neigh
```

🔎 View known neighbors.

```bash
arp -a
```

📋 Display cached ARP entries.

```bash
ip neigh show
```

🖥️ Inspect IP-to-MAC mappings.

**Example output:**

```bash
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

- `192.168.1.1` → IP address
- `aa:bb:cc:dd:ee:ff` → MAC address
- `REACHABLE` → Neighbor currently considered reachable

---

## ⚡ 02 · Bettercap — ARP Spoofing


### 🔁 `arp.spoof.fullduplex true`

Enables spoofing in both directions.

```bash
set arp.spoof.fullduplex true
```

💡 **Example:** Test bidirectional traffic visibility between two authorized lab devices.

### 🎯 `arp.spoof.targets`

Defines the target IP address or addresses.

```bash
set arp.spoof.targets 192.168.1.20
```

💡 **Example:** Select a single lab device at `192.168.1.20`.

### 🚀 `arp.spoof on`

Enables the ARP spoofing module using the configured settings.

```bash
arp.spoof on
```

💡 **Example:** Start the module during an authorized, isolated lab test.

> [!note] ⚙️ Bettercap setup Interface selection, installation, and complete configuration:


> 📎 **See:** [[Analyzing network]] 

---

## 🦈 03 · Wireshark Display Filters

> [!tip] 🔍 How to use Paste a filter into Wireshark's **Display Filter** bar and press Enter.

### 📡 ARP Filters

|Filter|Purpose|
|---|---|
|`arp`|📦 All ARP packets|
|`arp.opcode == 1`|❓ ARP requests|
|`arp.opcode == 2`|💬 ARP replies|
|`arp.src.proto_ipv4 == 192.168.1.10`|🎯 ARP packets claiming this sender IP|
|`arp.dst.proto_ipv4 == 192.168.1.1`|📍 ARP packets targeting this IP|

**Example:** Find ARP replies.

```bash
arp.opcode == 2
```

### 🌐 IP & Host Filters

|Filter|Purpose|
|---|---|
|`ip.addr == 192.168.1.20`|↔️ Traffic to/from a host|
|`ip.src == 192.168.1.20`|📤 Packets from a host|
|`ip.dst == 192.168.1.20`|📥 Packets to a host|
|`eth.addr == aa:bb:cc:dd:ee:ff`|🪪 Frames involving a MAC|

**Example:** Inspect traffic involving a lab device.

```
ip.addr == 192.168.1.20
```

### 🔌 Protocol & Port Filters

|Filter|Purpose|
|---|---|
|`tcp`|🔗 TCP traffic|
|`udp`|⚡ UDP traffic|
|`dns`|🌍 DNS queries and responses|
|`icmp`|📶 ICMP traffic|
|`tcp.port == 80`|🌐 TCP port 80|
|`tcp.port == 443`|🔒 TCP port 443|
|`tcp.flags.syn == 1 && tcp.flags.ack == 0`|🤝 TCP connection attempts|

**Example:** Inspect DNS traffic.

```
dns
```

### 🧩 Combined Filters

|Filter|Purpose|
|---|---|
|`arp && arp.opcode == 2`|ARP replies only|
|`dns||
|`ip.addr == 192.168.1.20 && tcp`|TCP traffic involving a host|
|`arp.src.proto_ipv4 == 192.168.1.1 && arp.opcode == 2`|ARP replies claiming the gateway IP|

**Operators:**

- `&&` → AND · both conditions must match
- `||` → OR · either condition can match
- `!` → NOT · exclude a condition

---

## 🚨 04 · Detect Suspicious ARP Activity

Start with:

```bash
arp
```

🔎 Check for:

- ⚠️ Multiple MAC addresses claiming the same IP.
- 🔄 Unexpected changes to the gateway's MAC address.
- 📢 Unusual or repeated ARP replies.
- 📈 Sudden ARP activity alongside connectivity issues.

**Example investigation:** Compare the gateway's advertised MAC address with a trusted record.

> [!caution] 🧠 Remember These signs are clues, not proof of spoofing. Legitimate network changes can produce similar patterns.

---

## ⚡ 05 · Pocket Cheat Sheet

|Task|Command / Filter|
|---|---|
|🧭 Inspect neighbors|`ip neigh`|
|📡 Show ARP|`arp`|
|❓ ARP requests|`arp.opcode == 1`|
|💬 ARP replies|`arp.opcode == 2`|
|🎯 Filter a host|`ip.addr == 192.168.1.20`|
|🌍 Filter DNS|`dns`|
|🔒 Filter HTTPS|`tcp.port == 443`|
|🔁 Full-duplex setting|`set arp.spoof.fullduplex true`|
|🎯 Target setting|`set arp.spoof.targets 192.168.1.20`|
|🚀 Enable module|`arp.spoof on`|

---