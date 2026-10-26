## 🌈 What is Colorama?

**Colorama** is a Python library that makes it easy to add **colored text and text styles** (like bold or bright) to terminal/console applications. It works on **Windows, macOS, and Linux**, and helps ensure colors display correctly, especially on Windows.

---

## 📦 How to Install Colorama

Use `pip` to install it:

`pip install colorama`

After installing, initialize it in your Python script like this:

```Python
from colorama import init # import colorama
init()
```

### **For reference:** [colorama website](https://pypi.org/project/colorama/)

---

## ⭐ Most Important Features

- **Cross-platform color support** (works on Windows and Unix terminals)
    
- Easy-to-use color **foregrounds** (text colors)
    
- **Background colors** for text
    
- Text **styles** like bright, dim, and reset
    
- Simple and readable syntax
    

Example of basic usage:

```Python
from colorama import init, Fore, Style # import colorama
init()  
print(Fore.RED + "This text is red!") 
print(Fore.GREEN + "This text is green!") 
print(Style.RESET_ALL + "Back to normal text") # reset to default
```

### **init(autoreset=False):**

>If you find yourself repeatedly sending reset sequences to turn off color changes at the end of every print, then ==init(autoreset=True)== will automate that:

```Python
from colorama import init, Fore, Style
init(autoreset=True)
print(Fore.RED + 'some red text')
print('automatically back to default color again')
```

## **Styles for colorama library**

>==**Fore:**== BLACK, RED, GREEN, YELLOW, BLUE, MAGENTA, CYAN, WHITE, RESET.
**==Back:==** BLACK, RED, GREEN, YELLOW, BLUE, MAGENTA, CYAN, WHITE, RESET.
==**Style:**== DIM, NORMAL, BRIGHT, RESET_ALL


---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]