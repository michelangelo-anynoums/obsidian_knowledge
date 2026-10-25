
# John von Neumann Architecture — Components Explained

![[imgupscaler-enhanced.png|523]]

The **von Neumann architecture** is a computer design in which **instructions and data are stored in the same main memory**. The CPU retrieves instructions from memory, processes them, and produces results.
**Reference:** [CPU simulator](https://vnmsim.c2r0b.ovh/en-us)

![[Pasted image 20261004111943.png]]

## 1. CPU — Central Processing Unit

The **CPU** is the "brain" of the computer. It executes the instructions of a program.

The CPU mainly contains:

- **Control Unit (CU)**
    
- **Arithmetic Logic Unit (ALU)**
    
- **Registers**
    

### Control Unit (CU)

The **Control Unit** manages and coordinates the CPU.

It tells the other components **what to do and when to do it**.

For example, if an instruction says:

> Add 5 and 3.

The Control Unit tells the CPU to:

1. Get the instruction from memory.
    
2. Get the required data.
    
3. Tell the ALU to perform the addition.
    
4. Store the result.
    

The Control Unit does not normally perform the calculation itself. It **controls the process**.

![[Pasted image 20261004111930.png]]

---

## 2. ALU — Arithmetic Logic Unit

The **ALU** performs calculations and logical operations.

### Arithmetic operations

- Addition: `5 + 3 = 8`
    
- Subtraction: `10 - 4 = 6`
    
- Multiplication
    
- Division
    

### Logical operations

The ALU can also compare values:

- `5 > 3` → **True**
    
- `5 = 5` → **True**
    
- `2 < 1` → **False**
    

It can also perform operations such as **AND, OR, and NOT**, which are important when working with binary data.

**Simple idea:**

> The ALU is the part of the CPU that **does the calculations and logical decisions**.

---

## 3. Registers

**Registers are very small, extremely fast storage locations inside the CPU.**

They temporarily hold information that the CPU is currently using.

Think of registers as the CPU's **working desk**. Instead of constantly going to the large but slower main memory, the CPU keeps important information close at hand.

### Example

Suppose the CPU needs to calculate:

`5 + 3`

It could temporarily place the numbers in registers:

**Register 1:** `5`  
**Register 2:** `3`

The ALU adds them:

`5 + 3 = 8`

The result can then be placed into another register:

**Register 3:** `8`

### Important CPU registers

Different CPUs have different registers, but common examples include:

**Program Counter (PC)**  
Stores the address of the **next instruction** that the CPU should fetch.

**Instruction Register (IR)**  
Stores the **current instruction** being decoded or executed.

**Memory Address Register (MAR)**  
Stores the **address in memory** that the CPU wants to access.

**Memory Data Register (MDR)**  
Stores the **data being transferred to or from memory**.

### A simple example

Imagine memory contains:

|Address|Content|
|---|---|
|100|`ADD 5, 3`|
|101|`...`|

The **PC** might contain `100`, meaning:

> "The next instruction is at memory address 100."

The CPU gets that instruction and puts it into the **IR**.

The instruction is then decoded and executed.

---

## 4. Main Memory (RAM)

**RAM (Random Access Memory)** stores programs and data that the computer is currently using.

For example, when you open a calculator program, its instructions and the data it uses can be loaded into RAM.

In the von Neumann architecture, **both instructions and data share the same memory**.

For example:

|Memory Address|Content|
|---|---|
|100|Instruction: ADD|
|101|Data: 5|
|102|Data: 3|
|103|Result: 8|

Each location has an **address**, similar to a house having an address.

The CPU uses these addresses to find the information it needs.

---

## 5. Bus

A **bus** is a set of electrical pathways used to transfer information between different parts of a computer.

Think of a bus like a **road system**:

- Memory and CPU are like different buildings.
    
- Data travels between them.
    
- The bus provides the paths for that information to travel.
    

There are three important types of buses:

### Data Bus

The **data bus carries the actual data**.

For example:

`0101 0011`

could represent a piece of data being transferred between memory and the CPU.

The data bus is generally **bidirectional**, meaning information can travel in both directions.

### Address Bus

The **address bus carries the address of the memory location** that the CPU wants to access.

For example:

> "I want the information stored at address 100."

The address bus carries:

`100`

It generally travels **from the CPU to memory**.

### Control Bus

The **control bus carries control signals** that coordinate operations.

For example:

- Read from memory
    
- Write to memory
    
- Interrupt
    
- Timing/control signals
    

The Control Unit uses these signals to coordinate the different components.

### Easy way to remember

|Bus|Carries|Think of it as|
|---|---|---|
|**Data bus**|Data|📦 The package|
|**Address bus**|Location|🏠 The address|
|**Control bus**|Instructions/signals|🚦 The traffic signals|

---

## 6. Input Devices

**Input devices** allow information to enter the computer.

Examples:

- Keyboard
    
- Mouse
    
- Microphone
    
- Scanner
    
- Camera
    

For example, when you press the letter **A** on a keyboard, the computer receives that input and processes it.

---

## 7. Output Devices

**Output devices** allow the computer to communicate the results to the user.

Examples:

- Monitor
    
- Printer
    
- Speakers
    
- Headphones
    

For example, after calculating `5 + 3`, the computer could display:

**8**

on the monitor.

---

# 🔄 How Everything Works Together

Suppose you run a program that calculates:

**5 + 3**

A simplified process is:

**1. Program stored in RAM**  
The instructions and data are placed in memory.

**2. PC points to the next instruction**  
The Program Counter contains the address of the instruction.

**3. Address travels through the address bus**  
The CPU requests the instruction from that memory address.

**4. Instruction travels through the data bus**  
The instruction is transferred from memory to the CPU.

**5. Instruction enters the IR**  
The Instruction Register holds the current instruction.

**6. Control Unit decodes it**  
The CU determines what needs to happen.

**7. Data is placed in registers**  
The values `5` and `3` are made available to the CPU.

**8. ALU performs the calculation**

`5 + 3 = 8`

**9. Result is stored**  
The result `8` can be placed in a register and eventually stored in memory.

**10. Output**  
The result can be sent to an output device, such as a monitor.

---

# ⭐ Quick Summary

|Component|Main job|
|---|---|
|**CPU**|Executes instructions|
|**Control Unit**|Controls and coordinates operations|
|**ALU**|Performs calculations and logic|
|**Registers**|Very fast temporary storage inside the CPU|
|**RAM**|Stores instructions and data currently being used|
|**Data Bus**|Carries data|
|**Address Bus**|Carries memory addresses|
|**Control Bus**|Carries control signals|
|**Input**|Sends information into the computer|
|**Output**|Sends results out of the computer|

### 🧠 Remember this

**CPU = Brain**  
**Registers = Working desk**  
**RAM = Main workspace/storage**  
**ALU = Calculator**  
**Control Unit = Manager**  
**Buses = Roads carrying information**