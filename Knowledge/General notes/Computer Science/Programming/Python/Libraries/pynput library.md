# 🐍 **Python ==pynput== Library — Introduction**
 **pynput**  is a Python library that lets you ==control and monitor input devices== like the **keyboard** and **mouse**. You can use it to create programs that listen to what you type or track mouse movements, or even control these devices from your code. ==It's great for automation, creating custom shortcuts, and making programs that respond to user input in real-time.==

### **Main Concepts of pynput**

1. **Controller**
    
    - The `Controller` class allows you to ==control the keyboard and mouse.==
        
    - With it, you can **type keys**, **move the mouse**, **click** buttons, and more.
        
    - Example: You can make the program type something automatically or move the mouse to a specific spot.
        
2. **Listener**
    
    - The `Listener` class ==listens to events from the keyboard or mouse.== It helps you track when a key is pressed or released, or when the mouse is moved or clicked.
        
    - Example: You can set up a program to detect when you press a specific key and then perform an action, like running a function.
        
3. **Mouse**
    
    - This part of `pynput` focuses on ==interacting with the mouse.== You can **move** the mouse, **click** buttons, and **scroll**.
        
    - Example: Automatically clicking through a series of buttons in a program.
        
4. **Keyboard**
    
    - ==This part focuses on the keyboard.==You can **press** and **release keys**, and **listen** for key presses.
        
    - Example: Creating a shortcut that triggers an action when you press a specific key combination.
        

### **Basic Example**

Here's a simple example that listens for keyboard events:

```Python
from pynput.keyboard import Listener

def on_press(key):     
	print(f"Key pressed: {key}")  # Listen for key presses with 
	
with Listener(on_press=on_press) as listener:     
	listener.join()
```

In this example, the program will print the key every time you press a key on the keyboard.

---
### **Important Commands in pynput**

## **Get Help for pynput**

You can use Python’s built-in `help()` function to view the documentation for `pynput` classes and methods.

```Python
import pynput 
help(pynput) # get documentation / help for this library 
```

This will show you an overview of the `pynput` library, including all available classes and methods.

---

## **List of All Keys (in Keyboard Component)**

You can access a list of all the keys available in the keyboard component by using the `Key` class from `pynput.keyboard`. Here’s a simple way to check available keys:

```Python
from pynput.keyboard import Key  
# Print all special keys available in the keyboard component 
print(Key)
```

This will print all the special keys like `Key.enter`, `Key.space`, `Key.esc`, etc.

To check for **all keys**, including normal characters (like 'a', 'b', etc.), you can check `KeyCode`:

```Python
from pynput.keyboard import Key, KeyCode  
# Example of a common key 
print(Key.space)  # Will print: Key.space  
# Example of a normal character 
print(KeyCode.from_char('a')) # Will print: KeyCode.from_char('a')
```

---

## **Listening for Specific Keys**

You can set up a listener that only reacts to specific keys. For example, you can listen for when the **"Esc"** key is pressed to stop the program:

```Python
from pynput.keyboard import Listener, Key

def on_press(key): 
	if key == Key.esc: 
		print("Esc key pressed! Exiting...") 
		return False # Stop the listener 
		
# Start listening for keys 
with Listener(on_press=on_press) as listener: 
	listener.join()
```

---

## **Controlling the Keyboard**

You can control the keyboard by sending key presses using the `Controller` class. For example:

```Python
from pynput.keyboard import Controller  
controller = Controller()  
controller.type('Hello') # Type 'Hello' on the keyboard
controller.press(Key.enter) # Press the 'enter' key 
controller.release(Key.enter)
```

---

## **Hotkeys (Trigger actions when pressing a combination of keys)**

You can set up hotkeys to trigger actions when specific key combinations are pressed. For example, you could set up a hotkey for "Ctrl + Shift + X" to run a function:

```Python
from pynput.keyboard import Key, Listener, KeyCode
def on_press(key):
	try: 
	# Example of a hotkey for "Ctrl + Shift + X"
		if key == KeyCode.from_char('x') and controller.pressed(Key.ctrl) and controller.pressed(Key.shift):
		print("Hotkey Ctrl + Shift + X was pressed!")            
		# Perform some action here     
	except AttributeError: 
		pass  
# Start listening for hotkeys 
with Listener(on_press=on_press) as listener:     
	listener.join()
```

---

# **Keyboard — Component:**

# **1. Keyboard Controller**

The `Keyboard Controller` is used to simulate keyboard events like pressing or releasing keys programmatically.

**Usage**: You can use it to "press" or "release" keys as if a user were typing.

**Example**:

```Python
from pynput.keyboard import Controller
import time  

keyboard = Controller()  

# Press a key (like 'a') and release it 
keyboard.press('a') 

time.sleep(1)  
# Pause for 1 second 

keyboard.release('a')  

# Type a string 
keyboard.type('Hello, World!')

```

**Explanation**:

- The `Controller` object lets you simulate keyboard actions.
    
- `press('a')` simulates pressing the "a" key.
    
- `release('a')` simulates releasing the "a" key.
    
- `type('Hello, World!')` types the string just like you were typing it.
    

---

# **2. Keyboard Listener**

The `Keyboard Listener` listens to keyboard events like key presses and releases, and you can execute custom functions when these events happen.

**Usage**: You can capture what keys are being pressed and perform actions based on that.

**Example**:

```Python
from pynput.keyboard import Listener  
# Function to run when a key is pressed 
def on_press(key):     
	try:         
		print(f'Key {key.char} pressed')     
	except AttributeError:         
		print(f'Special key {key} pressed')  

# Function to run when a key is released 
def on_release(key):     
	print(f'Key {key} released')     
	if key == 'esc':  
		# Stop listener if 'esc' is pressed         
		return False  
		
# Set up the listener 
with Listener(on_press=on_press, on_release=on_release) as listener:   
	listener.join()
```

>  **==Importnat note!==**  **key.char**: This will ==return== the **character** that was ==actually typed==, based on the active layout.

**Explanation**:

- The `Listener` listens to key press and release events.
    
- The `on_press` function gets triggered whenever a key is pressed, and `on_release` gets triggered when a key is released.
    
- The listener stops when the **Escape** key (`esc`) is pressed (`return False`).

---

## **Summary of Important Classes and Methods**

- **Key**: Contains special keys like `Key.enter`, `Key.space`, etc.
    
- **KeyCode**: Represents a character key, like `KeyCode.from_char('a')`.
    
- **Controller**: Used to simulate keyboard or mouse events (e.g., `controller.type('Hello')`).
    
- **Listener**: Used to listen to keyboard or mouse events (e.g., `Listener(on_press=on_press)`).

---

# **Mouse — Component:**
# **What is ==pynput== (mouse part)?**

==pynput== is a Python library that lets you **control** and **monitor** input devices such as the **mouse and keyboard**.

For the mouse, it provides:

- **Control** → move the mouse, click, scroll
    
- **Listen** → detect mouse movements, clicks, and scrolls
    

Mouse-related functionality lives in:

```Python
from pynput import mouse
```

---

## Core Concepts (Big Picture)

There are **two main roles** in ==pynput.mouse:==

|Role|Class|Purpose|
|---|---|---|
|**Controller**|`mouse.Controller`|Actively control the mouse|
|**Listener**|`mouse.Listener`|Passively listen to mouse events|

Think of it as:

- **Controller** → _“I move/click the mouse”_
    
- **Listener** → _“I observe what the user does”_
    

---

# 1️⃣ **mouse.Controller**

Used to **programmatically control the mouse**.

### Creating a Controller

```Python
from pynput.mouse import Controller  
mouse_controller = Controller()
```

---

### Mouse Position

#### Get current position

```Python
print(mouse_controller.position) # (x, y)
```

#### Set position (absolute)

```Python
mouse_controller.position = (500, 300)
```

#### Move relative to current position

```Python
mouse_controller.move(50, -20)
```

---

# **Mouse Buttons**

Buttons are defined in:

```Python
from pynput.mouse import Button
```

Common buttons:

- ==Button.left==
    
- ==Button.right==
    
- ==Button.middle==
    

#### Click

```Python
mouse_controller.click(Button.left, 1)   # single click 
mouse_controller.click(Button.left, 2)   # double click
```

#### Press and release

```Python
mouse_controller.press(Button.left) 
mouse_controller.release(Button.left)
```

---

### Scroll Wheel

```Python
mouse_controller.scroll(dx=0, dy=2)   # scroll up 
mouse_controller.scroll(dx=0, dy=-2)  # scroll down
```

- `dx` → horizontal scroll
    
- `dy` → vertical scroll
    

---

# 2️⃣ **mouse.Listener**

Used to **listen for mouse events** (movement, clicks, scrolling).

### Creating a Listener

You define **callback functions**, then pass them to the listener.

```Python
from pynput.mouse import Listener
```

---

# **Mouse Event Callbacks**

#### 1. **on_move(x, y)**

Called when the mouse moves.

```Python
def on_move(x, y):     
	print(f"Mouse moved to ({x}, {y})")
```

---

#### 2. **on_click(x, y, button, pressed)**

Called on button press/release.

```Python
def on_click(x, y, button, pressed):     
	if pressed:         
		print(f"{button} pressed at ({x}, {y})")     
	else:         
		print(f"{button} released")
```

---

#### 3. **on_scroll(x, y, dx, dy)**

Called when scrolling.

```Python
def on_scroll(x, y, dx, dy):     
	print(f"Scrolled {'up' if dy > 0 else 'down'}")
```

---

# **Starting the Listener**

```Python
with Listener(on_move=on_move, on_click=on_click,     on_scroll=on_scroll) as listener:     
	listener.join()
```

This blocks the program until the listener stops.

---

# **Stopping the Listener**

Return `False` from any callback:

```Python
def on_click(x, y, button, pressed):     
	if not pressed:         
		return False  # stop listener
```

Or stop it manually:

**listener.stop()**

---

## 3️⃣ Threading Behavior (Important Concept)

- `Listener` runs in a **separate thread**
    
- Your main program can continue running
    
- `listener.join()` blocks until listener stops
    

You can also start it non-blocking:

```Python
listener = Listener(on_move=on_move) 
listener.start()
```

---

## 4️⃣ Typical Use Cases

|Use Case|Tool|
|---|---|
|Mouse automation|`Controller`|
|Macro recording|`Listener`|
|Game bot / GUI automation|Both|
|User behavior tracking|`Listener`|

---

## 5️⃣ Minimal Example (Controller + Listener)

```Python
from pynput.mouse import Controller, Listener, Button  
mouse_ctrl = Controller()  

def on_click(x, y, button, pressed):     
	if pressed:         
		mouse_ctrl.position = (x, y)  
		mouse_ctrl.click(Button.left)         
		return False  
		
with Listener(on_click=on_click) as listener:     
	listener.join()
```

---

## 6️⃣ Key Things to Remember

✔ `Controller` = **do actions**  
✔ `Listener` = **observe actions**  
✔ Events are handled via **callbacks**  
✔ Listener runs in a **thread**  
✔ Return `False` to stop listening

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]