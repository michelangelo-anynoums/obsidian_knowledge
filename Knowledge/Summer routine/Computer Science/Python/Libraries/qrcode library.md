## What is the `qrcode` library?

The **qrcode** library is a simple and popular Python package for **generating QR codes**.  
You can use it to encode text, URLs, contact info, Wi-Fi credentials, or any data that fits into a QR code and export it as an image.

It’s built on top of **Pillow (PIL)** for image handling, which means you can easily customize size, colors, and formats.

---

## Installation

First, install the library (and Pillow, if needed):

```Python
pip install qrcode[pil] # or just 'pip install qrcode'
```

---

## Basic Concept

At its core, the workflow is:

1. Provide some data (string)
    
2. Generate a QR code
    
3. Save or display the image
    

---

## Simplest Example (One-liner style)

```Python
import qrcode

img = qrcode.make("https://www.example.com") 
img.save("example_qr.png")
```

✔️ This automatically:

- Chooses QR version and size
    
- Uses black & white colors
    
- Saves the QR as a PNG image
    

Great for quick use cases.

---

## More Control with `QRCode` Class

For real projects, you’ll usually want more control.

```Python
import qrcode

qr = qrcode.QRCode(
	version=1,  # controls size (1 is smallest)     
	error_correction=qrcode.constants.ERROR_CORRECT_L, 
	box_size=10,  # pixels per box     
	border=4,  # quiet zone (minimum is 4) 
)  

qr.add_data("Hello, QR Code!") # URL
qr.make(fit=True)  

img = qr.make_image(fill_color="black", back_color="white") 
img.save("hello_qr.png")
```

---

## Key Concepts You Should Know

### 1. **Version**

- Controls the **size** of the QR code
    
- Ranges from `1` (smallest) to `40` (largest)
    
- Higher version = more data capacity
    

`version=1`

---

### 2. **Error Correction**

Allows QR codes to be readable even if damaged.

Common options:

- `ERROR_CORRECT_L` → ~7% recovery
    
- `ERROR_CORRECT_M` → ~15%
    
- `ERROR_CORRECT_Q` → ~25%
    
- `ERROR_CORRECT_H` → ~30%
    

```Python
error_correction=qrcode.constants.ERROR_CORRECT_H
```

Use higher levels for logos or printing.

---

### 3. **Box Size**

Controls how big each square (“box”) is in pixels.

`box_size=10`

Larger = higher resolution image.

---

### 4. **Border**

The “quiet zone” around the QR code.

`border=4`

⚠️ Minimum recommended is **4**, otherwise scanners may fail.

---

### 5. **Colors**

You can customize foreground and background colors:

```Python
img = qr.make_image(fill_color="blue", back_color="white")
```

You can even use RGB tuples:

`fill_color=(0, 0, 0)`

---

## Encoding Different Types of Data

### URL

```Python
qr.add_data("https://github.com")
```

### Plain text

```Python
qr.add_data("Hello world")
```

### Wi-Fi (common pattern)

```Python
qr.add_data("WIFI:T:WPA;S:MyNetwork;P:MyPassword;;")
```
## Pro Tip: Build It Safely in Code

To avoid typos:

```Python
ssid = "MyNetwork" 
password = "MyPassword" 
security = "WPA"  

wifi_string = f"WIFI:T:{security};S:{ssid};P:{password};;" 

qr.add_data(wifi_string)
```

---

## Output Formats

Since it uses Pillow, you can save as:

- PNG
    
- JPG
    
- BMP
    
- etc.
    

```Python
img.save("qr_code.jpg")
```

---

## When to Use `qrcode`

✔️ Generating QR codes  
✔️ Simple customization  
✔️ Static data encoding

❌ Not for scanning QR codes (use `opencv`, `pyzbar`, etc. for that)

----

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]