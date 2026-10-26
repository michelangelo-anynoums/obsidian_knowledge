## Python `venv` — Quick Notes

## What is `venv`?

- `venv` is a built-in Python module used to create **virtual environments**.
    
- A virtual environment is an isolated space where you can install packages without affecting the global Python installation.
    

## Why use it?

- Avoid dependency conflicts between projects
    
- Keep project requirements separate
    
- Make projects more portable and reproducible
    

## Create a virtual environment

```bash
python -m venv myenv
```

## Activate the environment

- **macOS / Linux:**
    

```bash
source myenv/bin/activate
```

- **Windows:**
    

```bash
myenv\Scripts\activate
```

## Deactivate the environment

```bash
deactivate
```

## Install packages inside `venv`

```bash
pip install package_name
```

## Save dependencies

```bash
pip freeze > requirements.txt
```

## Install from requirements

```bash
pip install -r requirements.txt
```

## Notes

- Each project should have its own `venv`
    
- The environment folder (e.g., `myenv/`) is usually added to `.gitignore`
    
- Works with most Python tools and IDEs
    

## Quick tip

- Activate the environment before running your project to ensure correct dependencies are used

---

## Python Dependencies — Sharing Your Project

## Goal

Create a file listing all dependencies so others can install them easily.

## Standard approach: `requirements.txt`

### 1. Generate the file

Activate your virtual environment, then run:

```bash
pip freeze > requirements.txt
```

- This captures all installed packages and their exact versions

### 2. Share the file

Include `requirements.txt` in your project repository

### 3. Install dependencies (for others)

```bash
pip install -r requirements.txt
```

## Best Practices

- Run `pip freeze` **inside your virtual environment**
    
- Keep the environment clean (only install what your project needs)
    
- Commit `requirements.txt` to version control (e.g., Git)
    

## Optional: Minimal dependencies

Instead of freezing everything, you can manually create `requirements.txt`:

```
flask==3.0.0
requests>=2.31.0
```

## Alternative Tools

- `pip-tools` → more control over dependency resolution
    
- `poetry` → modern dependency + packaging manager
    
- `pipenv` → combines virtualenv + dependency management
    

## Quick Tip

- Use exact versions (`==`) for reproducibility
    
- Use ranges (`>=`) if you want flexibility

---
