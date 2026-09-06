# 🐍 **Python ==os== Library — Introduction**

The ==**os library**==in Python provides a way to interact with the **operating system**.  
It allows you to work with **files and directories**, **environment variables**, and **system paths** in a platform-independent way ==(Windows, macOS, Linux).==

The **==os==** module is commonly used for:

- File and folder management
    
- Path handling
    
- Checking file existence
    
- Reading environment variables
    
- Running system-level operations
    

---

# **Importing the Library**

```Python
import os
```

---

## 📂 Working with Directories

### Get Current Working Directory

```Python
os.getcwd() # outputs current working directory
```

### Change Directory

```Python
os.chdir("path/to/folder") # change working directory
```

### List Files in a Directory

```Python
os.listdir(".")  # current directory
```

---

## 📁 Creating and Removing Directories

## **Create a Directory**

```Python
os.mkdir("new_folder") # make a new folder in current directory 
```

## **Create Nested Directories**

```Python
os.makedirs("parent/child") # make folder in a new folder
```

## **Remove a Directory**

```Python
os.rmdir("empty_folder") # remove a folder/directory
```

---

## 📄 Working with Files

## **Check if File or Folder Exists**

```Python
os.path.exists("file.txt") # check if directory exists
```

## **Check File or Directory**

```Python
os.path.isfile("file.txt") # check if this is a file type
os.path.isdir("folder") # check if this is a folder/directory type
```

## **Rename File or Folder**

```Python
os.rename("old.txt", "new.txt") # 1 param: current name; 2 param: new name
```

## **Delete a File**

```Python
os.remove("file.txt") # remove a file
```

---

## 🛣️ Path Handling ==os.path==

## **Join Paths (Recommended)**

```Python 
os.path.join("folder", "file.txt") # join two directories
```

## **Get File Name and Directory**

```Python
os.path.basename("/path/file.txt") # outputs "file.txt"
os.path.dirname("/path/file.txt") # outputs "path"
```

## **Get File Extension**

```Python
name, extension = os.path.splitext("file.txt") # returns name and extension
```

---

## 🌱 Environment Variables

## **Get Environment Variable**

```Python
os.environ.get("HOME") # home directory
```

## **Set Environment Variable**

```Python
os.environ["MY_VAR"] = "123" # create a new environment variable
```

## ⚙️ **Running System Commands**

```Python
os.system("ls") # macOS/Linux 
os.system("dir") # Windows
```

> ⚠️ For modern code, `subprocess` is usually preferred over `os.system`.

----
### Using **os.walk()** (most common & powerful)

`os.walk()` recursively walks through all directories and files.

```Python
import os

root_dir = "project"  

for root, dirs, files in os.walk(root_dir): 
    print("Current directory:", root)     
    for file in files:         
	    file_path = os.path.join(root, file)     
	    print(file_path)
```

This gives you:

- `root` → current directory path
    
- `dirs` → subdirectories inside `root`
    
- `files` → files inside `root`
---

## ⭐ **Most Important Concepts (Summary)**

- `os.getcwd()` → current directory
    
- `os.listdir()` → list files
    
- `os.mkdir()` / `os.makedirs()` → create folders
    
- `os.remove()` → delete files
    
- `os.path.join()` → safe path creation
    
- `os.path.exists()` → check existence
    
- `os.environ` → environment variables


---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]