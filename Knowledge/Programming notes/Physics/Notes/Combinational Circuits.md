# 7.3 Combinational Circuits

![[Pasted image 20260728121121.png|572]]

## What are Combinational Circuits?

A **combinational circuit** is a digital circuit whose **output depends only on the current input**.

It **does not remember** previous inputs because it has **no memory**.

> **Current input → Output**

---

## How Do They Work?

Combinational circuits are built using **logic gates** such as:

- **AND**
    
- **OR**
    
- **NOT**
    
- **XOR**
    

The logic gates work together to produce the correct output.

---

## Adders

An **adder** is a combinational circuit that **adds binary numbers**.

The simplest adder is a **Half Adder**.

It has:

- **2 inputs:** A and B
    
- **2 outputs:** **Sum (S)** and **Carry (C)**
    

### Half Adder Equations

**Sum**


$$
S = A \oplus B
$$


**Carry**


$$
C = A \cdot B
$$


### Easy Example

Add:

- **A = 1**
    
- **B = 0**
    
- **Sum = 1**
    
- **Carry = 0**
    

Result:

**1 + 0 = 1**

---

## Multiplexers (MUX)

A **multiplexer (MUX)** is a circuit that **selects one input from several inputs** and sends it to the output.

It acts like a **switch**.

### Easy Example

Imagine **four roads** leading to one tunnel.

The multiplexer chooses **only one road** to enter the tunnel.

---

## Why are Combinational Circuits Important?

They are used to:

- **Perform calculations**
    
- **Select data**
    
- **Compare values**
    
- **Build processors and digital systems**
    

---

# Resolved Example 1

### Question

A combinational circuit receives:

- A = **1**
    
- B = **1**
    

Will the output depend on previous inputs?

### Solution

No.

A combinational circuit depends **only on the current inputs**.

**Answer:** The output depends only on **A = 1** and **B = 1**.

---

# Resolved Example 2

### Question

A Half Adder has:

- A = **1**
    
- B = **1**
    

Find the **Sum** and **Carry**.

### Solution

**Sum**


$$
S = A \oplus B = 1 \oplus 1 = 0
$$


**Carry**


$$
C = A \cdot B = 1 \cdot 1 = 1
$$


**Answer:**

- **Sum = 0**
    
- **Carry = 1**
    

---

# Resolved Example 3

### Question

A multiplexer has four inputs:

- Input 1 = 0
    
- Input 2 = 1
    
- Input 3 = 0
    
- Input 4 = 1
    

If the multiplexer selects **Input 2**, what is the output?

### Solution

The multiplexer sends the selected input directly to the output.

**Answer:** **1**

---

# Key Points

- A **combinational circuit** has **no memory**.
    
- The **output depends only on the current input**.
    
- **Adders** perform **binary addition**.
    
- **Multiplexers (MUX)** select **one input** from several inputs.
    
- Combinational circuits are important **building blocks of processors**.

---
