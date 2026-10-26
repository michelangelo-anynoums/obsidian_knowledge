![[Pasted image 20260728115926.png|547]]

# 7.2 Logic Gates

## What are Logic Gates?

**Logic gates** are **electronic circuits** that perform **Boolean logic**.

They take **binary inputs (0 or 1)** and produce **one binary output (0 or 1)**.

> **Logic gates** are the **basic building blocks of processors** and all digital circuits.

---

## Boolean Logic

**Boolean logic** uses only **two values**:

- **0 = False**
    
- **1 = True**
    

Computers use Boolean logic to **make decisions** and **process data**.

---

# AND Gate

The **AND** gate gives **1** only if **both inputs are 1**.

|A|B|Output|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

![[Pasted image 20260728120221.png|563]]
### Easy Example

A door opens only if **two keys** are used.

- Both keys present → **Door opens (1)**
    
- One or no key → **Door stays closed (0)**
    

---

# OR Gate

The **OR** gate gives **1** if **at least one input is 1**.

|A|B|Output|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

![[Pasted image 20260728120544.png|532]]
### Easy Example

A room light turns on if **either switch** is turned on.

---

# NOT Gate

The **NOT** gate **reverses** the input.

|Input|Output|
|---|---|
|0|1|
|1|0|

### Easy Example

If the signal is **1**, the output becomes **0**.

---

# XOR Gate

The **XOR (Exclusive OR)** gate gives **1** only if the inputs are **different**.

|A|B|Output|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

### Easy Example

A lamp turns on only when **exactly one switch** is on.

---

# Logic Gates in Processors

Processors contain **millions or billions of logic gates**.

These gates work together to:

- **Perform calculations**
    
- **Compare values**
    
- **Store data**
    
- **Make decisions**
    

Without logic gates, a computer **cannot process information**.

---
> Symbol "x" means AND
> Symbol "+" means OR

# Simple Boolean Equations

### AND

$$
Y = A \cdot B  
$$

---

### OR

$$ 
Y = A + B  
$$

---

### NOT

$$
Y = \overline{A}  
$$

---

### XOR

$$ 
Y = A \oplus B  
$$

Where:

- **A** = first input
    
- **B** = second input
    
- **Y** = output
    

---

# Resolved Example 1

### Question

An **AND** gate has:

- A = **1**
    
- B = **1**
    

What is the output?

### Solution

Both inputs are **1**.

$$
1 \text{ AND } 1 = 1  
$$

**Answer:** **1**

---

# Resolved Example 2

### Question

An **OR** gate has:

- A = **0**
    
- B = **1**
    

What is the output?

### Solution

At least one input is **1**.

$$
0 \text{ OR } 1 = 1  
$$

**Answer:** **1**

---

# Resolved Example 3

### Question

A **XOR** gate has:

- A = **1**
    
- B = **1**
    

What is the output?

### Solution

The inputs are **the same**.

$$
1 \text{ XOR } 1 = 0  
$$

**Answer:** **0**

---

# Key Points

- **Logic gates** process **binary signals**.
    
- **Boolean logic** uses only **0** and **1**.
    
- **AND** → both inputs must be **1**.
    
- **OR** → at least one input is **1**.
    
- **NOT** → reverses the input.
    
- **XOR** → output is **1** only when the inputs are **different**.
    
- **Logic gates** are the **building blocks of processors**.

---
