## 🐍 Flask – File Handling (Quick Notes)

### 📌 Basics

- Flask can **upload, save, and serve files**.
    
- Files are accessed via `request.files`.
    
- Use `enctype="multipart/form-data"` in HTML forms.
    

---

### 📤 Uploading Files

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/upload', methods=['POST'])
def upload_file():
    file = request.files['file']   # get file
    if file:
        file.save('uploads/' + file.filename)  # save file
        return "File uploaded!"
```

---

### 🧾 Simple HTML Form

```html
<form method="POST" action="/upload" enctype="multipart/form-data">
  <input type="file" name="file">
  <input type="submit">
</form>
```

---

### 🔒 Best Practice

- Use `werkzeug.utils.secure_filename` to avoid unsafe names:
    

```python
from werkzeug.utils import secure_filename

filename = secure_filename(file.filename)
file.save('uploads/' + filename)
```

---

### 📥 Serving Files (Download / View)

```python
from flask import send_from_directory

@app.route('/files/<name>')
def get_file(name):
    return send_from_directory('uploads', name)
```

---

### ⚙️ Config (Optional)

```python
app.config['UPLOAD_FOLDER'] = 'uploads/'
app.config['MAX_CONTENT_LENGTH'] = 16 * 1024 * 1024  # 16MB limit
```

---

### ✅ Key Points

- `request.files` → access uploaded files
    
- `file.save()` → store files
    
- `secure_filename()` → safety
    
- `send_from_directory()` → serve files
    

---

💡 Keep folders like `uploads/` created beforehand.