### What is `.gitignore`?

A **.gitignore** file tells Git:

> “Don’t track these files or folders.”

This is useful because you don’t want to upload things like:

- temporary files
    
- database files
    
- virtual environments
    
- cache files
    

---

## 1. Where to create `.gitignore`

You create it in the **root of your project** (main folder).

### Example structure:

```text
project_folder/
│
├── app.py
├── config.py
├── .gitignore   ← here
├── database/
│   └── my_database.db
└── venv/
```

---

## 2. How to create it

### Option 1 (manually)

Just create a file named:

```text
.gitignore
```

- The dot `.` at the beginning is important
    
- No file extension
    

---

### Option 2 (terminal)

```bash
touch .gitignore
```

---

## 3. How to ignore files

Inside `.gitignore`, you list files or folders you want Git to ignore.

---

### Example 1: Ignore a file

```text
config.py
```

This ignores only `config.py`.

---

### Example 2: Ignore a folder

```text
venv/
```

This ignores the entire virtual environment folder.

---

### Example 3: Ignore database files

```text
database.db
```

or if inside a folder:

```text
database/
```

---

### Example 4: Ignore all Python cache files

```text
__pycache__/
*.pyc
```

- `*` means “any file matching this pattern”
    

---

### Example 5: Common Flask/Python `.gitignore`

```text
# Virtual environment
venv/

# Python cache
__pycache__/
*.pyc

# Database files
*.db

# Environment variables
.env
```

---

## 4. Important rule (very important)

If you already added a file to Git, `.gitignore` won’t remove it automatically.

### Fix it:

```bash
git rm --cached filename
```

Example:

```bash
git rm --cached database.db
```

Then commit again.

---

## 5. How Git uses `.gitignore`

1. Git checks `.gitignore`
    
2. If a file matches → it is NOT tracked
    
3. If it is not in `.gitignore` → Git tracks it normally
    

---

## 6. Simple summary

- `.gitignore` = list of files Git should ignore
    
- Put it in project root
    
- Write file or folder names inside
    
- Use patterns like `*.db` or `__pycache__/`
    
- Commit everything except ignored files
    

---

That’s it—you now know how to control what Git tracks in a very simple way.