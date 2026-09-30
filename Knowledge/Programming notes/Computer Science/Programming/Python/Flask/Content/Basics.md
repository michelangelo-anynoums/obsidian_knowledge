## 🧪 Flask — Basic Notes (Practical)

---

### ⚙️ App Setup

```python
from flask import Flask

app = Flask(__name__)
```

---

### 🔀 Routes

```python
@app.route("/")
def home():
    return "Hello World"
```

- Dynamic route:
    

```python
@app.route("/user/<name>")
def user(name):
    return f"Hello {name}"
```

---

### ▶️ Run App

```python
if __name__ == "__main__":
    app.run(debug=True)
```

---

### ⚙️ Configuration (IMPORTANT)

#### 1. Basic Config

```python
app.config["DEBUG"] = True
app.config["SECRET_KEY"] = "mysecret"
```

#### 2. Load from File

```python
app.config.from_pyfile("config.py")
```

**config.py**

```python
DEBUG = True
SECRET_KEY = "mysecret"
```

#### 3. Load from Environment

```python
import os
app.config["SECRET_KEY"] = os.getenv("SECRET_KEY")
```

---

### 📥 Request Data

```python
from flask import request

@app.route("/login", methods=["POST"])
def login():
    username = request.form["username"]
    return username
```

---

### 📤 Responses (JSON)

```python
from flask import jsonify

@app.route("/api")
def api():
    return jsonify({"message": "ok"})
```

---

### 📄 Templates (HTML)

```python
from flask import render_template

@app.route("/page")
def page():
    return render_template("index.html")
```

- Folder: `/templates/index.html`
    

---

### 🎨 Static Files

- Folder: `/static/`
    
- Example: `/static/style.css`
    

---

### 🧩 Project Structure

```
project/
│
├── app.py
├── config.py
├── templates/
│   └── index.html
└── static/
    └── style.css
```

---

### 🧪 Minimal Example

```python
from flask import Flask, jsonify

app = Flask(__name__)

app.config["DEBUG"] = True

@app.route("/")
def home():
    return "Welcome"

@app.route("/api")
def api():
    return jsonify({"status": "ok"})

if __name__ == "__main__":
    app.run()
```

---

### ✅ Essentials to Remember

- `app = Flask(__name__)`
    
- `@app.route()` → define endpoints
    
- `app.config` → manage settings
    
- `request` → incoming data
    
- `jsonify()` → API responses
    
- `templates/` + `static/` → frontend
    

---