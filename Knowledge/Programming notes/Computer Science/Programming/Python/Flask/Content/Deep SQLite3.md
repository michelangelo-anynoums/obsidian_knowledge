**sqlite3** is a built-in Python module that lets you work with a small, file-based database. You don’t need to install anything extra—Python already includes it.

Here are the most important parts, explained simply:

---

### 1. `sqlite3.connect()`

**What it does:**  
Opens a connection to a database file.

```python
import sqlite3
conn = sqlite3.connect("example.db")
```

- If the file doesn’t exist, it will be created.
    
- Think of this as “opening” the database.
    

---

### 2. `conn.cursor()`

**What it does:**  
Creates a cursor object to run SQL commands.

```python
cursor = conn.cursor()
```

- The cursor is like a tool that lets you talk to the database.
    

---

### 3. `cursor.execute()`

**What it does:**  
Runs an SQL command (like creating tables or inserting data).

```python
cursor.execute("CREATE TABLE users (id INTEGER, name TEXT)")
```

- You use this for **all SQL queries** (CREATE, INSERT, SELECT, etc.).
    

---

### 4. `conn.commit()`

**What it does:**  
Saves changes to the database.

```python
conn.commit()
```

- Required after **INSERT, UPDATE, DELETE**
    
- Without this, changes may not be saved.
    

---

### 5. `cursor.fetchall()`

**What it does:**  
Gets all results from a query.

```python
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()
```

- Returns a list of rows (data from the database)
    

---

### 6. `cursor.fetchone()`

**What it does:**  
Gets just one result.

```python
row = cursor.fetchone()
```

- Useful when you only expect a single result
    

---

### 7. `conn.close()`

**What it does:**  
Closes the database connection.

```python
conn.close()
```

- Always close when you're done to free resources
    

---

### Simple Flow (How it all connects)

1. Connect → `connect()`
    
2. Create cursor → `cursor()`
    
3. Run query → `execute()`
    
4. Save (if needed) → `commit()`
    
5. Get results → `fetchall()` / `fetchone()`
    
6. Close → `close()`
    

---

That’s the core of `sqlite3`. Everything else builds on these basic steps.