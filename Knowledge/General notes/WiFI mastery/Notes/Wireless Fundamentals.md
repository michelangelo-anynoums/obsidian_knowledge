
![[Pasted image 20260721130032.png|697]]

# Wireless Fundamentals — Day 8: RF Fundamentals

## Radio Waves

**Radio waves** are a type of **electromagnetic wave** used to send information wirelessly.

- They can travel through **air and space**.
    
- They are used in **Wi-Fi, Bluetooth, mobile networks, and radio communication**.
    

**Wavelength Formula:** λ = fc​ ( λ = wavelength, c = speed of light, f = frequency) 

**Antenna Length:** For maximum efficiency (resonance), the antenna length ( L ) is typically a fraction of the wavelength:

- **Half-wave dipole:** $$L ≈  λ/2​$$
    
- **Quarter-wave monopole:** $$L ≈ λ/4​$$
    

Higher frequencies result in shorter wavelengths and thus shorter antennas.

![[Pasted image 20260720135916.png|601]]

## Frequency

**Frequency** is the number of times a wave repeats in one second.

- It is measured in **Hertz (Hz)**.
    
- A **higher frequency** means the wave repeats faster.
    
- Example: Wi-Fi uses frequencies like **2.4 GHz** and **5 GHz**.

![[Pasted image 20260720140249.png|472]]

## Wavelength

**Wavelength** is the distance between two points of the same wave (for example, from one peak to the next peak).

- It is usually measured in **meters (m)**.
    
- **Higher frequency = shorter wavelength**.
    
- **Lower frequency = longer wavelength**.
    

![[Pasted image 20260720140341.png|377]]
## RF Spectrum

The **RF (Radio Frequency) spectrum** is the range of frequencies used for wireless communication.

**AC** (Alternating Current) periodically **reverses direction**, powering homes and grids. 

**DC** (Direct Current) flows **one way only**, powering batteries and electronics.

- It includes different frequency bands for different technologies.
    
- Examples:
    
    - **AM/FM radio**
        
    - **TV signals**
        
    - **Wi-Fi**
        
    - **Cellular networks**
        



**Key idea:**  
**Frequency** tells how fast a wave repeats, while **wavelength** tells its physical size.

---

## Antennas

![[Pasted image 20260721130807.png|361]]

An **antenna** is a simple metal device that sends and receives radio waves.  Think of it as a bridge that changes electricity from a wire into invisible waves that travel through the air (like Wi-Fi or radio signals), and changes those waves back into electricity so your device can use them. Without antennas, phones, radios, and TVs could not work wirelessly.

**For reference:** https://youtu.be/ZaXm6wau-jc

![[Pasted image 20260721125548.png]]

![[Pasted image 20260721125927.png|570]]

![[Pasted image 20260721125954.png|513]]

# Types of Antennas

An **antenna** is a device used to **send or receive radio signals**. Different antennas have different shapes and are designed for different purposes.

### 1. Dipole Antenna

![[Pasted image 20260721125954.png|325]]

A **dipole antenna** is one of the simplest and most common antennas. It usually has **two metal rods or wires** arranged in a straight line, with the signal connected between them.

- **Shape:** Two equal-length arms.
- **Use:** Radio communication, TV, and many other wireless systems.
- **Example:** The simple “rabbit-ear” antenna used with some TVs is similar to a dipole.

**Easy idea:** Think of it as two metal arms working together to send or receive a signal.

### 2. Monopole Antenna

![[Pasted image 20260721125927.png|437]]

A **monopole antenna** is similar to half of a dipole. It normally has **one metal rod** placed above a conducting surface called a **ground plane**.

- **Shape:** One vertical rod.
- **Use:** Cars, radios, mobile communication, and Wi-Fi equipment.
- **Example:** The short antenna on a car radio is a common example.

**Easy idea:** A monopole is like a dipole that has been cut in half, with the ground plane acting as the other half.

### 3. Loop Antenna

![[Pasted image 20260913061116.png|370]]

A **loop antenna** is made from a wire or metal conductor formed into a **closed loop**, such as a circle or rectangle.

- **Shape:** Circular, square, or rectangular loop.
- **Use:** AM radio receivers, RFID systems, and direction-finding equipment.
- **Example:** Some small portable AM radios use a loop antenna inside the radio.

**Easy idea:** Instead of straight wires, the conductor is bent around to make a loop.

### 4. Yagi-Uda Antenna

![[Pasted image 20260721130807.png|361]]

A **Yagi-Uda antenna**, often simply called a **Yagi antenna**, has several metal elements arranged along a boom. It is designed to send or receive signals mainly in **one direction**.

- **Shape:** Several metal rods mounted along a long support.
- **Use:** Television reception, amateur radio, and some communication systems.
- **Example:** The antenna commonly seen on rooftops for receiving TV signals is often a Yagi-type antenna.

**Easy idea:** It works like a “spotlight” for radio signals, concentrating its strongest reception or transmission in one direction.

### 5. Parabolic / Dish Antenna

![[Pasted image 20260913061353.png|370]]

A **dish antenna** uses a curved, bowl-shaped reflector to **focus radio waves** toward a small antenna called the **feed**.

- **Shape:** Looks like a large bowl or satellite dish.
- **Main feature:** Highly **directional** — it sends or receives signals mainly in one direction.
- **Use:** Satellite TV, satellite communication, radar, radio astronomy, and long-distance wireless links.
- **Example:** The dish on a house used to receive **satellite TV**.

**Easy idea:** Imagine using a **magnifying glass**, but instead of focusing light, the dish focuses radio waves.
### Quick Comparison

| Type               | Basic shape               | Main feature                  | Example            |
| ------------------ | ------------------------- | ----------------------------- | ------------------ |
| **Dipole**         | Two straight arms         | Simple and widely used        | TV/radio antenna   |
| **Monopole**       | One straight rod + ground | Compact and simple            | Car radio antenna  |
| **Loop**           | Closed loop               | Compact; useful for receiving | AM radio           |
| **Yagi-Uda**       | Several rods on a boom    | Strongly directional          | Rooftop TV antenna |
| **Parabolic/Dish** | Curved reflector          | Very directional              | TV antenna         |

**In short:** Dipole and monopole antennas are among the simplest types, a loop antenna uses a closed conductor, and a Yagi-Uda antenna uses several elements to focus radio signals in a particular direction.

---

## Heinrich Hertz

![[Pasted image 20260720140647.png|200]]

https://youtu.be/FWCN_uI5ygY
https://youtu.be/9gDFll6Ge7g


**Heinrich Hertz** was a German physicist who proved that **radio waves exist**.

- In the 1880s, he created and detected **electromagnetic waves** in experiments.
    
- His work confirmed the ideas of **James Clerk Maxwell** about electromagnetic radiation.
    
- The unit of frequency, **Hertz (Hz)**, was named in his honor.
    

**1 Hertz (Hz) = 1 cycle per second**

![[300px-Electromagnetic_induction_-_solenoid_to_loop_-_animation 1.gif|406]]

![[Pasted image 20260720141739.png|378]]

**Key idea:**  
**Hertz showed that invisible radio waves can travel through space and carry energy.**

---

## James Clerk Maxwell (1831–1879) 

**James Clerk Maxwell** was a Scottish physicist who unified electricity, magnetism, and light into a single framework known as **electromagnetism**.  His most significant achievement was formulating **Maxwell's Equations**, a set of four laws describing how electric and magnetic fields interact and propagate as waves.

![[Pasted image 20260721130336.png|321]]



---
