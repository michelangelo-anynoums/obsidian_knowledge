## Flask + SQLite

## Basic Setup

```Python
pip install flask, sqlite3
```

---

## 1. Core Idea

- **Flask** → handles web routes (URLs, requests, responses).
    
- **SQLite** → stores data in a local `.db` file.
    
- **Goal** → connect Flask routes to a database.
    

---

## 2. Important Functions Explained

### `sqlite3.connect(DATABASE)`

- Opens (or creates) the database file.
    
- Returns a **connection object**.
    

```python
conn = sqlite3.connect("example.db")
```

---

### `get_db()`

- Ensures **one DB connection per request**.
    
- Uses Flask’s `g` object (temporary storage).
    

```python
def get_db():
    if "db" not in g:
        g.db = sqlite3.connect(DATABASE)
    return g.db
```

👉 Why?

- Avoids opening multiple connections.
    
- Keeps things efficient and clean.
    

---

### `g` (Flask global object)

- Stores data during a request.
    
- Reset after each request.
    

Example:

```python
g.db = connection
```

---

### `cursor()`

- Used to run SQL commands.
    

```python
cursor = db.cursor()
cursor.execute("SELECT * FROM users")
```

---

### `execute()`

- Runs SQL queries.
    

Examples:

```python
cursor.execute("CREATE TABLE users (id INTEGER, name TEXT)")
cursor.execute("INSERT INTO users (name) VALUES (?)", ("Alice",))
```

👉 Use `?` to prevent SQL injection.

---

### `commit()`

- Saves changes to the database.
    

```python
db.commit()
```

👉 Needed after:

- INSERT
    
- UPDATE
    
- DELETE
    

---

### `fetchall()` / `fetchone()`

- Gets query results.
    

```python
users = cursor.fetchall()
```

- `fetchall()` → all rows
    
- `fetchone()` → single row
    

---

### `@app.teardown_appcontext`

- Runs after each request.
    
- Used to **close DB connection**.
    

```python
@app.teardown_appcontext
def close_db(exception):
    db = g.pop("db", None)
    if db is not None:
        db.close()
```

👉 Prevents memory leaks.

---

## 3. Clean Example (Improved)

```python
from flask import Flask, g
import sqlite3

app = Flask(__name__)
DATABASE = "example.db"

def get_db():
    if "db" not in g:
        g.db = sqlite3.connect(DATABASE)
    return g.db

@app.teardown_appcontext
def close_db(exception):
    db = g.pop("db", None)
    if db:
        db.close()

@app.route("/users")
def users():
    db = get_db()
    cursor = db.cursor()

    cursor.execute("SELECT * FROM users")
    return str(cursor.fetchall())
```

---

## 4. Database Initialization (Important)

Instead of creating tables in routes:

```python
def init_db():
    db = sqlite3.connect(DATABASE)
    cursor = db.cursor()
    
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS users (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL
        )
    """)
    
    db.commit()
    db.close()
```

---

## 5. Using ORM (SQLAlchemy) — Easier Way

### What is ORM?

- ORM = Object Relational Mapping
    
- Lets you use **Python objects instead of SQL**
    

---

### Install

```bash
pip install flask-sqlalchemy
```

---

### Setup

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///example.db"

db = SQLAlchemy(app)
```

---

### Create Model (Table)

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
```

👉 This replaces SQL:

- Table = class
    
- Columns = attributes
    

---

### Create Database

```python
with app.app_context():
    db.create_all()
```

---

### Insert Data

```python
new_user = User(name="Alice")
db.session.add(new_user)
db.session.commit()
```

---

### Query Data

```python
users = User.query.all()
```

Other examples:

```python
User.query.first()
User.query.filter_by(name="Alice").first()
```

---

### Delete Data

```python
user = User.query.first()
db.session.delete(user)
db.session.commit()
```

---

## 6. When to Use What?

### Use `sqlite3` if:

- Very small project
    
- Learning SQL basics
    
- Full control needed
    

### Use ORM (SQLAlchemy) if:

- Medium/large project
    
- Cleaner code
    
- Less SQL writing
    

---

## 7. Key Takeaways

- Use `g` to manage DB connection per request.
    
- Always close connections (`teardown_appcontext`).
    
- Use `commit()` after changes.
    
- Prefer ORM for scalability and cleaner code.
    
- SQLite is perfect for simple apps and prototypes.
    

---