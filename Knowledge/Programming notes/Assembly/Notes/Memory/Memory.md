# 🧠 RAM, DRAM, SRAM, DDR & HBM

> [!abstract] The big picture **RAM** is a computer's short-term working memory. **DRAM** and **SRAM** are types of RAM, while **DDR** and **HBM** are technologies for implementing high-performance DRAM.

## 1. 🧩 RAM — Random Access Memory

RAM temporarily stores the data and instructions a computer needs right now.

- ⚡ Fast to access.
- 📝 Usually volatile: data disappears when power is lost.
- 🎯 Lets the CPU work without constantly retrieving data from an SSD.

**Example:** When you open a browser, its active tabs and working data can be stored in RAM.

Think of RAM as your **desk**: the bigger it is, the more things you can work on at once.

![[Pasted image 20261018153725.png|315]]

## 2. ⚙️ DRAM — Dynamic RAM

DRAM stores each bit using a tiny capacitor and a transistor. The capacitor gradually loses its charge, so the memory must be **refreshed repeatedly**.

- 💰 Relatively inexpensive per gigabyte.
- 📦 High capacity.
- 🔄 Requires refreshing.

**Example:** The 16 GB or 32 GB of main memory in a typical laptop is usually DRAM.

**Remember:** DRAM is dense and affordable, making it ideal for large amounts of memory.

## 3. 🚀 SRAM — Static RAM

SRAM stores each bit using a small transistor circuit, typically a group of six transistors per bit. It retains its value while powered without periodic refreshing.

- ⚡ Very fast.
- 💸 More expensive per bit.
- 📏 Takes up more chip area per bit than DRAM.

**Example:** CPU caches, such as L1, L2 and often L3, commonly use SRAM.

**Remember:** SRAM is fast but expensive, so it is ideal for small, frequently accessed data stores.

## 4. 🔢 DDR — Double Data Rate SDRAM

DDR is a family of high-speed DRAM technologies. It transfers data on both the rising and falling edges of the clock signal.

Common generations include DDR3, DDR4 and DDR5.

- 📈 Each generation can improve bandwidth and efficiency.
- 🧩 Used for a computer's main memory.
- ⚠️ Different generations are generally not physically or electrically interchangeable.

**Example:** A PC with 32 GB of DDR5 RAM uses DRAM modules to supply data to its CPU.

**Remember:** DDR is not a separate memory-cell type like SRAM. It is a way of designing and operating synchronous DRAM.

## 5. 🏎️ HBM — High Bandwidth Memory

HBM is a high-bandwidth DRAM technology that stacks memory dies vertically and connects them to a processor through a very wide interface, commonly using advanced packaging.

- 🚄 Extremely high memory bandwidth.
- 📚 Multiple memory dies can be stacked.
- 💻 Common in AI accelerators, GPUs and high-performance computing.
- 💰 More complex and expensive to manufacture and package.

**Example:** An AI accelerator uses HBM to feed a large amount of data to thousands of processing units during neural-network training.

**Remember:** HBM prioritizes moving huge amounts of data quickly, rather than simply maximizing capacity at the lowest cost.

![[Pasted image 20261018154044.png|657]]

---

## 📊 Quick comparison

|Type|Main advantage|Typical use|
|---|---|---|
|**RAM**|Temporary working memory|Active programs and data|
|**DRAM**|High capacity, low cost per bit|Main system memory|
|**SRAM**|Very low latency|CPU caches|
|**DDR**|High-speed DRAM transfers|Desktop and laptop RAM|
|**HBM**|Extremely high bandwidth|AI accelerators and high-end GPUs|

## 🔗 How they fit together

Imagine a computer running an AI application:

1. **RAM** is the working memory available to the system.
2. **DRAM** is the underlying memory-cell technology used in typical system RAM.
3. **DDR5** is one technology used to implement that main memory.
4. **SRAM** holds small, frequently needed pieces of data close to the CPU.
5. **HBM** supplies very high data bandwidth to certain GPUs and AI accelerators.

### 🧠 The five-second memory trick

- **RAM** = the general concept.
- **DRAM** = dense, affordable memory.
- **SRAM** = fast, small memory.
- **DDR** = a family of high-speed DRAM standards.
- **HBM** = stacked DRAM designed for very high bandwidth.

> [!tip] Final takeaway These terms are not five competing alternatives. They describe different levels or aspects of memory: a general category, two cell technologies, and two approaches to delivering high-performance DRAM.

---
