## What is JSON?

**JSON (JavaScript Object Notation)** is a lightweight data format used to store and exchange data.  
It’s human-readable and language-independent, which makes it super common in APIs, configuration files, and data storage.

Example JSON:

```Python
{   
	"name": "Alice",   
	"age": 30,   
	"is_student": false,   
	"skills": ["Python", "Data Analysis"] 
}
```

---

## The `json` Module in Python

Python’s built-in **json** module lets you:

- Convert Python objects → JSON (**serialize**)
    
- Convert JSON → Python objects (**deserialize**)
    

First, import it:

```Python
import json
```

---

## Python ↔ JSON Mapping

|Python type|JSON type|
|---|---|
|dict|object|
|list|array|
|str|string|
|int/float|number|
|True/False|true/false|
|None|null|

---

## Example 1: Convert Python → JSON (**json.dumps**)

```Python
data = {     
	"name": "Alice",     
	"age": 30,     
	"is_student": False,     
	"skills": ["Python", "ML"] 
}  
	
json_string = json.dumps(data) 
print(json_string)
```

**Output:**

```Python
{"name": "Alice", "age": 30, "is_student": false, "skills": ["Python", "ML"]}
```

👉 Tip: Make it pretty (great for debugging):

```Python
json.dumps(data, indent=4)
```

---

## Example 2: Convert JSON → Python (**json.loads**)

```Python
json_string = '{"name": "Bob", "age": 25}'  

python_data = json.loads(json_string) 
print(python_data) 
print(type(python_data))
```

**Output:**

```Python
{'name': 'Bob', 'age': 25} <class 'dict'>
```

---

## Example 3: Write JSON to a File (**json.dump**)

```Python
data = {"project": "JSON tutorial", "version": 1}  

with open("data.json", "w") as f:     
	json.dump(data, f, indent=4)
```

This creates a file called `data.json`.

---

## Example 4: Read JSON from a File (**json.load**)

```Python
with open("data.json", "r") as f:     
	data = json.load(f)  
	print(data)
```

---

## When Do You Use Each Function?

|Function|Use case|
|---|---|
|`json.dumps()`|Python → JSON string|
|`json.loads()`|JSON string → Python|
|`json.dump()`|Python → JSON file|
|`json.load()`|JSON file → Python|

---

## Common Gotchas 🚨

- JSON **must use double quotes** (`"`) for strings
    
- Python objects like `set` or `tuple` are **not JSON-serializable**
    
- JSON has no comments

----


Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]