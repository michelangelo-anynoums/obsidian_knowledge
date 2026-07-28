# 7.4 Sequential Circuits

## What are Sequential Circuits?

A **sequential circuit** is a digital circuit whose **output depends on:**

![[Pasted image 20260728121501.png]]

- The **current input**
    
- The **previous inputs (history)**
    

Unlike a combinational circuit, a sequential circuit **has memory**.

> **Current input + Previous state → Output**

---

## Memory Elements

A **memory element** is a component that **stores one or more bits of data**.

The most common memory elements are:

- **Flip-flops**
    
- **Registers**
    

These components allow a computer to **remember information**.

---

## State Depends on History

The **state** of a sequential circuit is the information stored in its memory.

Because it has memory, the output depends on:

- **Current input**
    
- **Previous state**
    

This means the circuit can remember what happened before.

---

## Easy Example

Imagine a **light switch**.

- Press the button once → **Light ON**
    
- Press the button again → **Light OFF**
    

The result depends on the **previous state** of the light.

---

## Flip-Flop

A **flip-flop** is the simplest memory element.

It stores **one bit**.

- **0**
    
- **1**
    

A flip-flop keeps its value until it receives a new input.

---

## Where are Sequential Circuits Used?

Sequential circuits are used in:

- **Computer memory (RAM)**
    
- **Registers**
    
- **Counters**
    
- **Digital clocks**
    
- **Processors**
    

---

# Simple Equation

The next state depends on the **current input** and the **current state**.


$$
\text{Next State} = f(\text{Current Input},\ \text{Current State})
$$


Where:

- **Current Input** = new binary input
    
- **Current State** = stored value
    
- **Next State** = new stored value
    

---

# Resolved Example 1

### Question

A flip-flop stores **1**.

A new input does **not** change the value.

What is the stored value?

### Solution

The flip-flop keeps its previous value.

**Answer:** **1**

---

# Resolved Example 2

### Question

A sequential circuit stored **0**.

A new input changes the stored value to **1**.

What is the new state?

### Solution

The memory updates its value.

**Answer:** **1**

---

# Resolved Example 3

### Question

Which circuit has memory?

- **A)** Combinational circuit
    
- **B)** Sequential circuit
    

### Solution

Only a **sequential circuit** stores previous information.

**Answer:** **B) Sequential circuit**

---

# Key Points

- A **sequential circuit** has **memory**.
    
- The **output depends on the current input and previous state**.
    
- **Memory elements** store binary data.
    
- A **flip-flop** stores **1 bit**.
    
- Sequential circuits are used in **RAM, registers, counters, and processors**.

---
