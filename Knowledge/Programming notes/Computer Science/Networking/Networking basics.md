# 🌐 Networking Fundamentals

![[Pasted image 20261028075943.png|540]]

> [!abstract] 🎯 Goal Understand IP addresses, binary, subnet masks, NAT, and subnetting.

## 1. 📍 IP Addresses

An **IP address** identifies a network interface so data can reach the correct device.

Example: `192.168.1.10`

- IPv4 = **32 bits** (4 octets)
- Each octet = 8 bits
- Each octet ranges from `0–255`

> [!important] Binary representation:

```text
11111111.11111111.11111111.00000000
```

![[Pasted image 20261028075013.png|684]]
### ⚙️ Essential settings

|Setting|Purpose|Example|
|---|---|---|
|IP address|Device address|`192.168.1.10`|
|Subnet mask|Defines the subnet|`255.255.255.0`|
|Default gateway|Route to other networks|`192.168.1.1`|

![[Pasted image 20261028075202.png|538]]

### 💻 Useful commands

```powershell
# Windows
ipconfig
ipconfig /all
```

```bash
# Linux
ip a
ifconfig
```

## 2. 🏠 Network vs. Host

Example: `192.168.1.10/24`

- 🌐 Network: `192.168.1.0`
- 💻 Host: `10` (in this example)
- 🚪 Gateway: often `192.168.1.1`
- 📢 Broadcast: `192.168.1.255`

The `/24` means **24 network bits + 8 host bits**.

![[Pasted image 20261028075313.png|427]]

![[Pasted image 20261028075609.png]]
## 3. 🔢 IPv4 Address Capacity

$$2^{32}=4,294,967,2962$$

Approximately **4.3 billion possible IPv4 addresses**.

![[Pasted image 20261028075629.png]]
### Historical address classes

|Class|First octet|Purpose|
|---|---|---|
|A|1–126|Historically large networks|
|B|128–191|Medium networks|
|C|192–223|Small networks|
|D|224–239|Multicast|
|E|240–255|Reserved/experimental|

![[Pasted image 20261028075846.png|338]]

Today, networks primarily use **CIDR** (`/24`, `/26`, etc.) instead of address classes.

### 🔄 Loopback

`127.0.0.1` = your own device (`localhost`).

bash

```
ping 127.0.0.1
```



## 4. 🔒 Private IPs & NAT

RFC 1918 defines three private IPv4 ranges.

|Private range|CIDR|
|---|---|
|`10.0.0.0–10.255.255.255`|`10.0.0.0/8`|
|`172.16.0.0–172.31.255.255`|`172.16.0.0/12`|
|`192.168.0.0–192.168.255.255`|`192.168.0.0/16`|

### 🌍 How NAT works

**NAT = Network Address Translation**

Multiple private devices can share one public IPv4 address through NAT/PAT.

1. 💻 Laptop sends a request.
2. 🛜 Router translates the source address and tracks the connection.
3. 🌍 Website replies to the public address.
4. 🏠 Router forwards the reply to the correct device.

![[Pasted image 20261028082816.png|548]]

> [!note] ⚠️ NAT ≠ Firewall. 
> NAT translates addresses. A firewall controls which traffic is allowed.

## 5. 🚀 IPv4 vs. IPv6

| Feature          | IPv4           | IPv6            |
| ---------------- | -------------- | --------------- |
| Size             | 32 bits        | 128 bits        |
| Format           | Decimal        | Hexadecimal     |
| Example          | `192.168.1.10` | `2001:db8::10`  |
| Address capacity | $$2322^{32}$$  | $$21282^{128}$$ |

IPv6 provides an enormous address space, reducing the need to conserve public addresses through IPv4-style NAT.

## 6. 🔢 Binary Numbers

Computers use two values: `0` and `1`.

Each binary position represents a power of two.

|Bit position|7|6|5|4|3|2|1|0|
|---|---|---|---|---|---|---|---|---|
|Value|128|64|32|16|8|4|2|1|

### Binary → Decimal

Example: `11000000`

$$128+64=192$$

Result: **192**

![[Pasted image 20261028083315.png|319]]

### Decimal → Binary

Example: `17`

![[imgupscaler-enhanced.jpg|407]]

Result: `10001`

### ⚡ Remember

- `11111111` = 255
- `10000000` = 128
- `11000000` = 192
- `11111100` = 252

## 7. 🎭 Subnet Masks

> [!abstract] A subnet mask separates network bits (`1`) from host bits (`0`).

Example:

```text
255.255.255.0
11111111.11111111.11111111.00000000
```

This is `/24`.

### 📊 Common masks

|CIDR|Subnet mask|Total IPs|Usable hosts*|
|---|---|---|---|
|`/24`|`255.255.255.0`|256|254|
|`/25`|`255.255.255.128`|128|126|
|`/26`|`255.255.255.192`|64|62|
|`/27`|`255.255.255.224`|32|30|
|`/28`|`255.255.255.240`|16|14|
|`/29`|`255.255.255.248`|8|6|
|`/30`|`255.255.255.252`|4|2|

*For conventional IPv4 subnets, excluding the network and broadcast addresses.*
## 8. ✂️ Subnetting

> [!important] **Subnetting = dividing one network into smaller networks.**

Useful for separating departments, reducing broadcast domains, and organizing IP addresses.

### 🧩 Example: Create 4 subnets

Starting network: `192.168.1.0/24`

**Step 1 — Borrow 2 bits**

$$22=4 (subnets)$$

**Step 2 — Calculate the new prefix**

`/24 + 2 = /26`

New mask: `255.255.255.192`

Binary last octet: `11000000`

**Step 3 — Calculate subnet size**

$$26=64(IPs)$$

$$2^6=64\text{ IPs per subnet}$$

**Step 4 — Find the ranges**

|Subnet|Network|Usable hosts|Broadcast|
|---|---|---|---|
|1|`192.168.1.0/26`|`.1–.62`|`.63`|
|2|`192.168.1.64/26`|`.65–.126`|`.127`|
|3|`192.168.1.128/26`|`.129–.190`|`.191`|
|4|`192.168.1.192/26`|`.193–.254`|`.255`|

The abbreviated addresses refer to `192.168.1.x`.

## 9. ☕ Practical Example: Café Network

Separate devices into three networks.

|Department|Devices needed|Subnet|Usable hosts|
|---|---|---|---|
|👥 Customers|50|`/26`|62|
|💻 Staff|20|`/27`|30|
|💳 Payment terminals|10|`/28`|14|

Example allocation from `192.168.10.0/24`:

|Network|Subnet|Example gateway|
|---|---|---|
|Customers|`192.168.10.0/26`|`192.168.10.1`|
|Staff|`192.168.10.64/27`|`192.168.10.65`|
|Payments|`192.168.10.96/28`|`192.168.10.97`|

> [!question] 💡 Different subnets alone do not guarantee isolation. Use appropriate VLANs and firewall rules to restrict communication between customers, staff, and payment devices.

![[Pasted image 20261028084438.png|619]]

## 10. 🧠 Reverse Subnetting (VLSM)

**VLSM = Variable Length Subnet Masking.**

Instead of starting with a subnet mask, start with the number of hosts needed.

Example: `192.168.20.0/24`

|Required hosts|Subnet|Usable hosts|
|---|---|---|
|100|`/25`|126|
|50|`/26`|62|
|20|`/27`|30|
|10|`/28`|14|

Allocate from largest to smallest:

|Network|Allocation|
|---|---|
|A|`192.168.20.0/25`|
|B|`192.168.20.128/26`|
|C|`192.168.20.192/27`|
|D|`192.168.20.224/28`|

Each subnet must start at a valid boundary, and the ranges must not overlap.

## 📝 Quick Revision

- 🌐 **IP address:** Identifies a network interface.
- 🎭 **Subnet mask:** Separates network and host bits.
- 🚪 **Gateway:** Routes traffic to other networks.
- 🔒 **NAT/PAT:** Allows private devices to share a public IPv4 address.
- 🔢 **Binary:** The foundation of IP addressing and subnetting.
- ✂️ **Subnetting:** Divides a network into smaller networks.
- 🧩 **VLSM:** Creates subnets of different sizes.

> [!success] 🎯 The key skill Learn to move between **CIDR prefixes, subnet masks, binary, block sizes, and host ranges**. Once these are connected, subnetting becomes much easier.