# Python Environment Variables and `.env` Files

## Overview

Environment variables are key-value pairs stored outside your source code and commonly used for:

- API keys
    
- Database credentials
    
- Secret tokens
    
- Configuration values
    
- Runtime settings
    

Example:

```bash
DATABASE_URL=postgres://localhost/mydb
DEBUG=True
API_KEY=abc123
```

In Python, environment variables are usually accessed through the built-in `os` module.

---

# Why Use Environment Variables?

Hardcoding secrets directly into code is risky.

Bad:

```python
API_KEY = "super-secret-key"
```

Better:

```python
import os

API_KEY = os.getenv("API_KEY")
```

Benefits:

- Keeps secrets out of source control
    
- Makes configuration environment-specific
    
- Easier deployment across dev/staging/production
    
- Works well with Docker, CI/CD, cloud platforms
    

---

# `.env` Files

A `.env` file is a local text file containing environment variables.

Example `.env`:

```env
APP_NAME=MyApp
DEBUG=True
PORT=8000
DATABASE_URL=postgresql://user:pass@localhost/db
SECRET_KEY=mysecret
```

Typically placed in the project root.

---

# Installing `python-dotenv`

The most common library is `python-dotenv`.

Install:

```bash
pip install python-dotenv
```

Official project:

[python-dotenv](https://github.com/theskumar/python-dotenv?utm_source=chatgpt.com)

---

# Loading `.env` Variables

Basic usage:

```python
from dotenv import load_dotenv
import os

load_dotenv()

secret = os.getenv("SECRET_KEY")

print(secret)
```

`load_dotenv()` reads the `.env` file and injects variables into `os.environ`.

---

# `os.environ`

`os.environ` behaves like a dictionary.

Example:

```python
import os

print(os.environ)
```

Access variable:

```python
db_url = os.environ["DATABASE_URL"]
```

Important:

- Raises `KeyError` if variable does not exist
    

Safer alternative:

```python
db_url = os.environ.get("DATABASE_URL")
```

---

# All Common Ways to Retrieve Environment Variables

## 1. `os.getenv()`

Most commonly used.

```python
import os

debug = os.getenv("DEBUG")
```

With default value:

```python
debug = os.getenv("DEBUG", "False")
```

Advantages:

- Safe
    
- Returns `None` if missing
    
- Supports defaults
    

---

## 2. `os.environ["KEY"]`

Strict access.

```python
import os

api_key = os.environ["API_KEY"]
```

Behavior:

- Raises `KeyError` if missing
    

Use when variable MUST exist.

---

## 3. `os.environ.get("KEY")`

Dictionary-style safe access.

```python
import os

api_key = os.environ.get("API_KEY")
```

With default:

```python
port = os.environ.get("PORT", 5000)
```

---

## 4. `dotenv_values()`

Reads `.env` without modifying environment variables.

```python
from dotenv import dotenv_values

config = dotenv_values(".env")

print(config["SECRET_KEY"])
```

Useful for:

- Config previews
    
- Testing
    
- Multiple config files
    

---

# Full Example

## `.env`

```env
APP_ENV=development
DEBUG=True
PORT=8000
API_KEY=xyz123
```

## `main.py`

```python
from dotenv import load_dotenv
import os

load_dotenv()

app_env = os.getenv("APP_ENV")
debug = os.getenv("DEBUG")
port = os.getenv("PORT")
api_key = os.environ.get("API_KEY")

print("Environment:", app_env)
print("Debug:", debug)
print("Port:", port)
print("API Key:", api_key)
```

---

# Type Conversion

Environment variables are always strings.

Example:

```python
port = os.getenv("PORT")
print(type(port))
```

Output:

```python
<class 'str'>
```

Convert manually:

```python
port = int(os.getenv("PORT", 8000))
```

Boolean conversion:

```python
debug = os.getenv("DEBUG", "False").lower() == "true"
```

---

# Multiple `.env` Files

Common structure:

```text
.env
.env.development
.env.production
.env.test
```

Load specific file:

```python
from dotenv import load_dotenv

load_dotenv(".env.production")
```

---

# Override Existing Variables

By default, existing system variables are NOT overwritten.

```python
load_dotenv(override=True)
```

---

# Check If Variable Exists

```python
import os

if "API_KEY" in os.environ:
    print("Exists")
```

---

# Listing All Environment Variables

```python
import os

for key, value in os.environ.items():
    print(key, value)
```

---

# Best Practices

## 1. Never Commit `.env`

Add to `.gitignore`:

```gitignore
.env
```

---

## 2. Provide `.env.example`

Example:

```env
DATABASE_URL=
SECRET_KEY=
DEBUG=
```

This documents required variables.

---

## 3. Validate Required Variables

```python
import os

required = ["DATABASE_URL", "SECRET_KEY"]

for key in required:
    if not os.getenv(key):
        raise ValueError(f"Missing environment variable: {key}")
```

---

## 4. Use Defaults Carefully

Good:

```python
port = int(os.getenv("PORT", 8000))
```

Dangerous:

```python
secret = os.getenv("SECRET_KEY", "default-secret")
```

Never provide insecure defaults for secrets.

---

# Common Mistakes

## Forgetting `load_dotenv()`

```python
from dotenv import load_dotenv

load_dotenv()
```

Without this, `.env` variables may not load locally.

---

## Assuming Booleans Are Real Booleans

Wrong:

```python
if os.getenv("DEBUG"):
```

Because `"False"` is still truthy.

Correct:

```python
debug = os.getenv("DEBUG", "False").lower() == "true"
```

---

## Committing Secrets

Never push:

- `.env`
    
- API keys
    
- Database passwords
    
- JWT secrets
    

---

# Useful Patterns

## Config Class

```python
import os
from dotenv import load_dotenv

load_dotenv()

class Config:
    DEBUG = os.getenv("DEBUG", "False").lower() == "true"
    PORT = int(os.getenv("PORT", 8000))
    DATABASE_URL = os.getenv("DATABASE_URL")
```

Usage:

```python
print(Config.PORT)
```

---

# Environment Variables in Docker

Docker example:

```bash
docker run -e API_KEY=abc123 myapp
```

Docker Compose:

```yaml
environment:
  - API_KEY=abc123
```

Or:

```yaml
env_file:
  - .env
```

---

# Environment Variables in Production

Production platforms usually provide native environment variable systems:

- [Docker](https://www.docker.com/?utm_source=chatgpt.com)
    
- [Kubernetes](https://kubernetes.io/?utm_source=chatgpt.com)
    
- [Heroku](https://www.heroku.com/?utm_source=chatgpt.com)
    
- [Vercel](https://vercel.com/?utm_source=chatgpt.com)
    
- [Render](https://render.com/?utm_source=chatgpt.com)
    
- [Railway](https://railway.com/?utm_source=chatgpt.com)
    

In production, `.env` files are often replaced with platform-managed secrets.

---

# Quick Reference

|Method|Safe if Missing?|Supports Default?|Notes|
|---|---|---|---|
|`os.environ["KEY"]`|No|No|Raises `KeyError`|
|`os.environ.get("KEY")`|Yes|Yes|Dict-style|
|`os.getenv("KEY")`|Yes|Yes|Most common|
|`dotenv_values()`|Yes|N/A|Reads file only|

---

# Recommended Standard Setup

```python
from dotenv import load_dotenv
import os

load_dotenv()

DATABASE_URL = os.getenv("DATABASE_URL")
DEBUG = os.getenv("DEBUG", "False").lower() == "true"
PORT = int(os.getenv("PORT", 8000))
```

This is the most common and practical approach for modern Python applications.