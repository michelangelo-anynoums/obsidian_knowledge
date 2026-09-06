### Simple Guide: File Handling in Flask (Uploads & Downloads)

Think of file handling in Flask as two main things:

> **1. Receiving files from users (uploads)**  
> **2. Sending files back to users (downloads)**

---

## 1. Uploading Files (User → Server)

### How it works (in plain words)

- The user selects a file in a form
    
- The browser sends it to your Flask app
    
- Flask lets you access it via `request.files`
    
- You save it somewhere on your server
    

---

### Minimal Example

```python
from flask import request

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["file"]
    file.save("myfile.txt")
    return "Uploaded!"
```

---

### What’s happening here?

- `request.files` → contains uploaded files
    
- `"file"` → must match the `<input name="file">` in HTML
    
- `file.save(...)` → stores the file on your server
    

---

### Important Concepts (Keep it simple)

**File object**

- Not just raw data—it has useful properties:
    
    - `file.filename` → original name
        
    - `file.content_type` → type (e.g., image/png)
        

---

### Very Important: Safety Basics ⚠️

- Never trust file names directly
    
- Always control where files are saved
    
- Optionally restrict file types (e.g., only `.jpg`, `.pdf`)
    

Simple idea:

```python
if file.filename.endswith(".jpg"):
    file.save("uploads/image.jpg")
```

---

## 2. Downloading Files (Server → User)

### How it works

- You already have a file on your server
    
- Flask sends it to the user
    

---

### Minimal Example

```python
from flask import send_file

@app.route("/download")
def download():
    return send_file("myfile.txt")
```

---

### What’s happening?

- `send_file()` → sends a file as a response
    
- The browser will either display it or download it
    

---

### Optional: Force Download

```python
return send_file("myfile.txt", as_attachment=True)
```

- This makes the browser download instead of opening it
    

---

## 3. Better Organization (Good Practice)

Instead of saving files randomly:

- Create a folder like `/uploads`
    
- Save files there
    

```python
file.save("uploads/" + file.filename)
```

---

## 4. Common Mistakes (Easy to Avoid)

- ❌ Forgetting `methods=["POST"]` → upload won’t work
    
- ❌ Using wrong input name → `request.files["file"]` fails
    
- ❌ Saving files without checking type → security risk
    
- ❌ Overwriting files with same name
    

---

## 5. Mental Model

Think of it like this:

- `request.files` → “What the user gave me”
    
- `file.save()` → “Store it on my computer”
    
- `send_file()` → “Give a file back to the user”
    

---

## 6. Tiny Real Example Flow

1. User uploads `photo.jpg`
    
2. Flask receives it
    
3. You save it in `/uploads`
    
4. Later, user downloads it
    

---

## Final Takeaway

You only need to remember 3 things:

- `request.files` → get the file
    
- `file.save()` → store it
    
- `send_file()` → send it back
    

That’s the core of file handling in Flask.

---