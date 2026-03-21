---

---

## 🌈 Introduction to the **rich** Library

**Rich** is a Python library for **rich text and formatting in the terminal**.  
It helps you display:

- Colored and styled text
    
- Tables
    
- Progress bars
    
- Syntax-highlighted code
    
- Tracebacks (better error messages)
    
- Trees (hierarchical data)
    

📦 Install it first:

```Python
pip install rich
```

---

## 1️⃣ The **Console** – the heart of Rich

Almost everything in Rich goes through a **Console** object.

```Python
from rich.console import Console  
console = Console() 
console.print("Hello, [bold magenta]Rich[/bold magenta]!")
```

### Why **console.print()** instead of **print()**?

- Supports **colors**, **styles**, **emoji**
    
- Automatically adapts to terminal width
    
- Can print Rich objects (tables, trees, panels, etc.)
    

---

## 2️⃣ Text Styling & Markup

Rich uses **BBCode-like markup** inside strings.

```Python
console.print("[bold]Bold[/bold]") 
console.print("[italic]Italic[/italic]") 
console.print("[underline]Underline[/underline]") 
console.print("[red]Red text[/red]") 
console.print("[green]Success![/green] ✅")
```

### Combine styles

```Python
console.print("[bold blue]Important message[/bold blue]")
```

---

## 3️⃣ **Text** object (when you need more control)

Use `Text` when you want to **style parts programmatically**.

```Python
from rich.text import Text  

text = Text("Hello World") 
text.stylize("bold magenta", 0, 5) 
console.print(text)
```

Use this when:

- Styling depends on logic
    
- You don’t want inline markup strings
    

---

## 4️⃣ Tables

Tables are one of Rich’s killer features.

```Python
from rich.table import Table  

table = Table(title="Users")  
table.add_column("Name", style="cyan") 
table.add_column("Age", justify="right") 
table.add_column("Role", style="green")  
table.add_row("Alice", "24", "Admin") 
table.add_row("Bob", "30", "User")  
console.print(table)
```

💡 Great for:

- CLI tools
    
- Debugging structured data
    
- Reports
    

---

## 5️⃣ Pretty Tracebacks (Errors)

Rich can replace Python’s ugly tracebacks with readable ones.

```Python
from rich.traceback import install 
install()  

def crash():     
	return 1 / 0  
	
crash()
```

✔ Colored  
✔ Shows local variables  
✔ Much easier to debug

---

## 6️⃣ Progress Bars

```Python
from rich.progress import track 
import time  

for i in track(range(10), description="Processing..."):     
	time.sleep(0.5)
```

You get:

- Percentage
    
- Elapsed time
    
- Smooth animations
    

---

## 🌳 **Trees in Rich**

Trees are used to display **hierarchical structures** (folders, data, dependencies).

---

## 7️⃣ Basic Tree

```Python
from rich.tree import Tree  

tree = Tree("🌍 World")  
tree.add("🌎 America") 
tree.add("🌍 Europe") 
tree.add("🌏 Asia")

console.print(tree)
```

---

## 8️⃣ Nested Trees

```Python
tree = Tree("📁 Project")  

src = tree.add("📂 src") 
src.add("main.py") 
src.add("utils.py")  
tests = tree.add("📂 tests") 
tests.add("test_main.py")  

console.print(tree)
```

Perfect for:

- File structures
    
- Dependency graphs
    
- Menu systems
    

---

## 9️⃣ Styled Trees

```Python
tree = Tree("[bold blue]Languages[/bold blue]")  

python = tree.add("[green]Python[/green]") 
python.add("Django") 
python.add("FastAPI")  
js = tree.add("[yellow]JavaScript[/yellow]") 
js.add("React") 
js.add("Vue")  

console.print(tree)
```

Trees support:

- Colors
    
- Emojis
    
- Any Rich renderable (tables, text, panels)
    

---

## 🔟 Tree with Dynamic Data

```Python
data = { "Fruits": ["Apple", "Banana"],     
		 "Vegetables": ["Carrot", "Potato"] }  
		 
tree = Tree("🛒 Shop")  

for category, items in data.items():     
	branch = tree.add(category)     
	for item in items:         
		branch.add(item)  

console.print(tree)
```

----

Rich’s `Console` object has a built-in `clear()` method:

```Python
from rich.console import Console  

console = Console() 
console.clear()
```

That’s it. This works across platforms (Windows, macOS, Linux) and plays nicely with Rich’s rendering.

---

## ✅ When to Use Rich

Use Rich when you want:

- Clean CLI output
    
- Better debugging
    
- Professional-looking terminal tools
    
- More joy while coding 😄

----

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]