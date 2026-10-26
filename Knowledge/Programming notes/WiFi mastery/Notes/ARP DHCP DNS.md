# ARP + DHCP + DNS

## ARP (Address Resolution Protocol)

- **ARP** finds the **MAC address** of a device using its **IP address**.
    
- It works only inside the **local network (LAN)**.
    
- The sender sends an **ARP Request** ("Who has this IP?").
    
- The correct device sends an **ARP Reply** with its **MAC address**.
    

---

## DHCP Process (Dynamic Host Configuration Protocol)

**DHCP** automatically gives network settings to a device.

### Steps (DORA)

1. **Discover** – The device asks for an IP address.
    
2. **Offer** – The DHCP server offers an IP address.
    
3. **Request** – The device asks to use the offered address.
    
4. **Acknowledge (ACK)** – The server confirms the address.
    

The device also receives:

- **IP address**
    
- **Subnet mask**
    
- **Default gateway**
    
- **DNS server**
    

---

## DNS Resolution (Domain Name System)

- **DNS** changes a **domain name** into an **IP address**.
    
- Example: **google.com → 142.x.x.x**
    
- The device asks a **DNS server** for the IP address.
    
- The DNS server returns the correct IP.
    
- The device then connects to the website using that **IP address**.