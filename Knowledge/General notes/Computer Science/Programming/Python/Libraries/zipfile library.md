## Python **zipfile** Library — Easy Introduction

### What is **zipfile**?

The **zipfile** library is a built-in Python module used to **create, read, extract, and manage ZIP files** (compressed files).

You **do not need to install it** — it comes with Python.

```Python
import zipfile
```

---

## Main Uses of **zipfile**

- Create ZIP files
    
- Add files to a ZIP
    
- Read files inside a ZIP
    
- Extract ZIP files
    
- List files inside a ZIP
    

---

## Important Concepts & Commands

### 1. Creating a ZIP File

Use **write mode ('w')** to create a new ZIP file.

```Python
import zipfile  

with zipfile.ZipFile("myfiles.zip", "w") as zipf:     
	zipf.write("file1.txt")     
	zipf.write("file2.txt")
```

✅ Creates `myfiles.zip`  
⚠️ `'w'` overwrites the ZIP if it already exists

---

### 2. Adding Files to an Existing ZIP

Use **append mode ('a')**.

```Python
with zipfile.ZipFile("myfiles.zip", "a") as zipf:   
	zipf.write("file3.txt")
```

---

### 3. Listing Files Inside a ZIP

Use **namelist()**.

```Python
with zipfile.ZipFile("myfiles.zip", "r") as zipf:  
	print(zipf.namelist())
```

Output example:

```Python
['file1.txt', 'file2.txt', 'file3.txt']
```

---

### 4. Extracting All Files

Use **extractall()**.

```Python
with zipfile.ZipFile("myfiles.zip", "r") as zipf:     
	zipf.extractall("output_folder")
```

✅ Extracts all files into **output_folder**

---

### 5. Extracting a Single File

```Python
with zipfile.ZipFile("myfiles.zip", "r") as zipf:
	zipf.extract("file1.txt")
```

---

### 6. Reading a File Inside a ZIP (Without Extracting)

```Python
with zipfile.ZipFile("myfiles.zip", "r") as zipf:     
	with zipf.open("file1.txt") as file:         
		content = file.read()         
		print(content.decode())
```

---

### 7. Compression Types (Optional but Important)

To compress files, use **ZIP_DEFLATED**.

```Python
with zipfile.ZipFile("compressed.zip", "w", zipfile.ZIP_DEFLATED) as zipf:     
	zipf.write("file1.txt")
```

---

## Common ZipFile Modes

|Mode|Meaning|
|---|---|
|`'r'`|Read ZIP|
|`'w'`|Write (overwrite)|
|`'a'`|Append|
|`'x'`|Create (error if exists)|

---

## Key Class

- **zipfile.ZipFile** → main class to work with ZIP files
----

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]