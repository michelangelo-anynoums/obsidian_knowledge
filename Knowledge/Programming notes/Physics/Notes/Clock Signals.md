# 7.5 Clock Signals

## What is a Clock Signal?

![[Pasted image 20260728121837.png|505]]

A **clock signal** is a regular **electrical pulse** that controls the timing of a computer.

It tells the processor **when to perform each operation**.

> A clock signal acts like a **heartbeat** for the computer.

---

## Timing Synchronization

**Timing synchronization** means that all parts of the computer **work together at the correct time**.

The clock signal keeps all components **synchronized**.

Without a clock signal:

- Operations could happen in the wrong order.
    
- Data could be lost or corrupted.
    

---

## CPU Cycles

A **CPU cycle** is **one complete clock pulse**.

During each cycle, the CPU performs a small task, such as:

- **Fetching** an instruction
    
- **Decoding** the instruction
    
- **Executing** the instruction
    

The CPU repeats these cycles **millions or billions of times every second**.

---

## Clock Frequency

The **clock frequency** tells us **how many clock cycles occur each second**.

It is measured in **Hertz (Hz)**.

### Formula


$$
f=\frac{1}{T}
$$


Where:

- **(f)** = frequency (Hz)
    
- **(T)** = period (s)
    

---

## Easy Example

A clock has a frequency of **2 Hz**.

This means it produces:

- **2 clock cycles every second**
    

---

## Why are Clock Signals Important?

Clock signals help the CPU to:

- **Stay synchronized**
    
- **Execute instructions correctly**
    
- **Control data flow**
    
- **Coordinate all hardware components**
    

---

# Resolved Example 1

### Question

A CPU clock has a frequency of **5 Hz**.

How many clock cycles occur in **1 second**?

### Solution

A frequency of **5 Hz** means **5 cycles per second**.

**Answer:** **5 CPU cycles**

---

# Resolved Example 2

### Question

The clock period is:
$$
T = 0.5\ \text{s}
$$
Find the frequency.

### Solution

Use the formula:


$$
f=\frac{1}{T}
$$

Substitute the value:


$$
f=\frac{1}{0.5}=2\ \text{Hz}
$$


**Answer:** **2 Hz**

---

# Resolved Example 3

### Question

A processor receives **10 clock pulses**.

How many CPU cycles are completed?

### Solution

One clock pulse equals **one CPU cycle**.

**Answer:** **10 CPU cycles**

---

# Key Points

- A **clock signal** is an electrical pulse that controls the CPU.
    
- It keeps all computer components **synchronized**.
    
- A **CPU cycle** is **one clock pulse**.
    
- **Clock frequency** is measured in **Hertz (Hz)**.
    
- The relationship between frequency and period is:
    


$$
f=\frac{1}{T}
$$

---
