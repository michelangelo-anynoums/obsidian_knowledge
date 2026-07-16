
## What is **psutil**?

**`psutil` (process and system utilities)** lets Python talk to your computer and ask questions like:

- How much **CPU** is being used?
    
- How much **memory (RAM)** is free?
    
- What **processes** (programs) are running?
    
- How much **disk space** is left?
    
- How busy is the **network**?
    

It works on **Windows, macOS, and Linux**.

---

## Installing **psutil**

```Python
pip install psutil
```

Then import it in Python:

```Python
import psutil
```

---

## Core ideas (important concepts)

Think of **psutil** as giving you **status reports** about your system:

1. **CPU info** – how busy your processor is
    
2. **Memory info** – RAM usage
    
3. **Disk info** – storage usage
    
4. **Network info** – sent/received data
    
5. **Processes** – running programs (like Chrome, Python, etc.)
    

---

## CPU information

### CPU usage (percentage)

```Python
import psutil  
cpu_usage = psutil.cpu_percent(interval=1) 
print(cpu_usage)
```

📌 What this means:

- `interval=1` → measure CPU usage over 1 second
    
- Output: something like `23.5` (23.5% usage)
    

---

### Number of CPU cores

```Python
print(psutil.cpu_count())
```

Logical cores (including hyper-threading):

```Python
print(psutil.cpu_count(logical=True))
```

---

## Memory (RAM) information

### RAM usage

```Python
memory = psutil.virtual_memory() print(memory)
```

This prints a lot of info. Common ones:

```Python
print(memory.total) # total RAM (bytes) 
print(memory.used) # used RAM 
print(memory.percent) # usage percentage
```

Example (more readable):

```Python
print(f"RAM used: {memory.percent}%")
```

---

## Disk (storage) information

### Disk usage

```Python
disk = psutil.disk_usage('/') print(disk)
```

Common fields:

```Python
print(disk.total) 
print(disk.used) 
print(disk.free) 
print(disk.percent)
```

📌 On Windows, you might use:

```Python
psutil.disk_usage('C:\\')
```

---

## Network information

### Network usage (bytes sent/received)

```Python
net = psutil.net_io_counters() print(net)
```

Useful fields:

```Python
print(net.bytes_sent) print(net.bytes_recv)
```

---

## Working with processes (important part!)

### List all running processes

```Python
for proc in psutil.process_iter():     
	print(proc.pid, proc.name())
```

📌 This shows:

- `pid` → process ID
    
- `name()` → program name
    

---

### Get info about a specific process

```Python
pid = 1234  # example PID 
p = psutil.Process(pid)  
print(p.name()) 
print(p.status()) 
print(p.cpu_percent()) 
print(p.memory_info())
```

---

### Find processes by name

```Python
for proc in psutil.process_iter(['pid', 'name']):     
	if proc.info['name'] == 'python.exe':         
		print(proc.info)
```

Great for monitoring or automation.

---

## A small real example: simple system monitor

```Python
import psutil  
print("CPU:", psutil.cpu_percent(), "%") 
print("RAM:", psutil.virtual_memory().percent, "%") 
print("Disk:", psutil.disk_usage('/').percent, "%")
```

This could run every few seconds to watch system health.

---

## When is **psutil** useful?

- System monitoring tools
    
- Performance tracking
    
- Server health checks
    
- Killing or managing processes
    
- Learning how operating systems work

----
## 3️⃣ Key USB-Related Concepts in **psutil**

### 🔹 1. USB Storage = Disk Partitions

When you plug in a USB drive:

- The OS mounts it as a **disk**
    
- `psutil` can see it via **disk partitions**
    

Key function:

```Python
import psutil
psutil.disk_partitions()
```

---

### 🔹 2. Disk Usage (How much space?)

Once you find the USB mount point, you can check:

- Total size
    
- Used space
    
- Free space
    

Function:

```Python
import psutil
psutil.disk_usage(path)
```

---

### 🔹 3. Detecting Plug / Unplug (Polling)

**psutil** cannot “listen” to USB events.  
Instead, you:

1. Check connected disks
    
2. Wait
    
3. Check again
    
4. Compare results
    

This is called **polling**.

---

## 4️⃣ Example: List All Connected Drives (Including USB)

```Python
import psutil  

partitions = psutil.disk_partitions()  

for p in partitions:     
	print("Device:", p.device)     
	print("Mount point:", p.mountpoint)     
	print("File system:", p.fstype)     
	print("Options:", p.opts)     
	print("-" * 30)
```

💡 USB drives often:

- Appear under `/media`, `/mnt` (Linux)
    
- Appear as `E:\`, `F:\` (Windows)
    
- Have removable flags in options
    

---

## 5️⃣ Example: Detect USB Flash Drives (Simple Method)

### Windows-friendly approach

```Python
import psutil  
usb_drives = []  

for p in psutil.disk_partitions():     
		if "removable" in p.opts.lower():         
			usb_drives.append(p)  
			for usb in usb_drives:     
				print("USB Device:", usb.device, "at", usb.mountpoint)
```

---

### Linux/macOS approach (common pattern)

```Python
import psutil

for p in psutil.disk_partitions():     
	if "/media" in p.mountpoint or "/mnt" in p.mountpoint:        
		print("Possible USB:", p.device, p.mountpoint)
```

---

## 6️⃣ Example: Check USB Drive Size and Free Space

```Python
import psutil

path = "/media/usb"   # change this to your USB mount point 
usage = psutil.disk_usage(path)

print("Total:", usage.total // (1024**3), "GB") 
print("Used:", usage.used // (1024**3), "GB") 
print("Free:", usage.free // (1024**3), "GB")
```

---

## 7️⃣ Example: Detect USB Insert / Removal (Polling)

```Python
import psutil
import time
   
def get_devices():
     return set(p.device for p in psutil.disk_partitions())  
     
old_devices = get_devices()  

while True:     
	time.sleep(2)     
	new_devices = get_devices()      
	added = new_devices - old_devices     
	removed = old_devices - new_devices      
	for d in added:         
		print("USB inserted:", d)      
		for d in removed:         
			print("USB removed:", d)      
			old_devices = new_devices
```

🧠 Concept learned here:

- `set()` → helps compare old vs new states
    
- Polling → checking repeatedly instead of listening
---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]