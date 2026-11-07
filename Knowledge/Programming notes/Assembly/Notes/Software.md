# 💻 OS, Firmware, Drivers & Software

> [!abstract] The big picture 
> These are the main components that allow a computer to start, communicate with hardware, and run applications.

## 1. ⚙️ Firmware

**Firmware** is low-level software stored inside a hardware device. It controls how that device operates.

Examples:

- BIOS / UEFI → Starts and initializes the computer.
- SSD firmware → Controls the storage device.
- Router firmware → Controls router functionality.

💡 Firmware lives in non-volatile memory and is closely tied to hardware.

## 2. 🐧 Operating System (OS)

The **Operating System** manages computer resources and provides an environment for applications.

Main responsibilities:

- Manage CPU and memory.
- Manage files and storage.
- Manage processes.
- Control user permissions.
- Communicate with hardware through drivers.

Examples:

- Windows
- Linux (Ubuntu, Debian)
- macOS
- Android

## 3. 🔌 Drivers

A **driver** allows the operating system to communicate with a specific hardware device.

Examples:

- Graphics driver → GPU.
- Audio driver → Sound card.
- Network driver → Ethernet or Wi-Fi adapter.
- Printer driver → Printer.

💡 Without the correct driver, hardware might not work properly or may have limited functionality.

## 4. 📦 Software

**Software** is a general term for programs and instructions that perform tasks.

Two main categories:

|Type|Purpose|Examples|
|---|---|---|
|System software|Runs and manages the computer|OS, drivers, utilities|
|Application software|Performs user tasks|Chrome, VS Code, VLC|

Examples:

- Web browsers
- Text editors
- Games
- Database systems
- Development tools

## 5. 🔗 How everything works together

Example: You open a game on your computer.

1. **Firmware:** Initializes hardware during startup.
2. **OS:** Manages the computer and runs the game.
3. **Driver:** Allows the OS to communicate with the GPU.
4. **Software:** The game uses the system to display graphics and process input.

## 6. 🧠 Visual architecture


```
        👤 USER
           |
           ▼
   📦 APPLICATION SOFTWARE
      Chrome / Games / VS Code
           |
           ▼
      🐧 OPERATING SYSTEM
       Windows / Linux
           |
           ▼
       🔌 DRIVERS
     GPU / Audio / Network
           |
           ▼
       🖥️ HARDWARE
     CPU / GPU / SSD / RAM

  ⚙️ FIRMWARE
  Initializes and controls
  hardware at a low level
```

_Note: Firmware operates within hardware devices and is not simply another layer between the OS and hardware._

---
