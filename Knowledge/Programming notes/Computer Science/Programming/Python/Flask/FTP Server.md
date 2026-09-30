# Mini Project Note — Flask LAN File Server

## 1. What are we building?

A small **HTTP file server** using Python and Flask.

```text
📱 Phone
   │
   │ HTTP over Wi-Fi
   ▼
💻 Laptop
   │
   └── Flask
       │
       ▼
    shared/
```

The phone can connect to the laptop through the local network and upload files into the `shared` folder.

---

## 2. Project structure

```text
LAN_Server/
│
├── venv/
├── server.py
└── shared/
```

- `venv/` → isolated Python environment
- `server.py` → our Flask server
- `shared/` → uploaded files

---

## 3. Important libraries

```python
from flask import Flask, request, send_from_directory
import os
```

### `Flask`

Creates our web application.

```python
app = Flask(__name__)
```

### `request`

Lets Flask access information sent by the browser.

For file uploads:

```python
request.files
```

### `os`

Lets Python work with the operating system:

```python
os.path.exists()
os.mkdir()
os.listdir()
os.path.join()
```

---

## 4. Creating the shared folder

```python
folder = "shared"

if not os.path.exists(folder):
    os.mkdir(folder)
```

This means:

> If the `shared` folder doesn't exist, create it.

---

## 5. `GET /` — displaying the webpage

```python
@app.route("/")
def index():
    ...
```

When the phone visits:

```text
http://LAPTOP-IP:8080/
```

the browser sends:

```text
GET /
```

Flask responds with our HTML page.

---

## 6. The upload form

```html
<form method="POST"
      action="/upload"
      enctype="multipart/form-data">

    <input type="file" name="file">

    <button type="submit">
        Submit
    </button>

</form>
```

The important parts are:

```text
method="POST"
```

We're **sending data**.

```text
action="/upload"
```

Send the data to the `/upload` route.

```text
enctype="multipart/form-data"
```

We're sending a file.

And:

```html
name="file"
```

gives the uploaded file the name `"file"`.

---

# 7. `POST /upload` — receiving the file

This is the main upload function:

```python
@app.route("/upload", methods=["POST"])
def upload():

    file = request.files["file"]

    path = os.path.join(folder, file.filename)

    file.save(path)

    return "<h1>Success!</h1>"
```

Let's understand it line by line.

### Route

```python
@app.route("/upload", methods=["POST"])
```

This tells Flask:

> When a `POST` request arrives at `/upload`, run `upload()`.

The browser sends:

```text
POST /upload
```

---

### Get the file

```python
file = request.files["file"]
```

Flask looks inside the HTTP request for the uploaded file named `"file"`.

Remember:

```html
<input type="file" name="file">
```

matches:

```python
request.files["file"]
```

---

### Create the destination path

```python
path = os.path.join(folder, file.filename)
```

For example:

```text
folder       = shared
filename     = photo.jpg

             ↓

shared/photo.jpg
```

---

### Save the file

```python
file.save(path)
```

This writes the uploaded file to the laptop's disk.

So:

```text
📱 photo.jpg
      │
      │ POST /upload
      ▼
   Flask
      │
      │ file.save(...)
      ▼
💻 shared/photo.jpg
```

---

### Respond to the phone

```python
return "<h1>Success!</h1>"
```

Flask sends an HTTP response back to the browser.

The phone then displays:

```text
Success!
```

---

# 8. Complete upload flow

The whole process is:

```text
📱 PHONE

Select photo.jpg
       │
       ▼
<input type="file" name="file">
       │
       ▼
POST /upload
       │
       │ HTTP
       ▼
💻 FLASK

request.files["file"]
       │
       ▼
file
       │
       ▼
os.path.join("shared", file.filename)
       │
       ▼
file.save(path)
       │
       ▼
shared/photo.jpg
       │
       ▼
"Success!"
       │
       ▼
📱 PHONE
```

---

# 9. Multiple files

If you later want multiple files, change:

```html
<input type="file" name="file">
```

to:

```html
<input type="file" name="files" multiple>
```

Then:

```python
files = request.files.getlist("files")

for file in files:
    path = os.path.join(folder, file.filename)
    file.save(path)
```

The concept is:

```text
ONE FILE
request.files["file"]

MULTIPLE FILES
request.files.getlist("files")
```

---

## 10. The key HTTP concepts

For this project, remember:

|HTTP|Meaning|
|---|---|
|`GET /`|Give me the webpage|
|`POST /upload`|Here's a file|
|`request.files`|Access uploaded files|
|`file.save()`|Save the file to disk|
|`os.path.join()`|Build a file path|

So the heart of your project is really just:

```python
@app.route("/upload", methods=["POST"])
def upload():

    file = request.files["file"]

    path = os.path.join(folder, file.filename)

    file.save(path)

    return "<h1>Success!</h1>"
```

**Browser → HTTP POST → Flask → `request.files` → `file.save()` → `shared/`**