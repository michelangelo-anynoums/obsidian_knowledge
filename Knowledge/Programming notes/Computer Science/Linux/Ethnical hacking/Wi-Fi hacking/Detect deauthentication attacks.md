# 📡 Wi-Fi Deauthentication Packets in Wireshark

> [!abstract] Overview  
> **Deauthentication (Deauth)** frames are IEEE 802.11 management frames used to terminate an authenticated Wi-Fi connection.
> 
> In Wireshark, they can be identified using their **802.11 frame subtype**.

---

## 🔎 Detection

### Deauthentication

Use this **display filter**:

```text
wlan.fc.type == 0 && wlan.fc.subtype == 12
```

Or the more concise subtype filter:

```text
wlan.fc.type_subtype == 0x0c
```

### Disassociation

Disassociation is related to deauthentication but uses a different frame subtype:

```text
wlan.fc.type_subtype == 0x0a
```

|Frame|Type|Subtype|Filter|
|---|---|---|---|
|📕 Deauthentication|0|12|`wlan.fc.type_subtype == 0x0c`|
|📙 Disassociation|0|10|`wlan.fc.type_subtype == 0x0a`|

---

## 🖥️ Capture Requirements

> [!important]  
> To see 802.11 management frames, your wireless adapter generally needs to be operating in **monitor mode**.

A normal Wi-Fi capture from an interface connected to your network may not expose all 802.11 management traffic.

For useful results:

- Enable **monitor mode**
    
- Capture on the relevant **Wi-Fi channel**
    
- Capture long enough to establish normal network behavior
    
- Preferably capture in an environment/network you are authorized to monitor
    

---

## 🧩 Inspecting a Deauth Frame

Select a matching packet and expand:

```text
IEEE 802.11
└── IEEE 802.11 Management
    └── Fixed parameters
```

Pay particular attention to:

|Field|What it tells you|
|---|---|
|**Source**|Device transmitting the frame|
|**Destination**|Device receiving the frame|
|**BSSID**|Access point/network associated with the frame|
|**Reason code**|Reason given for terminating authentication|

---

## 🎯 Filtering a Specific AP

If you know the BSSID of the access point:

```text
wlan.fc.type_subtype == 0x0c &&
wlan.bssid == aa:bb:cc:dd:ee:ff
```

Replace the example MAC address with the AP's actual BSSID.

> [!tip]  
> You can find the BSSID by inspecting normal beacon or data frames from the network.

---

## 🚨 Recognizing Suspicious Activity

> [!warning]  
> **One deauthentication frame does not automatically mean an attack.**

Deauthentication can occur legitimately—for example, when an AP disconnects a client or network conditions change.

More interesting indicators include:

- 🔴 Large numbers of deauth frames in a short period
    
- 🔴 Many different clients receiving deauth frames
    
- 🔴 Repeated deauth frames targeting the same client
    
- 🔴 Unexpected source addresses
    
- 🔴 Frames that appear inconsistent with the legitimate AP
    
- 🔴 A sudden burst of deauth/disassociation traffic accompanied by clients losing connectivity
    

### Useful investigation filter

```text
wlan.fc.type_subtype == 0x0c
```

Then sort or inspect packets chronologically and compare:

**Source → Destination → BSSID → Reason Code → Timestamp**

---

## 🧠 Deauth vs. Disassoc

```text
          802.11 Management
                 │
        ┌────────┴────────┐
        │                 │
   Disassociation    Deauthentication
     subtype 10          subtype 12
        │                 │
   Ends association   Ends authentication
```

They are related, but **not interchangeable**.

---

## 📝 Quick Reference

### Deauthentication

```text
wlan.fc.type_subtype == 0x0c
```

### Disassociation

```text
wlan.fc.type_subtype == 0x0a
```

### Deauth for a specific BSSID

```text
wlan.fc.type_subtype == 0x0c &&
wlan.bssid == aa:bb:cc:dd:ee:ff
```

### Key fields

```text
Source
Destination
BSSID
Reason Code
Timestamp
```

> [!quote] Remember  
> **A deauthentication frame is an event, not proof of an attack.**  
> Look for patterns, frequency, sources, destinations, and whether the observed behavior matches what the legitimate network should be doing.

---


# 📡 Wireshark — Specific Wi-Fi Channel

> [!abstract] Goal  
> To capture 802.11 management frames on a specific Wi-Fi channel, first put the wireless adapter into **monitor mode**, then tune it to the desired channel.

## 1. Find the adapter

```bash
iw dev
```

Example interface:

```text
wlan0
```

## 2. Enable monitor mode

Using `airmon-ng`:

```bash
sudo airmon-ng start wlan0
```

This may create:

```text
wlan0mon
```

Verify:

```bash
iw dev
```

## 3. Set the channel

For example, **channel 6**:

```bash
sudo iw dev wlan0mon set channel 6
```

Verify:

```bash
iw dev wlan0mon info
```

Expected:

```text
type monitor
channel 6 (2437 MHz)
```

## 4. Capture with Wireshark

Open Wireshark and select:

```text
wlan0mon
```

Start the capture.

Then filter for deauthentication frames:

```text
wlan.fc.type_subtype == 0x0c
```

## 🧠 Key Concept

> [!tip]  
> **The adapter determines the channel; Wireshark analyzes the packets.**

```text
Adapter
   ↓
Monitor Mode
   ↓
Channel 6
   ↓
Wireshark
   ↓
802.11 packets
```

### ⚠️ Important

A typical Wi-Fi adapter can listen to **one channel at a time**. Channel hopping can be used to observe multiple channels, but packets may be missed while switching.

Only capture wireless traffic on networks/channels you are authorized to monitor.

---
