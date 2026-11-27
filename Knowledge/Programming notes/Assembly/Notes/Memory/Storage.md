# 💾 Storage

**Storage** is used to **save data permanently**, allowing files and programs to remain available even when the computer is **turned off**.

> [!abstract] 📚 Storage Types — Explained! [Watch the video](https://www.youtube.com/watch?v=1vO9l1idWac)

![[Pasted image 20260719112100.png|630]]

---

## 🧲 1. HDD (Hard Disk Drive)

An **HDD** is a storage device that uses **magnetic technology** to store data on spinning disks (platters).

### ⚙️ Key Characteristics

- 🧲 **Magnetic storage:** Data is stored magnetically on spinning disks.
- 📦 **Large capacity:** Offers plenty of storage space, often at a lower cost per GB.
- 🐢 **Slower performance:** Has slower read and write speeds than SSDs.
- ⚙️ **Moving parts:** Uses mechanical components, including spinning platters and a moving read/write head.

### 🔍 How Does an HDD Store Data?

HDDs store information by changing the **magnetic orientation of tiny regions** on their platters.

- ✍️ **Writing data:** The read/write head changes the magnetic direction of tiny regions on the disk.
- 📖 **Reading data:** The head detects these magnetic orientations to retrieve stored information.
- 🔄 **Rewriting data:** Rewriting a sector changes its magnetic pattern rather than physically wearing away the disk's surface.

> [!important] ⚠️ Important: HDD Lifespan Repeated writing does not normally wear out an HDD's magnetic surface. Instead, HDD failures are more commonly associated with **mechanical components**, such as the motor, bearings, and read/write mechanism.

### 🎥 Video References

- [HDD Explained! — Video 1](https://www.youtube.com/watch?v=wtdnatmVdIg)
- [HDD Explained! — Video 2](https://www.youtube.com/watch?v=Hvbpa2qvGxw)

### 🖼️ Internal Components & Images

![[Pasted image 20261127115952.png|384]]

![[Pasted image 20261127120115.png|390]]

![[Pasted image 20261127120239.png|390]]

![[Pasted image 20261127120409.png]]

![[Pasted image 20261127120417.png]]

---

## ⚡ 2. SATA SSD (Solid State Drive)

A **SATA SSD** is a storage device that uses **NAND flash memory** to store data electronically, without any moving mechanical parts.

### ⚙️ Key Characteristics

- 💾 **Flash storage:** Stores data using NAND flash memory.
- 🚀 **Faster performance:** Offers significantly faster read and write speeds than an HDD.
- 🔌 **SATA interface:** Uses the SATA connection to communicate with the computer.
- 🔇 **No moving parts:** Operates silently and is more resistant to physical shock than an HDD.

### 🧬 Limited Write Cycles of NAND Flash Memory

SSDs store data by **trapping electrical charges (electrons) inside tiny memory cells**.

However, NAND flash memory has a limited number of write/erase cycles.

#### 🔬 Why Does NAND Flash Wear Out?

1. ⚡ **Electron movement:** Writing and erasing data moves electrons through a thin insulating layer.
2. 🧱 **Insulation degradation:** Repeated electrical operations gradually damage this insulating layer.
3. 📉 **Reduced reliability:** Over time, memory cells become less capable of retaining their electrical charge.
4. ⛔ **End of lifespan:** Eventually, cells can no longer reliably store data.

> [!warning] ⚠️ Important: SSD Lifespan NAND flash memory has a finite number of write/erase cycles. However, modern SSDs use techniques such as **wear leveling** to distribute writes across memory cells and extend the drive's lifespan.

### 🎥 Video References

- [USB Memory Explained!](https://youtu.be/r2KaVfSH884)
- [NAND Flash Memory Explained!](https://youtu.be/5Mh3o886qpg)
- [SSD Explained!](https://youtu.be/yoTPMQ7aL8o)

---

## 🚀 3. NVMe SSD (Non-Volatile Memory Express)

An **NVMe SSD** is a high-performance storage device that uses **NAND flash memory** and communicates through the **PCIe (Peripheral Component Interconnect Express) interface**.

### ⚙️ Key Characteristics

- 💾 **Flash storage:** Uses NAND flash memory, just like SATA SSDs.
- 🔌 **PCIe interface:** Communicates directly through the PCI Express bus.
- ⚡ **Extremely fast:** Offers significantly higher potential read and write speeds than SATA SSDs.
- 🎮 **Gaming:** Helps reduce loading times.
- 🎬 **Video editing:** Provides faster access to large video files.
- 📂 **File transfers:** Allows much faster transfers when the rest of the system supports the required speeds.

### 🔍 SATA SSD vs. NVMe SSD

The main difference is the **interface and communication protocol**:

- **SATA SSD:** Uses the SATA interface and AHCI protocol.
- **NVMe SSD:** Uses the PCIe interface and the NVMe protocol, which is designed specifically for flash storage.

> [!info] 💡 Remember **M.2** refers to a physical form factor, not necessarily NVMe. An M.2 SSD can use either SATA or PCIe/NVMe, depending on the model.

### 🎥 Video Reference

- [M.2 SSD Explained!](https://youtu.be/HvfIeTieXOI)

### 🖼️ Image

![[Pasted image 20261022061603.png|516]]

---

## 📊 4. Quick Comparison

|Feature|🧲 HDD|⚡ SATA SSD|🚀 NVMe SSD|
|---|---|---|---|
|Technology|Magnetic|NAND Flash|NAND Flash|
|Interface|SATA (typically)|SATA|PCIe|
|Moving parts|Yes|No|No|
|Speed|Slow|Fast|Very fast|
|Noise|Audible|Silent|Silent|
|Shock resistance|Lower|Higher|Higher|
|Write cycles|No NAND limit|Limited|Limited|
|Typical use|Mass storage|Everyday computing|High-performance computing|

> [!tip] 🧠 Key Takeaways
> 
> - 🧲 **HDD:** Magnetic storage, large capacity, mechanical moving parts.
> - ⚡ **SATA SSD:** Flash storage, faster than HDDs, uses SATA.
> - 🚀 **NVMe SSD:** Flash storage, uses PCIe, offers very high performance.
> 
> **Remember:** HDDs store data magnetically, whereas SSDs store data electronically using NAND flash memory.