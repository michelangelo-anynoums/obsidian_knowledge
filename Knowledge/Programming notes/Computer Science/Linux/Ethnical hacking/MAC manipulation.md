# 🕵️ MAC Address Manipulation

> [!abstract] Overview A **MAC (Media Access Control) address** is a Layer 2 identifier assigned to a network interface. On Linux, you can temporarily change the address for network testing, privacy, and lab exercises.

## 🔍 1. Identify Network Interfaces

List interfaces and their current MAC addresses:

```bash
ip link show
```

Check a specific interface:

```bash
ip link show eth0
```

Display MAC addresses in a concise format:

```bash
ip -br link
```

> [!tip] Interface names Common names include `eth0`, `wlan0`, `enp0s3`, and `wlp2s0`. Replace these examples with the actual interface name on your system.

## 🛠️ 2. Change the MAC Address

Install the utility if needed:

```bash
sudo apt update
sudo apt install macchanger
```

Check available options:

```bash
macchanger --help
```

### Option A — Generate a random MAC

```bash
sudo ip link set dev eth0 down
sudo macchanger -r eth0
sudo ip link set dev eth0 up
```

### Option B — Set a specific MAC

```bash
sudo ip link set dev eth0 down
sudo macchanger -m 02:11:22:33:44:55 eth0
sudo ip link set dev eth0 up
```

The example address uses the locally administered bit, making it suitable for a controlled test configuration.

### Option C — Use `ip` directly

```bash
sudo ip link set dev eth0 down
sudo ip link set dev eth0 address 02:11:22:33:44:55
sudo ip link set dev eth0 up
```

## ✅ 3. Verify the Change

```bash
ip link show eth0
macchanger -s eth0
```

Compare the reported MAC address with the value you intended to set.

## ↩️ 4. Restore the Original MAC

If the original address was recorded before the change:

```bash
sudo ip link set dev eth0 down
sudo macchanger -p eth0
sudo ip link set dev eth0 up
```

`macchanger -p` attempts to restore the hardware MAC address. The result depends on the interface and driver.

> [!warning] Important
> 
> - MAC changes are generally temporary and may be lost after a reboot or network reconnection.
> - NetworkManager, Wi-Fi drivers, or access-point policies may interfere with changes.
> - Changing a MAC can interrupt your network connection.
> - Use these techniques only on devices and networks you own or are authorized to test.
> - MAC spoofing changes the address presented at Layer 2; it does **not** make you anonymous or conceal your activity by itself.

## 🧠 Quick Reference

|Task|Command|
|---|---|
|List interfaces|`ip -br link`|
|Show MAC address|`ip link show eth0`|
|Randomize MAC|`sudo macchanger -r eth0`|
|Set custom MAC|`sudo macchanger -m 02:11:22:33:44:55 eth0`|
|Check current MAC|`macchanger -s eth0`|
|Restore hardware MAC|`sudo macchanger -p eth0`|

---

## 🔗 Related Notes

![[Pasted image 20261019062116.png|171]]

> [!link] Further Reading
> 
>  [[Python Scapy — Packet Manipulation]]. Explore programmatic packet crafting, inspection, and Layer 2 operations with Python's Scapy library.