# 🔐 WireGuard — Setup & Usage

> A fast, modern VPN that creates a secure tunnel between devices using public/private keys.

## 🧠 1. How it works

- **Server** → Accepts VPN connections.
- **Client** → Connects to the server.
- **PrivateKey** → Secret key. Never share it.
- **PublicKey** → Shared with peers.
- **Endpoint** → Server IP + port.
- **AllowedIPs** → IP ranges routed through the tunnel.

```text
Client ───── Encrypted Tunnel ───── Server
10.0.0.2                         10.0.0.1
```

## 📦 2. Install WireGuard

**Debian / Ubuntu**

```bash
sudo apt update
sudo apt install wireguard -y
```

**Fedora**

```bash
sudo dnf install wireguard-tools
```

**Arch Linux**

```bash
sudo pacman -S wireguard-tools
```

## 🔑 3. Generate keys

Run on both server and client:

```bash
umask 077

wg genkey | tee privatekey | wg pubkey > publickey
```

View keys:

```bash
cat privatekey
cat publickey
```

⚠️ Keep `privatekey` secret!

## 🖥️ 4. Configure the server

Create the configuration:

```bash
sudo nano /etc/wireguard/wg0.conf
```

**Server example:**

```ini
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = SERVER_PRIVATE_KEY

[Peer]
PublicKey = CLIENT_PUBLIC_KEY
AllowedIPs = 10.0.0.2/32
```

## 💻 5. Configure the client

Create `wg0.conf`:

```ini
[Interface]
Address = 10.0.0.2/24
PrivateKey = CLIENT_PRIVATE_KEY

[Peer]
PublicKey = SERVER_PUBLIC_KEY
Endpoint = SERVER_PUBLIC_IP:51820
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

💡 `AllowedIPs` determines which traffic uses the VPN.

- `10.0.0.0/24` → Only VPN subnet.
- `0.0.0.0/0` → All IPv4 traffic.
- `::/0` → All IPv6 traffic.

## 🚀 6. Start WireGuard

**Start the interface:**

```bash
sudo wg-quick up wg0
```

**Stop the interface:**

```bash
sudo wg-quick down wg0
```

**Enable at boot:**

```bash
sudo systemctl enable wg-quick@wg0
```

**Check status:**

```bash
sudo wg show
```

## 🌐 7. Server networking

For remote clients to access the internet through the VPN, the server also needs:

1. IP forwarding enabled.
2. Firewall rules allowing VPN traffic.
3. NAT / masquerading configured.
4. UDP port `51820` accessible from the internet.

Enable IPv4 forwarding:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

For persistence, add to `/etc/sysctl.conf`:

```ini
net.ipv4.ip_forward=1
```

⚠️ Configure NAT and firewall rules according to your server's network interface and firewall system.

## 🔍 8. Useful commands

|Command|Description|
|---|---|
|`wg show`|Show VPN status|
|`wg showconf wg0`|Display configuration|
|`wg show wg0 latest-handshakes`|Show last handshakes|
|`wg show wg0 transfer`|Show traffic statistics|
|`ip addr show wg0`|Show interface IP|
|`ip route`|Show routing table|
|`sudo wg-quick up wg0`|Connect|
|`sudo wg-quick down wg0`|Disconnect|

---
