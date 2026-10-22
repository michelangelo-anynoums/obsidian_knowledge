# 🖥️ Computer Hardware Roadmap

> [!abstract] Learning Goal Understand the main computer components, peripherals, cooling systems, and maintenance procedures well enough to explain how they work without relying on notes.

---

## 🧭 Learning Path

- [[#01 — Peripherals & Displays|01 · Peripherals & Displays]]
- [[#02 — Internal Components|02 · Internal Components]]
- [[#03 — Cooling & Thermal Management|03 · Cooling & Thermal Management]]
- [[#04 — Ports, Cables & Connectivity|04 ·  Ports, Cables & Connectivity]]

---

# 01 — Peripherals & Displays

> [!abstract] Objective Understand the most common computer input and output devices, their technologies, and their differences.

## ⌨️ Keyboards [[Keyboards]]

### Membrane Keyboards

- Use rubber-dome or membrane-based mechanisms.
- Quiet and affordable.
- Common in laptops and office keyboards.

### Mechanical Keyboards

- Use individual mechanical switches.
- Generally offer longer switch lifespans and easier switch replacement on compatible models.

**Switch types**

|Type|Characteristics|Example|
|---|---|---|
|Linear|Smooth keystroke, no tactile bump|Cherry MX Red|
|Tactile|Noticeable bump, no distinct click required|Cherry MX Brown|
|Clicky|Tactile feedback with an audible click|Cherry MX Blue|

### Other Keyboard Technologies

- **Optical:** Detect keystrokes using light-based actuation.
- **Low-profile:** Use shorter switches and reduced key travel.
- **Ergonomic:** Use split, curved, or angled layouts to improve typing posture.

### References

- [Keyboard Explained — YouTube](https://www.youtube.com/watch?v=6HqO1ltAat4)
- [Keyboard Guide — YouTube](https://youtu.be/Qx-8JdRgAK4)

---

## 🖱️ Mouse Types [[Mouse Types]]

### Sensor Technologies

- **Mechanical:** Uses a physical tracking ball; largely obsolete.
- **Optical:** Uses an LED or other light source and an optical sensor.
- **Laser:** Uses a laser-based optical sensor and may track on a wider range of surfaces, depending on the sensor.

### Connection Types

- **Wired:** Typically connects through USB; requires no mouse battery.
- **Wireless:** Connects through Bluetooth or a USB receiver; may require batteries or charging.

### Specialized Mice

- **Gaming:** High-performance sensors, adjustable DPI, and additional buttons.
- **Vertical:** Designed to reduce forearm pronation.
- **Trackball:** Remains stationary while the user rotates a ball with their fingers or thumb.

### References

- [Types of Computer Mice — YouTube](https://www.youtube.com/watch?v=eoUgDF5QtP0)

---

## 🖥️ Display Technologies [[Display Types]]

### LCD-Based Displays

LCD panels use liquid crystals to control how light passes through the display.

- **LED:** An LCD display that uses LED backlighting.
- **IPS:** Wide viewing angles and generally good color reproduction.
- **TN:** Often offers fast response times, with more limited viewing angles.
- **VA:** Generally provides high contrast and deep blacks.

### Self-Emissive Displays

- **OLED:** Individual pixels produce their own light, enabling excellent contrast and true blacks.

### Advanced Backlighting

- **Mini-LED:** Uses many small LEDs for more precise LCD backlighting and improved local dimming and HDR performance.

> [!note] Important Distinction IPS, TN, and VA describe LCD panel technologies. LED describes a backlighting method, while OLED uses self-emissive pixels.

### References

- [Types of Computer Screens Explained — YouTube](https://www.youtube.com/watch?v=EMg87BB4BoU)

---

# 02 — Internal Components

> [!abstract] Objective Understand the major hardware components inside a computer and how they work together.

## ⚙️ CPU — Central Processing Unit [[CPU term]]

The CPU executes instructions and performs general-purpose computations.

### Key Concepts

- **Cores:** Independent processing units within the CPU.
- **Threads:** Execution sequences handled by the processor.
- **Clock speed:** The rate at which the CPU operates, usually measured in GHz.
- **Cache:** Small, fast memory used to store frequently needed data.
- **Integrated graphics:** Graphics processing built into the CPU or processor package.

### Examples

- Intel Core processors
- AMD Ryzen processors

### References

- Official documentation and learning resources: [Intel](https://www.intel.com/) · [AMD](https://www.amd.com/)

---

## 🧩 Motherboard [[Motherboard]]

The motherboard connects the computer's components and allows them to communicate.

### Key Components

- **CPU socket:** Holds the compatible processor.
- **Chipset:** Provides platform connectivity and manages selected I/O functions.
- **RAM slots:** Hold memory modules.
- **Storage connectors:** Connect SATA drives and supported M.2 devices.
- **Expansion slots:** Commonly used for graphics cards and other PCIe devices.

### References

- [Intel — PC Components and Hardware](https://www.intel.com/)
- [ASUS Support](https://www.asus.com/support/)

---

## 🧠 RAM — Random Access Memory [[RAM]]

RAM temporarily stores data and instructions that the system is actively using.

### DDR Generations

- **DDR3:** Older memory generation.
- **DDR4:** Widely used in many desktop and laptop systems.
- **DDR5:** Newer generation with increased bandwidth and other architectural improvements.

### Form Factors

- **DIMM:** Commonly used in desktop computers.
- **SO-DIMM:** Commonly used in laptops and compact systems.

### Key Characteristics

- **Capacity:** How much data memory can hold.
- **Frequency / data rate:** Indicates memory transfer speed.
- **Latency:** Describes delays in accessing data.

> [!tip] Compatibility Check Memory must be compatible with the motherboard and CPU. DDR generations are not interchangeable between their respective slots.

### References

- [Crucial — Memory and SSD Resources](https://www.crucial.com/)

---

## 💾 Storage [[Storage]]

Storage retains files, applications, and the operating system when the computer is powered off.

### HDD — Hard Disk Drive

- Uses magnetic platters and moving mechanical parts.
- Offers high capacity at a relatively low cost.
- Generally slower than SSDs.

### SATA SSD

- Uses flash memory with no moving parts.
- Connects through the SATA interface.
- Provides faster access and responsiveness than an HDD.

### NVMe SSD

- Uses the NVMe protocol, typically over PCIe.
- Offers high bandwidth and low latency.
- Performance depends on the drive, PCIe generation, and system configuration.

### References

- [Crucial — SSD and Storage Guides](https://www.crucial.com/)

---

## 🎮 GPU — Graphics Processing Unit [[GPU & memory]]

The GPU processes graphics and performs parallel computations.

### Integrated Graphics

- Built into the processor or processor package.
- Shares system memory in many implementations.
- Suitable for everyday tasks and some gaming workloads.

### Dedicated Graphics Card

- A separate graphics processor, typically installed in a PCIe slot.
- Usually has its own video memory (VRAM).
- Provides greater graphics performance for demanding workloads.

### References

- [NVIDIA](https://www.nvidia.com/)
- [AMD Radeon](https://www.amd.com/en/products/graphics)

---

# 03 — Cooling & Thermal Management

> [!abstract] Objective Understand how computers manage heat, how cooling components work, and why thermal maintenance matters.

## 🌡️ Cooling Systems [[Cooling Systems]]

### Passive Cooling

- Uses heat sinks and natural convection.
- Has no fan or other powered airflow mechanism.
- Operates silently but depends on suitable thermal design and airflow.

### Active Cooling

- Uses fans or other powered mechanisms to move heat away.
- Commonly combines heat sinks, fans, and thermal interfaces.

---

## 🧊 Heat Sinks

Heat sinks transfer heat away from components and release it into the surrounding air.

### Key Concepts

- **Aluminum:** Lightweight and widely used.
- **Copper:** Offers higher thermal conductivity than aluminum.
- **Heat pipes:** Move heat from a hot area to a cooler area through phase-change heat transfer.

---

## 🌀 Cooling Fans

### Axial Fans

- Move air approximately parallel to the fan's rotational axis.
- Common in desktop cases, CPU coolers, and radiators.

![[Pasted image 20260724140653.png|339]]

### Blower Fans

- Draw air in and redirect it outward, typically at an angle to the intake.
- Common in compact devices and some laptop cooling systems.

![[Pasted image 20260724140619.png|427]]

---

## 🧴 Thermal Paste [[Thermal Paste theory]]

Thermal paste fills microscopic gaps between a processor and its cooler to improve heat transfer.

### Key Concepts

- Purpose and thermal conductivity.
- Correct application and cooler contact.
- Product lifespan and manufacturer recommendations.
- Signs that inspection or replacement may be necessary.

> [!warning] Maintenance Note Thermal paste does not always need to be replaced on a fixed schedule. Follow the manufacturer's guidance and investigate actual thermal symptoms before disassembling a cooler.

---

## 🌫️ Dust Accumulation [[Dust Accumulation]]

Dust restricts airflow and can reduce the effectiveness of cooling systems.

### Common Effects

- Higher operating temperatures.
- Increased fan noise.
- Thermal throttling and reduced performance.
- Greater cooling-system strain.

### References

- [iFixit — Repair Guides](https://www.ifixit.com/)
- [Intel — Support and Troubleshooting](https://www.intel.com/content/www/us/en/support.html)

---

---

# 04 — Ports, Cables & Connectivity

> [!abstract] Objective Identify the major computer ports, cables, and connectors, understand their purposes, and know where they are commonly used.

## 🔌 USB & Data Cables

> [!Important] USB is a *Universal Serial Bus*

- **USB-A:** Common connector for keyboards, mice, flash drives, and other peripherals.
- **USB-B:** Often used by printers and older peripherals.
- **USB-C:** Reversible connector supporting data, charging, and video on compatible devices.
- **Micro-USB:** Common on older phones, accessories, and small electronics.
- **Mini-USB:** Found on older cameras and portable devices.
- **USB 3.x Micro-B:** Wide connector used by some external hard drives.
- **Thunderbolt 3 / 4 / 5:** High-speed connectivity using USB-C connectors.
- **USB Extension Cable:** Extends the reach of a USB connection.

![[Pasted image 20261022062646.png|325]]

## 🖥️ Display & Video Cables

- **HDMI:** Digital video and audio for monitors, TVs, and projectors.
- **DisplayPort:** Digital video and audio, commonly used with PC monitors.
- **Mini DisplayPort:** Smaller DisplayPort connector found on some older computers.
- **VGA:** Analog video connector used by older displays and projectors.
- **DVI:** Digital video, with some variants also supporting analog signals.
- **USB-C Display Cable:** Transmits video using supported DisplayPort Alternate Mode or Thunderbolt functionality.
- **SDI:** Professional digital video connection used in broadcast equipment.

![[Pasted image 20261022062903.png|446]]
## 🌐 Network & Internet Cables

- **Ethernet (RJ45):** Wired network connection for computers, routers, and switches.
- **Cat5e:** Supports Gigabit Ethernet.
- **Cat6:** Supports Gigabit Ethernet and higher speeds over suitable distances.
- **Cat6a:** Supports 10 Gigabit Ethernet up to 100 metres under specified conditions.
- **Cat7 / Cat8:** Shielded cabling categories used in particular high-frequency networking applications.
- **Fiber Optic:** Transmits data using light; common in high-speed networks and internet infrastructure.
- **Coaxial:** Used for cable internet, antennas, and some networking equipment.

![[Pasted image 20261022063226.png|350]]

## 🎧 Audio Cables

- **3.5 mm Audio Jack (TRS / TRRS):** Headphones, speakers, and headsets.
- **6.35 mm (¼-inch) Jack:** Instruments and professional audio equipment.
- **RCA:** Analog audio and video connections.
- **Optical S/PDIF (TOSLINK):** Digital audio transmission using light.
- **USB Audio Cable:** Connects USB microphones, headsets, and audio interfaces.
- **XLR:** Balanced audio connection for microphones and professional equipment.

![[Pasted image 20261022063346.png|605]]
## 💾 Internal Storage & Drive Cables

- **SATA Data Cable:** Connects SATA HDDs and SSDs to the motherboard.
- **SATA Power Cable:** Supplies power to SATA drives from the power supply.
- **IDE / PATA Ribbon Cable:** Legacy connection for older hard drives and optical drives.
- **SAS Cable:** Connects enterprise storage devices and controllers.
- **External SATA (eSATA):** Legacy external storage interface.
- **USB-to-SATA Cable:** Connects SATA drives externally through USB.



> [!note] Important Distinction M.2 and NVMe are not cable types. M.2 is a physical form factor, while NVMe is a storage protocol commonly used over PCIe. These drives usually connect directly to the motherboard.

## ⚡ Power Supply & Internal Power Cables

- **ATX 24-pin:** Main motherboard power connector.
- **EPS 4-pin / 8-pin:** Supplies power to the CPU.
- **PCIe 6-pin / 8-pin:** Powers compatible graphics cards.
- **12V-2x6:** Modern high-power graphics card connector.
- **SATA Power:** Powers SATA drives and compatible accessories.
- **4-pin Molex:** Legacy power connector for older drives, fans, and accessories.
- **Floppy Berg Connector:** Small legacy power connector.
- **AC Power Cable:** Connects a desktop PSU or external adapter to mains power.
- **DC Barrel Connector:** Supplies power from an external adapter to compatible devices.
- **USB-C Power Delivery Cable:** Carries power between compatible chargers and devices.

## 🌀 Cooling & Fan Cables

- **3-pin Fan Connector:** Supplies power and typically supports speed monitoring.
- **4-pin PWM Fan Connector:** Allows compatible motherboards to control fan speed using PWM.
- **CPU Fan / CPU OPT:** Fan headers intended for CPU cooling systems.
- **AIO Pump Connector:** Powers or monitors compatible liquid-cooling pumps.
- **ARGB 3-pin (5 V):** Controls individually addressable lighting.
- **RGB 4-pin (12 V):** Controls conventional RGB lighting.

> [!warning] Compatibility Never connect a 5 V ARGB device to a 12 V RGB header. Check the voltage, pin layout, and manufacturer's instructions before connecting components.

## 🔄 Adapters & Specialized Cables

- **USB-to-Ethernet:** Adds wired networking through USB.
- **USB-to-HDMI:** Provides display output through compatible adapters.
- **DisplayPort-to-HDMI:** Connects compatible DisplayPort outputs to HDMI displays.
- **USB-to-Serial (RS-232):** Connects legacy equipment and diagnostic devices.
- **KVM Cables:** Carry connections between computers and a keyboard, video, and mouse switch.
- **Riser / PCIe Extension Cable:** Connects a PCIe device remotely, commonly used in custom PC builds.
- **Internal USB Header Cable:** Connects front-panel USB ports or internal USB devices to the motherboard.

## 📚 References

- [USB Implementers Forum — USB Standards](https://www.usb.org/)
- [HDMI — Official Specifications](https://www.hdmi.org/)
- [VESA — DisplayPort](https://www.displayport.org/)
- [Intel — Thunderbolt Technology](https://www.intel.com/content/www/us/en/architecture-and-technology/thunderbolt/overview.html)
- [Ethernet Alliance](https://ethernetalliance.org/)
- [Fluke Networks — Cabling Resources](https://www.flukenetworks.com/)
- [Serial ATA International Organization](https://sata-io.org/)
- [PCI-SIG — PCI Express Standards](https://pcisig.com/)

---
