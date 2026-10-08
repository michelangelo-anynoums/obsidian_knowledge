# CPU Architecture

![[Pasted image 20261008061957.png|493]]

---

# 🖥️ CPU & Computer Architecture

> [!summary] The big picture A **CPU** executes instructions. A **microprocessor** is a CPU implemented on a chip, while a **microcontroller** combines a CPU with memory and peripherals on a single chip. **ARM, x86, and RISC-V** are examples of instruction-set architectures. **RISC** describes a design philosophy. **Chipsets** are supporting hardware that connects the CPU to other parts of a computer.

---

## 🧠 CPU — Central Processing Unit

The **CPU (Central Processing Unit)** is the main processor that executes instructions and performs calculations.

A CPU contains things such as:

- **Cores** — processing units that can execute instructions.
- **Registers** — very small and extremely fast storage.
- **Cache** — fast memory close to the CPU.
- **Control units** — coordinate the execution of instructions.
- **Execution units** — perform calculations and other operations.

A simple way to think about it:

> **CPU = the part of the computer that does the processing.**

---

# 🔲 Microprocessor

A **microprocessor** is essentially a **CPU implemented on a single integrated circuit (chip)**.

Modern desktop and laptop CPUs are microprocessors.

For example:

```
Computer
   ↓
Motherboard
   ↓
CPU
   ↓
Microprocessor
```

The terms **CPU** and **microprocessor** are often used almost interchangeably when talking about modern computers.

---

# 🔌 Microcontroller (MCU)

A **microcontroller** is different from a typical desktop CPU.

A microcontroller usually combines several things onto **one chip**:

```
┌──────────────────────────┐
│     MICROCONTROLLER      │
│                          │
│  ┌───────┐   ┌────────┐  │
│  │  CPU  │   │ Memory │  │
│  └───────┘   └────────┘  │
│                          │
│  GPIO │ Timers │ UART    │
│  SPI  │ I²C    │ ADC     │
└──────────────────────────┘
```

It may contain:

- CPU core
- RAM
- Flash/storage
- Timers
- GPIO pins
- Communication interfaces
- Analog-to-digital converters
- Other peripherals

Microcontrollers are commonly used in:

- Cars
- Washing machines
- Keyboards
- Sensors
- Toys
- Smart appliances
- Industrial equipment
- Embedded systems

> **Microprocessor:** mainly the processing unit. **Microcontroller:** CPU + memory + peripherals on one chip.

---

# 📖 Instruction Set Architecture — ISA

An **ISA (Instruction Set Architecture)** defines the instructions that a CPU understands.

Think of it as the **language spoken by the processor**.

It defines things such as:

- Instructions
- Registers
- Data types
- Memory operations
- How software communicates with the CPU

Examples of ISAs include:

- **x86 / x86-64**
- **ARM / AArch64**
- **RISC-V**

---

# ⚙️ RISC

**RISC** stands for:

> **Reduced Instruction Set Computer**

RISC is a design philosophy where the instruction set is generally designed around relatively simple, regular instructions.

The idea is to make instructions efficient to decode and execute.

RISC architectures commonly emphasize:

- Simple instructions
- Regular instruction formats
- Efficient execution
- Large numbers of general-purpose registers
- A load/store approach to memory

Examples include:

- **ARM**
- **RISC-V**
- **MIPS**

> ⚠️ **RISC is not the same thing as ARM.** **RISC = design philosophy** **ARM = a specific instruction-set architecture based on RISC principles**

---

# 🦾 ARM

**ARM** is a family of processor architectures based on RISC principles.

ARM processors are extremely common in:

- Smartphones
- Tablets
- Embedded devices
- Microcontrollers
- Single-board computers
- Servers
- Laptops

You may encounter names such as:

```
ARM
│
├── ARM32
│
└── ARM64 / AArch64
```

Modern 64-bit ARM systems generally use **AArch64**.

ARM is particularly popular because of its combination of performance and power efficiency.

---

# 💻 x86

**x86** is another major CPU architecture family.

It originated with Intel's **8086** processor.

The name comes from the older processor names:

```
8086
80186
80286
80386
80486
   ↓
 x86
```

x86 became extremely common in personal computers.

Today, desktop and laptop processors from companies such as **Intel and AMD** commonly implement **x86-64**.

---

# 🔢 32-bit vs 64-bit

The terms **32-bit** and **64-bit** describe aspects of how a processor architecture handles data, registers, addresses, and instructions.

A simplified way of thinking about it:

> **32-bit → generally works with 32-bit-wide registers/addresses** **64-bit → generally works with 64-bit-wide registers/addresses**

One major consequence is the amount of memory that can theoretically be addressed.

### 32-bit

```
2³² bytes
≈ 4 GB
```

A 32-bit system therefore has a theoretical address space of around **4 GB**, although the usable amount can be lower.

### 64-bit

```
2⁶⁴ bytes
≈ 18.4 exabytes
```

A 64-bit architecture has a vastly larger theoretical address space.

> Modern operating systems and CPUs don't necessarily support the entire theoretical 64-bit address space.

---

# 🆚 32-bit vs 64-bit

||32-bit|64-bit|
|---|---|---|
|Register width|Generally 32-bit|Generally 64-bit|
|Theoretical address space|2³²|2⁶⁴|
|Maximum theoretical address space|~4 GB|~18.4 EB|
|Modern PCs|Mostly obsolete|Standard|
|Large memory support|Limited|Much greater|
|Common today|Older systems / embedded|PCs, phones, servers|

---

# 🧩 Chipset

A **chipset** is supporting hardware on a motherboard that provides various communication and I/O functions.

Historically, PCs often had two major chipset components:

```
CPU
 │
 ├── Northbridge
 │
 └── Southbridge
```

The **Northbridge** traditionally handled high-speed communication such as:

- RAM
- Graphics
- CPU communication

The **Southbridge** handled slower I/O such as:

- USB
- SATA
- Audio
- Other peripherals

Modern CPUs have integrated many functions that used to belong to the Northbridge.

So modern chipsets are generally more focused on providing **additional I/O and connectivity**.

---

# 🔗 How Everything Fits Together

Here's the important relationship:

```
                    COMPUTER
                       │
              ┌────────┴────────┐
              │                 │
             CPU            Other Hardware
              │
       ┌──────┴──────┐
       │             │
      ISA       Microarchitecture
       │
 ┌─────┼─────────┐
 │     │         │
x86   ARM     RISC-V
 │
 ├── 32-bit
 │
 └── 64-bit
```

And for embedded systems:

```
              MICROCONTROLLER
                     │
        ┌────────────┼────────────┐
        │            │            │
       CPU         Memory     Peripherals
                                  │
                         ┌────────┼────────┐
                         │        │        │
                        GPIO     UART     SPI
```

---

# 🏗️ CPU vs Microprocessor vs Microcontroller

|Term|Simple meaning|
|---|---|
|**CPU**|The unit that executes instructions|
|**Microprocessor**|A CPU implemented on a chip|
|**Microcontroller**|CPU + memory + peripherals on one chip|
|**Chipset**|Supporting hardware providing communication/I/O functions|
|**ISA**|The instructions a CPU understands|
|**RISC**|A processor design philosophy|
|**ARM**|A family of RISC-based processor architectures|
|**x86**|A processor architecture family|
|**32-bit**|Architecture with 32-bit characteristics|
|**64-bit**|Architecture with 64-bit characteristics|

---

# ⭐ The Important Bits

If you remember nothing else, remember these:

1. **CPU** → executes instructions.
2. **Microprocessor** → essentially a CPU on a chip.
3. **Microcontroller** → CPU + memory + peripherals on one chip.
4. **ISA** → defines the instructions a CPU understands.
5. **RISC** → a philosophy of using relatively simple, regular instructions.
6. **ARM** → a family of RISC-based processor architectures.
7. **x86** → a major processor architecture family.
8. **32-bit vs 64-bit** → describes important characteristics of how an architecture handles data and addresses.
9. **Chipset** → provides supporting communication and I/O functions around the CPU.
10. **ARM and x86 are not the same thing as CPU manufacturers** — they describe architectures; companies build processors that implement those architectures.

> [!tip] The simplest mental model **CPU = what does the work** **ISA = language it understands** **RISC = a design philosophy** **ARM / x86 / RISC-V = architectures** **Microprocessor = CPU on a chip** **Microcontroller = CPU + memory + peripherals** **Chipset = supporting communication/I/O hardware** **32-bit / 64-bit = characteristics of the architecture and its data/address handling**