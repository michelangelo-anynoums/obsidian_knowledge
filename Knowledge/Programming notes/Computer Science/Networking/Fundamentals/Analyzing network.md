# 🐉 Bettercap on Kali Linux

### Stylish Cheat Sheet · Commands & Practical Usage

## 🔎 1. What Is Bettercap?

**Bettercap** is a network security and penetration-testing framework used for network discovery, traffic analysis, protocol inspection, and authorized security assessments.

![[Pasted image 20261020062435.png|383]]

## ⚙️ 2. Installation & Updates

Update your package lists:

```bash
sudo apt update
```

Install Bettercap:

```bash
sudo apt install bettercap
```

Check the installed version:

```bash
bettercap --version
```

Display command-line options:

```bash
bettercap -h
```

## 🚀 3. Starting Bettercap

Start the interactive console:

```bash
sudo bettercap
```

Start Bettercap using a specific network interface:

```bash
sudo bettercap -iface eth0
```

> 💡 Replace `eth0` with the interface on your machine.

List network interfaces:

```bash
ip link show
```

Display IP addresses and interface details:

```bash
ip addr show
```

Display the routing table:

```bash
ip route
```

## 🧭 4. Essential Console Commands

Run these inside the Bettercap console.

|Command|Purpose|
|---|---|
|`help`|Display available commands|
|`help net.recon`|Show help for a specific command|
|`get`|Display configuration parameters|
|`get net.*`|Inspect network-related settings|
|`get net.interface`|Show the selected network interface|
|`net.show`|Display discovered network hosts|
|`quit`|Exit Bettercap|

💡 Use `help` whenever you need to discover available modules or check their syntax.

## 🌐 5. Network Discovery

Discover devices on a network you own or are authorized to assess.

Enable network reconnaissance:

```bash
net.recon on
```

Display discovered hosts:

```bash
net.show
```

Stop network reconnaissance:

```bash
net.recon off
```

Probe for hosts on the local network:

```bash
net.probe on
```

Stop host probing:

```bash
net.probe off
```

**What these commands do:**

- 🔍 `net.recon on` enables Bettercap's network-discovery module.
- 🖥️ `net.show` displays hosts and available information collected by Bettercap.
- 📡 `net.probe on` sends discovery probes to identify reachable local hosts.

Discovery results depend on the network, interface, permissions, and device configuration.

## 📡 6. Wi-Fi Interface Checks

Before conducting a wireless assessment, identify your wireless interface:

```bash
iw dev
```

Check wireless status:

```bash
iwconfig
```

Display interfaces and their addresses:

```bash
ip addr show
```

Check whether your wireless adapter supports monitor mode:

```bash
iw list
```

> ⚠️ Wireless capabilities depend on your adapter, driver, and operating system configuration. Do not assume every interface supports monitor mode.

## 📦 7. Traffic Analysis

Bettercap includes modules for examining network traffic and protocol activity.

Display available modules:

```bash
help
```

Inspect the available packet-sniffing commands:

```bash
help net.sniff
```

Check packet-sniffing configuration:

```bash
get net.sniff.*
```

## 🧰 8. Useful Linux Networking Commands

These commands are run in a separate Kali terminal, not inside Bettercap.

|Command|Purpose|
|---|---|
|`ip addr`|Show IP addresses|
|`ip route`|Show routes and the default gateway|
|`ip neigh`|Show the local neighbor table|
|`ping -c 4 192.168.1.1`|Test connectivity to a host|
|`ss -tuln`|Display listening TCP/UDP sockets|
|`sudo tcpdump -D`|List packet-capture interfaces|
|`sudo tcpdump -i eth0`|Inspect traffic on an authorized interface|
|`man tcpdump`|Read the packet-capture manual|

Replace example IP addresses and interface names with your own lab values.

## 🧪 9. A Simple Practice Workflow

1. 🖥️ Identify your interface with `ip link show`.
2. 🌐 Check your IP address with `ip addr`.
3. 🛣️ Check your default route with `ip route`.
4. 🚀 Start Bettercap using the correct interface.
5. 🔎 Enter `help` to review available modules.
6. 📡 Enable `net.recon on` in your authorized lab.
7. 📋 Enter `net.show` to inspect discovered hosts.
8. 🛑 Disable reconnaissance with `net.recon off`.
9. 🚪 Exit with `quit`.

---
