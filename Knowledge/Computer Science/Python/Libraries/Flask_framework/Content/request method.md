### Deep Dive: `request` in Flask

`request` is a global object in Flask that represents the **incoming HTTP request** sent by the client (browser, API call, etc.).  
It lets you access form data, query parameters, headers, files, and more.

---

## Basic Usage

```python
from flask import request

@app.route("/hello")
def hello():
    user_agent = request.headers.get("User-Agent")
    return f"Your browser is {user_agent}"
```

---

## What is `request` Internally?

- It’s a **context-local object** (you don’t pass it around; Flask provides it automatically).
    
- It only exists during an active request.
    
- Built on top of Werkzeug’s request system.
    

---

## Most Important Attributes & Methods

---

### 1. `request.method`

Returns the HTTP method used.

```python
@app.route("/submit", methods=["GET", "POST"])
def submit():
    if request.method == "POST":
        return "Form submitted"
    return "Show form"
```

---

### 2. `request.args` (Query Parameters)

Access data from the URL query string.

Example: `/search?q=flask`

```python
@app.route("/search")
def search():
    query = request.args.get("q")
    return f"Searching for {query}"
```

- Type: Immutable dictionary
    
- Use `.get()` to avoid errors
    

---

### 3. `request.form` (Form Data)

Access data sent via HTML forms (POST).

```python
@app.route("/login", methods=["POST"])
def login():
    username = request.form.get("username")
    password = request.form.get("password")
    return f"User: {username}"
```

---

### 4. `request.json` (JSON Body)

Used when client sends JSON data.

```python
@app.route("/api/user", methods=["POST"])
def create_user():
    data = request.json
    return f"Name: {data['name']}"
```

---

### 5. `request.files` (File Uploads)

Handles uploaded files.

```python
@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["file"]
    file.save("uploaded_file.txt")
    return "File uploaded"
```

---

### 6. `request.headers`

Access HTTP headers.

```python
@app.route("/")
def index():
    auth = request.headers.get("Authorization")
    return f"Auth header: {auth}"
```

---

### 7. `request.cookies`

Access cookies sent by the client.

```python
@app.route("/")
def home():
    user = request.cookies.get("user")
    return f"Welcome {user}"
```

---

### 8. `request.path` & `request.url`

Information about the request URL.

```python
@app.route("/info")
def info():
    return f"Path: {request.path}, Full URL: {request.url}"
```

---

### 9. `request.remote_addr`

Client’s IP address.

```python
@app.route("/")
def ip():
    return f"Your IP: {request.remote_addr}"
```

---

### 10. `request.get_json()`

Safer way to parse JSON.

```python
@app.route("/data", methods=["POST"])
def data():
    data = request.get_json()
    return data["key"]
```

---

## Combined Example

```python
from flask import Flask, request

app = Flask(__name__)

@app.route("/submit", methods=["GET", "POST"])
def submit():
    if request.method == "POST":
        name = request.form.get("name")
        return f"Hello {name}"
    
    query = request.args.get("q", "nothing")
    return f"Query: {query}"
```

---

## Common Pitfalls

- Accessing `request` **outside a route** → ❌ error (no request context)
    
- Using `request.form` for JSON → ❌ use `request.json` or `get_json()`
    
- Not validating input → ⚠️ security risk
    

---

## Mental Model

Think of `request` as:

> “Everything the client just sent to your server.”

---

## Quick Summary

- `request.method` → GET, POST, etc.
    
- `request.args` → URL query params
    
- `request.form` → form data
    
- `request.json` → JSON body
    
- `request.files` → uploaded files
    
- `request.headers` → metadata
    
- `request.cookies` → client storage
    

---

Mastering `request` lets you properly **receive and handle user input**, which is at the heart of any web app.