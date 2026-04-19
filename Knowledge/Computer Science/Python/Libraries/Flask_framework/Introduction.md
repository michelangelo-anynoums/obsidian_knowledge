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

## **Essential Flask Components & Functions (with short examples)**

---

### 1. Flask (Core App)

The main class used to create your application.

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"
```

---

### 2. route (URL Mapping)

Defines which function runs for a given URL.

```python
@app.route("/about")
def about():
    return "About page"
```

---

### 3. request (Handling Client Data)

Used to access incoming request data (forms, query params, headers).

```python
from flask import request

@app.route("/greet", methods=["POST"])
def greet():
    name = request.form.get("name")
    return f"Hello {name}"
```

---

### 4. render_template (HTML Rendering)

Renders HTML files using Jinja2 templates.

```python
from flask import render_template

@app.route("/profile")
def profile():
    return render_template("profile.html", username="Alex")
```

---

### 5. url_for (Dynamic URL Building)

Generates URLs instead of hardcoding them.

```python
from flask import url_for

@app.route("/")
def home():
    return url_for("about")  # returns "/about"
```

---

### 6. redirect (Page Redirection)

Redirects users to another route.

```python
from flask import redirect, url_for

@app.route("/login")
def login():
    return redirect(url_for("home"))
```

---

### 7. session (User Sessions)

Stores user-specific data between requests (uses cookies).

```python
from flask import session

app.secret_key = "secret123"

@app.route("/set")
def set_session():
    session["user"] = "Alex"
    return "Session set"
```

---

### 8. jsonify (JSON Responses)

Converts Python data into JSON (useful for APIs).

```python
from flask import jsonify

@app.route("/api")
def api():
    return jsonify({"name": "Alex", "age": 25})
```

---

### 9. abort (Error Handling)

Stops execution and returns an HTTP error.

```python
from flask import abort

@app.route("/secret")
def secret():
    abort(403)  # Forbidden
```

---

### 10. flash (User Messages)

Displays temporary messages to users (often used with templates).

```python
from flask import flash

@app.route("/submit")
def submit():
    flash("Form submitted successfully!")
    return "Done"
```

---

### 11. Blueprint (App Organization)

Helps split large apps into smaller modules.

```python
from flask import Blueprint

main = Blueprint("main", __name__)

@main.route("/")
def home():
    return "Blueprint home"
```

---

### 12. g (Global Request Object)

Stores data during a single request lifecycle.

```python
from flask import g

@app.before_request
def before():
    g.user = "Alex"
```

---

### 13. make_response (Custom Responses)

Lets you modify response objects (headers, cookies, etc.).

```python
from flask import make_response

@app.route("/")
def home():
    res = make_response("Hello")
    res.set_cookie("user", "Alex")
    return res
```

---

### 14. send_file / send_from_directory (File Serving)

Used to send files to users.

```python
from flask import send_file

@app.route("/download")
def download():
    return send_file("example.pdf")
```

---

### 15. before_request / after_request (Hooks)

Run logic before or after each request.

```python
@app.before_request
def before():
    print("Before request")

@app.after_request
def after(response):
    print("After request")
    return response
```

---

### Quick Summary

These are the “core toolkit” pieces you’ll use constantly:

- App creation → Flask
    
- Routing → route
    
- Requests → request
    
- Responses → render_template, jsonify
    
- Navigation → redirect, url_for
    
- State → session
    
- Structure → Blueprint
    

---

### Deep Dive: `@app.route()` in Flask

The `route()` decorator is one of the most important parts of Flask. It connects a URL (like `/home`) to a Python function (called a _view function_).

---

## Basic Syntax

```python
@app.route("/path", methods=["GET"])
def my_view():
    return "Hello"
```

---

## Full Signature (Simplified)

```python
@app.route(
    rule,
    endpoint=None,
    methods=None,
    defaults=None,
    strict_slashes=None
)
```

---

## Parameter Breakdown

### 1. `rule` (REQUIRED)

The URL pattern.

```python
@app.route("/about")
def about():
    return "About page"
```

You can also use dynamic values:

```python
@app.route("/user/<name>")
def user(name):
    return f"Hello {name}"
```

**Converters (type casting):**

```python
@app.route("/post/<int:id>")
def post(id):
    return f"Post {id}"
```

Common converters:

- `string` (default)
    
- `int`
    
- `float`
    
- `path` (accepts slashes)
    
- `uuid`
    

---

### 2. `endpoint` (OPTIONAL)

The internal name of the route (defaults to function name).

```python
@app.route("/home", endpoint="main_home")
def home():
    return "Home"
```

Used with `url_for()`:

```python
url_for("main_home")
```

---

### 3. `methods` (OPTIONAL)

Specifies allowed HTTP methods.

Default: `["GET"]`

```python
@app.route("/submit", methods=["GET", "POST"])
def submit():
    if request.method == "POST":
        return "Form submitted"
    return "Show form"
```

---

### 4. `defaults` (OPTIONAL)

Provides default values for route variables.

```python
@app.route("/page/", defaults={"page": 1})
@app.route("/page/<int:page>")
def show_page(page):
    return f"Page {page}"
```

- `/page/` → page = 1
    
- `/page/3` → page = 3
    

---

### 5. `strict_slashes` (OPTIONAL)

Controls whether trailing slashes matter.

```python
@app.route("/about", strict_slashes=False)
def about():
    return "About"
```

- `True` (default): `/about` ≠ `/about/`
    
- `False`: both work
    

---

## Important Behaviors

### Multiple Routes for One Function

```python
@app.route("/")
@app.route("/home")
def home():
    return "Home page"
```

---

### Methods Shortcut Decorators

Flask also provides shortcuts:

```python
@app.get("/data")
def get_data():
    return "GET request"

@app.post("/data")
def post_data():
    return "POST request"
```

---

### URL Building Connection

Every route is tied to `url_for()`:

```python
url_for("home")  # Uses function name as endpoint
```

---

## Real Example Combining Everything

```python
from flask import Flask, request

app = Flask(__name__)

@app.route(
    "/product/<int:id>",
    methods=["GET", "POST"],
    endpoint="product_detail",
    strict_slashes=False
)
def product(id):
    if request.method == "POST":
        return f"Updated product {id}"
    return f"Viewing product {id}"
```

---

## Mental Model

Think of `route()` as:

> “When a user visits THIS URL with THESE methods → run THIS function.”

---

## Quick Summary

- `rule` → URL pattern (**required**)
    
- `methods` → HTTP methods (GET, POST, etc.)
    
- `endpoint` → internal name for `url_for`
    
- `defaults` → fallback values for variables
    
- `strict_slashes` → trailing slash behavior
    

---

Mastering `route()` is key—almost everything in Flask builds on top of it.

---
### Recommended Tools & Resources

|   |   |
|---|---|
|Category|Tools/Libraries|
|**Core**|Flask, Werkzeug, Jinja2|
|**Database**|Flask-SQLAlchemy, Flask-Migrate, SQLite|
|**Forms/Auth**|Flask-WTF, Flask-Login, Werkzeug Security|
|**APIs**|Flask-RESTful, Requests|
|**Testing**|Pytest|
|**Deployment**|Gunicorn, Docker, GitHub Actions|
|**Learning**|Official Flask Docs, Real Python, Coursera Roadmap|