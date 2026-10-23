
> [!important] **YouTube reference:** [file systems explained!](https://youtu.be/5AE7ARZGe2Y)


# 💾 PC File Systems — A Simple Guide

> [!abstract] Overview A **file system** is the method an operating system uses to organize, store, find, and manage files on a storage device, such as an HDD, SSD, or USB drive.

Think of a disk as a huge library 📚. The file system is the system that organizes the shelves, records where every book is stored, and helps you find it again.

![[Pasted image 20261023073320.png|613]]

---

## 🧱 1. What Is a File System?

A file system manages how data is stored and retrieved on a storage device.

It helps the computer:

- 📁 Organize files and folders.
- 🔎 Find stored information.
- 📏 Track file sizes and locations.
- 🔐 Manage permissions and access.
- 🗑️ Mark space as available when files are deleted.

### Common file systems

|File system|Main use|
|---|---|
|**NTFS**|Windows system drives and internal disks|
|**FAT32**|Older devices, USB drives, and broad compatibility|
|**exFAT**|USB drives and external storage, especially for large files|
|**ext4**|Common Linux file system|
|**APFS**|Modern Apple devices|
|**Btrfs**|Linux systems with features such as snapshots|

💡 **Remember:** A storage device is the physical hardware; a file system is the structure used to organize its data.

---

## 🧩 2. Bits, Bytes, Sectors, and Clusters

These concepts explain how data is stored at different levels.

### 🔹 Bit and byte

- **Bit:** The smallest unit of digital data, represented by `0` or `1`.
- **Byte:** A group of 8 bits.
- **Kilobyte (KB), megabyte (MB), gigabyte (GB):** Units used to measure data size.

![[Pasted image 20261023073507.png|431]]

### 🔹 Sector

A **sector** is a small addressable unit of storage on a disk.

- Traditional disk sectors commonly contain 512 bytes.
- Modern disks often use 4,096-byte physical sectors.
- The operating system and storage device work together to read and write data in addressable units.

![[Pasted image 20261023073201.png|453]]

### 🔹 Cluster

A **cluster** is a group of sectors that a file system allocates as a unit for storing file data. It is also called an _allocation unit_.

For example, imagine a file system with a cluster size of 4 KB:

- A 1 KB file occupies one 4 KB cluster.
- A 4 KB file occupies one cluster.
- A 6 KB file needs two clusters, occupying 8 KB in total.

The unused space in the last cluster is called **slack space**.

💡 **Why do clusters matter?**

- Smaller clusters can reduce wasted space when storing many small files.
- Larger clusters can reduce allocation overhead for large files.
- The best size depends on the file system and how the disk is used.

![[Pasted image 20261023073230.png|388]]

---

## 🗂️ 3. Partitions, Volumes, and Drives

These terms are related, but they do not mean exactly the same thing.

### 💿 Disk

A physical storage device, such as an HDD or SSD.

### 🧱 Partition

A defined region of a disk described by a partition table.

A disk might contain:

- A Windows system partition.
- A recovery partition.
- A data partition.

### 📦 Volume

A storage area that an operating system can use, usually with a file system.

A volume may occupy one partition, span multiple storage devices, or use a more complex storage arrangement.

### 🔤 Drive letter

In Windows, a volume can appear as a drive such as `C:`, `D:`, or `E:`.

Example:

`Physical SSD → Partition → NTFS volume → C: → Folders and files`

💡 A partition and a volume are often closely related, but they are not always identical.

---

## 🧭 4. MBR — Master Boot Record

**MBR** is an older partitioning scheme used to describe disk partitions and support traditional PC booting.

It is located in the first sector of an MBR-partitioned disk.

### Key characteristics

- 🕰️ An older and widely supported partitioning scheme.
- 📏 Typically supports disks up to about 2 TiB when using 512-byte logical sectors.
- 🧱 Supports up to four primary partition entries, or a combination involving an extended partition and logical partitions.
- 🖥️ Commonly associated with legacy BIOS booting.

### Limitations

MBR has limited partition-table space and uses 32-bit sector addressing, which restricts its practical capacity on conventional disks.

💡 **Remember:** MBR is both a disk-partitioning structure and, in traditional BIOS booting, a location for initial boot code.

---

## 🧭 5. GPT — GUID Partition Table

**GPT** is the modern partitioning scheme commonly used on Windows PCs with UEFI firmware.

GPT stands for **GUID Partition Table**.

### Key characteristics

- 🚀 Supports very large disks.
- 🧩 Supports many partitions; Windows commonly allows up to 128 GPT partitions on a basic disk.
- 🛡️ Stores a primary partition table and a backup copy.
- ✅ Uses checksums to help detect corruption in its partition-table structures.
- 🖥️ Commonly used with UEFI booting.

### GPT vs. MBR

|Feature|MBR|GPT|
|---|---|---|
|Age|Older|Modern|
|Partition capacity|Limited|Much larger|
|Windows partition limit|Four primary entries|Commonly 128|
|Backup partition table|No|Yes|
|Error detection|Limited|Checksums for key structures|
|Typical boot pairing|Legacy BIOS|UEFI|

💡 **Important:** GPT and NTFS serve different purposes. GPT describes partitions; NTFS organizes files inside a volume.

---

## ⚙️ 6. How a File System Organizes Data

A file system needs more than clusters to manage files. It also maintains information about files, folders, and available storage.

Important concepts include:

### 📇 Metadata

Metadata is information about a file rather than its actual contents.

It can include:

- File name and size.
- Timestamps.
- Permissions.
- File attributes.
- References to where the file's data is stored.

### 🗃️ Directory

A directory, commonly called a folder, organizes files and other directories.

It provides the structure that lets you navigate paths such as:

`C:\Users\Alex\Documents\Notes.txt`

### 🧾 Allocation map

A file system tracks which allocation units are in use and which are available.

Different file systems use different structures to do this.

### 🧩 Fragmentation

A file is fragmented when its data is stored in separate, non-contiguous locations.

- HDDs can experience slower access because the read head must move between locations.
- SSDs handle scattered data differently and are much less affected by mechanical seek delays.

---

## 🛡️ 7. Journaling and Data Integrity

Some file systems use **journaling** to help recover from unexpected shutdowns or crashes.

### How journaling works

1. The file system records certain intended changes in a journal.
2. It applies the changes to the main file-system structures.
3. After a crash, the journal can help the system recover a consistent structure.

NTFS uses journaling mechanisms for important file-system metadata.

### What journaling does not guarantee

- It does not prevent every form of data loss.
- It does not replace backups.
- It does not necessarily protect the contents of every file against sudden power loss.

💡 **Remember:** Journaling improves recovery; backups protect against a much wider range of problems.

---

## 🔌 8. Formatting a Disk

**Formatting** prepares a volume for use with a particular file system.

For example, formatting a volume as NTFS creates the structures needed for NTFS to manage files and directories.

### Quick format vs. full format

- **Quick format:** Creates new file-system structures without performing a full sector-by-sector scan of the volume.
- **Full format:** In modern Windows versions, checks the volume for bad areas and writes zeros to its sectors.

⚠️ Formatting can make existing files inaccessible. Always back up important data before formatting a drive.

---

## 🖥️ 9. What Happens When You Open a File?

Imagine opening `report.docx`.

1. 🖱️ You select the file in File Explorer.
2. 📁 Windows accesses the directory information to identify the file.
3. 📇 The file system consults its metadata structures, such as the MFT on NTFS.
4. 📍 It determines which storage locations contain the file's data.
5. 💾 The storage device reads the requested data.
6. 🧠 Windows makes the data available to the application.

The process happens quickly, even when files are spread across many storage locations.

---

## 🧠 10. Essential Concepts at a Glance

|Term|Simple meaning|
|---|---|
|**File system**|Organizes and manages files|
|**Sector**|Addressable storage unit|
|**Cluster**|Allocation unit made up of sectors|
|**Partition**|Defined region of a disk|
|**Volume**|Storage area presented for use|
|**MBR**|Older partitioning scheme|
|**GPT**|Modern partitioning scheme|
|**NTFS**|Common Windows file system|
|**MFT**|NTFS file-record table|
|**Metadata**|Information about files|
|**Fragmentation**|File data stored in separate locations|
|**Journaling**|Helps recover file-system structures after a crash|
|**Formatting**|Creates file-system structures on a volume|
|**UEFI**|Modern PC firmware interface|
|**BIOS**|Traditional PC firmware interface|

---

## 🎯 Final Takeaway

Think of a PC's storage system as a series of layers:

**Physical disk → Partition scheme (GPT/MBR) → Partition or volume → File system (NTFS, FAT32, etc.) → Directories and files → Clusters containing file data**

Each layer has a different job:

- 💽 **Disk:** Stores the data physically.
- 🧭 **GPT/MBR:** Describes how the disk is divided into partitions.
- 🗂️ **File system:** Organizes and tracks files.
- 🧱 **Clusters:** Provide the units used to allocate space for file data.
- 📇 **MFT (NTFS):** Records information about files and directories.

Once these layers make sense, understanding how Windows stores, locates, and manages files becomes much easier.

---
