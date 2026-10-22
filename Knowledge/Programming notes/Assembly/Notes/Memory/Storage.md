# Storage

**Storage** is used to **save data permanently**. It keeps files even when the computer is **turned off**.

![[Pasted image 20260719112100.png|630]]
## HDD (Hard Disk Drive)

- Uses **magnetic storage** to save data.
    
- Has a **large capacity**.
    
- **Slower** than SSDs.
    

## SATA SSD (Solid State Drive)

- Stores data on **flash memory**.
    
- **Faster** than an HDD.
    
- Uses the **SATA interface**.
    

## NVMe SSD (Non-Volatile Memory Express)

- Also uses **flash memory**.
    
- Uses the **PCIe interface**.
    
- **Significantly faster** than a SATA SSD.
    
- Good for **gaming**, **video editing**, and **fast file transfers**.

![[Pasted image 20261022061603.png|516]]

---

# 💾 USB Flash Drive — How It Works

> [!abstract] 💡 The Big Picture A **USB flash drive** is a small, portable storage device that saves data using electronic memory. It keeps your files even when you unplug it.

## 🧩 1. Main Components

- 🔌 **USB connector:** Connects the drive to your computer.
- 🧠 **Controller:** The tiny processor that manages reading, writing, and organizing data.
- 💾 **NAND Flash Memory:** The chips that store your files.
- ⚡ **Power:** Supplied by the USB port; no battery is normally needed.

## 💾 2. How Does It Store Data?

Flash memory stores information using tiny electronic structures called **memory cells**.

These cells retain electrical charge to represent information as bits: `0` and `1`.

- 📝 **Write:** The controller programs the memory cells to store data.
- 📖 **Read:** The controller detects the cells' stored states and reconstructs the data.
- 📴 **Power off:** The information remains stored without electricity.

This is called **non-volatile memory**.

![[Pasted image 20261022065308.png|395]]

## 🔄 3. How Does Saving a File Work?

Imagine copying a photo onto your USB drive 📸

1. 🖥️ **Computer:** Sends the photo's data through USB.
2. 🧠 **Controller:** Receives the data and decides where to store it.
3. 💾 **Flash memory:** Stores the data in memory cells.
4. 📋 **File system:** Keeps track of the file's name, location, and size.
5. ✅ **Finished:** Your photo is stored and can be opened later.

When you plug the drive into another computer, it can read the stored data and reconstruct your photo.

![[Pasted image 20261022065433.png|471]]

## 📚 4. Important Terms

|Term|Simple meaning|
|---|---|
|💾 **NAND Flash**|Memory technology that stores your data|
|🧠 **Controller**|Manages the memory and data transfers|
|🗂️ **File system**|Organizes files and folders (e.g., FAT32, exFAT, NTFS)|
|📦 **Capacity**|How much data the drive can store|
|🚀 **Read speed**|How quickly data can be retrieved|
|✍️ **Write speed**|How quickly data can be saved|
|🔌 **USB standard**|Defines the connection and potential transfer speed|
|🔋 **Non-volatile**|Keeps data without continuous power|

## ⚠️ 5. Why Can a Flash Drive Wear Out?

Flash memory cells can only tolerate a limited number of erase-and-write cycles.

- 🔄 Repeated writing and erasing gradually wears out the memory.
- 🧹 The controller spreads writes across memory cells to help extend their lifespan. This is called **wear leveling**.
- 🛡️ Quality drives may include error correction to help protect data.

**Tip:** Always eject the drive safely when possible, especially while files are being copied. Unplugging it during a write can corrupt files or the file system.

## 🆚 6. Flash Drive vs. RAM vs. HDD

|Feature|USB Flash Drive|RAM|HDD|
|---|---|---|---|
|Stores data without power?|✅ Yes|❌ No|✅ Yes|
|Main technology|NAND flash|DRAM|Magnetic disks|
|Typical purpose|Portable storage|Temporary working memory|Long-term storage|
|Speed|Moderate to fast|Very fast|Generally slower|

---

## 🧷 Quick Summary

- 💾 A flash drive stores data electronically in NAND flash memory.
- ⚡ It keeps data without power.
- 🧠 A controller manages reading, writing, and memory health.
- 🗂️ A file system organizes files and folders.
- 🔄 Flash cells wear out over time, but wear leveling helps extend their life.

> [!quote] 💡 Final takeaway A USB flash drive converts your files into digital data, stores that data in electronic memory cells, and retrieves it whenever you need it — even after being unplugged.

---