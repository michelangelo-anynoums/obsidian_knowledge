# MAC Addresses + Ethernet + Switching

## **MAC Addresses**

- A **MAC address** is a **unique hardware address** for a network device.
    
- It is usually **48 bits (6 bytes)** long.
    
- It works at the **Data Link Layer (Layer 2)**.
    
- Example: `00:1A:2B:3C:4D:5E`
    

## **OUI (Organizationally Unique Identifier)**

- The **first 3 bytes** of a MAC address are called the **OUI**.
    
- The OUI shows the **manufacturer (vendor)** of the device.
    
- The **last 3 bytes** are chosen by the manufacturer to make each address unique.
    

## **Broadcast**

- A **broadcast** sends data to **every device** on the local network.
    
- Broadcast MAC address:
    
    - `FF:FF:FF:FF:FF:FF`
        
- All devices receive and process the message.
    

## **Multicast**

- A **multicast** sends data to a **specific group of devices**.
    
- Only devices in the group receive the message.
    
- It is more efficient than broadcasting to everyone.
    

## **Ethernet Frames**

- An **Ethernet frame** is the **data format** used in Ethernet networks.
    
- It contains:
    
    - **Destination MAC address**
        
    - **Source MAC address**
        
    - **Type/Length**
        
    - **Data (payload)**
        
    - **FCS (Frame Check Sequence)** for **error detection**
        

## **Switches**

- A **switch** connects devices in a **local area network (LAN)**.
    
- It learns **MAC addresses** and stores them in a **MAC address table**.
    
- It sends a frame **only to the correct device**, reducing unnecessary network traffic.
    
- Switches work at the **Data Link Layer (Layer 2)**.

---
