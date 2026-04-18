## 🐍 Flask (Python) — Beginner Notes

## 📌 What is Flask?

**Flask** is a lightweight web framework for Python used to build web applications and APIs quickly. It is called a _micro-framework_ because it includes only the essentials, giving you flexibility to add what you need.

---

## ⚙️ Installation

```bash
pip install flask
```

---

## 🚀 Basic Example (Hello World)

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"

if __name__ == "__main__":
    app.run(debug=True)
```

---

## 🌐 Routing

Routes map URLs to Python functions.

```python
@app.route("/about")
def about():
    return "About page"
```

### Dynamic Routes:

```python
@app.route("/user/<name>")
def user(name):
    return f"Hello, {name}"
```

---

## 📥 Request Handling

```python
from flask import request

@app.route("/login", methods=["POST"])
def login():
    username = request.form["username"]
    return f"Welcome {username}"
```

---

## 📤 Returning Responses

```python
from flask import jsonify

@app.route("/api")
def api():
    return jsonify({"message": "Hello, API"})
```

---

## 🧩 Templates (Jinja2)

```python
from flask import render_template

@app.route("/")
def home():
    return render_template("index.html", name="Alice")
```

---

## 📁 Project Structure

```
project/
│
├── app.py
├── templates/
├── static/
```

---