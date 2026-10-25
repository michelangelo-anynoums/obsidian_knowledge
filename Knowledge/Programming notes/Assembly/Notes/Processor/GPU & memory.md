# GPU

The **GPU (Graphics Processing Unit)** is responsible for **displaying images, videos, and graphics**. It also helps with **3D rendering** and **gaming**.

> [!important] Reference: [[GPU models]]

![[Pasted image 20260719112728.png|532]]
## Integrated Graphics

- **Integrated graphics** are **built into the CPU**.
    
- They use **less power**.
    
- Good for **everyday tasks**, **videos**, and **office work**.
    

## Dedicated Graphics Card

- A **dedicated graphics card** is a **separate processor** with its own memory.
    
- It provides **higher graphical performance**.
    
- Best for **gaming**, **video editing**, **3D design**, and **AI applications**.


---

## How does it works?

![[Pasted image 20261022061215.png]]


A **CPU** (Central Processing Unit) is a general-purpose processor with **few powerful cores** designed for **sequential processing** and complex, varied tasks like running an operating system. 

A **GPU** (Graphics Processing Unit) is a specialized processor with **hundreds or thousands of smaller cores** optimized for **parallel processing**, allowing it to handle massive amounts of simple calculations simultaneously.

**How the GPU works:**

- **Parallel Architecture:** Instead of one core doing one thing at a time, a GPU splits complex problems into thousands of smaller tasks executed at once.
    
- **Throughput over Latency:** While a CPU core finishes a single task faster, a GPU processes **thousands of tasks concurrently**, making it ideal for graphics rendering, video editing, and AI workloads.
    
- **Specialized Units:** GPUs use simplified control logic and arithmetic units to efficiently run the same instruction across multiple data points (SIMD), maximizing efficiency for repetitive mathematical operations.

---

# 🎮 GPU, VRAM & GRAM — Simple Guide

> [!abstract] 💡 The Big Picture A **GPU (Graphics Processing Unit)** processes graphics and parallel computations. It uses its own fast memory to store the data it needs to work efficiently.

## 🧠 1. Essential Concepts

### ⚙️ GPU — Graphics Processing Unit

The **GPU** is the processor responsible for rendering images, videos, 3D graphics, and accelerating AI calculations.

- 🖥️ **Integrated GPU (iGPU):** Built into the CPU or SoC; usually shares system RAM.
- 🎮 **Dedicated GPU (dGPU):** A separate graphics processor, typically with its own VRAM.

### 💾 VRAM — Video RAM

**VRAM** is the high-speed memory used by a GPU to store graphics and computing data.

It holds:

- 🖼️ Textures and images
- 📐 3D models and geometry
- 🖥️ Frame buffers (the images being displayed)
- 🤖 AI models, tensors, and intermediate calculations

**Example:** A game loads its textures into VRAM so the GPU can access them quickly while rendering the scene.

![[Pasted image 20261022064641.png|459]]

### 🔤 GRAM — Graphics RAM

**GRAM** means _Graphics RAM_. It is a general term for memory used for graphics, often referring to graphics memory in displays, embedded systems, or older hardware.

> [!tip] 🔎 VRAM vs. GRAM The terms overlap. **VRAM** is the more common modern PC term, while **GRAM** is often used in display and embedded hardware. They are not two separate memory pools that every GPU has.



### 🧩 Other Important Components

|Component|Simple explanation|
|---|---|
|🧮 **CUDA cores / shader cores**|Perform many calculations in parallel|
|🧠 **CPU**|Runs general-purpose tasks and prepares work for the GPU|
|💻 **RAM**|Main system memory used by the CPU and applications|
|⚡ **Memory bandwidth**|How quickly data moves between VRAM and the GPU|
|🔌 **PCIe**|Connects a dedicated GPU to the rest of the computer|
|❄️ **Cooling**|Prevents overheating and helps maintain performance|
|🔋 **TDP / power limit**|Indicates the GPU's power and thermal requirements|
|🖼️ **Resolution**|Number of pixels the GPU must render|
|🎞️ **FPS**|Number of frames rendered or displayed per second|

## 🔄 2. How Everything Works Together

Example: You launch a 3D game 🎮

1. 🧠 **CPU:** Runs the game logic and prepares rendering commands.
2. 💾 **RAM:** Stores the game, its code, and data needed by the CPU.
3. 🚚 **PCIe:** Transfers required data from system memory to the dedicated GPU.
4. 📦 **VRAM:** Stores textures, models, shaders, and rendering data.
5. ⚙️ **GPU cores:** Process the data and calculate the scene's pixels.
6. 🖼️ **Frame buffer:** Holds the completed image.
7. 🖥️ **Display:** Shows the image on your monitor.

**The result:** A rendered frame appears on your screen!

---

## 🧷 Quick Summary

- **GPU:** Processes graphics and parallel workloads.
- **VRAM:** Fast memory dedicated to GPU workloads.
- **GRAM:** Another graphics-memory term, commonly used in display and embedded contexts.
- **RAM:** Main memory used by the system.
- **Bandwidth:** How fast memory data can move.
- **GPU cores:** Perform the actual calculations.
- **FPS:** Measures frame production per second.

> [!quote] 💡 Final takeaway The **CPU coordinates**, the **GPU computes**, the **VRAM supplies fast working space**, and the **monitor displays the result**.