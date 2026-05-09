## 🐍 Python Learning Roadmap (Progress Tracker)

---

## 1. 🧱 Classes & Object-Oriented Programming

### Core Concepts

- [x]  Class structure and instance methods  
[[Class structure and instance methods]]
- [x]  Class vs instance attributes
[[Class vs instance attributes]]
- [x]  `__init__` and `self`
[[__init__ and self]]
- [x]  Inheritance
[[Inheritance]]
- [x]  Polymorphism
[[Polymorphism]]
- [x]  `super()` usage
[[super() usage]]

- [x]  Encapsulation basics
[[encapsulation basics]]


### Advanced Features

- [x]  `@property`
[[property decorator]]
- [x]  `@staticmethod`
[[static method]]
- [ ]  `@classmethod`

## Python Classes

- [ ]  Understand what **dunder methods** (“double underscore methods”) are
- [ ]  Learn the most common object lifecycle methods:
    - [ ]  `__init__`
    - [ ]  `__del__`
    - [ ]  `__new__`
- [ ]  Learn how objects are represented:
    - [ ]  `__str__`
    - [ ]  `__repr__`
- [ ]  Learn comparison and equality methods:
    - [ ]  `__eq__`
    - [ ]  `__lt__`
    - [ ]  `__gt__`
- [ ]  Learn operator overloading:
    - [ ]  `__add__`
    - [ ]  `__sub__`
    - [ ]  `__mul__`
- [ ]  Learn container and iterable behavior:
    - [ ]  `__len__`
    - [ ]  `__getitem__`
    - [ ]  `__setitem__`
    - [ ]  `__iter__`
- [ ]  Learn callable and context manager objects:
    - [ ]  `__call__`
    - [ ]  `__enter__`
    - [ ]  `__exit__`
- [ ]  Understand the difference between:
    - [ ]  instance attributes
    - [ ]  class attributes
    - [ ]  properties with `@property`

---

## Dataclasses

- [ ]  Learn why Python provides the `dataclasses` module
- [ ]  Create your first dataclass with `@dataclass`
- [ ]  Understand automatic method generation:
    - [ ]  `__init__`
    - [ ]  `__repr__`
    - [ ]  `__eq__`
- [ ]  Learn dataclass options:
    - [ ]  `frozen=True`
    - [ ]  `order=True`
    - [ ]  `slots=True`
- [ ]  Learn default values and `field()`
- [ ]  Learn `default_factory`
- [ ]  Learn type hints inside dataclasses
- [ ]  Convert dataclasses to dictionaries with `asdict()`
- [ ]  Learn when to use:
    - [ ]  normal classes
    - [ ]  dataclasses
    - [ ]  namedtuples
- [ ]  Build small practice projects using dataclasses:
    - [ ]  inventory system
    - [ ]  game character stats
    - [ ]  banking/account models
    - [ ]  configuration objects
### Practice

- [ ]  Bank Account system (deposit, withdraw, balance)
- [ ]  Library Manager (books, users, borrowing)
- [ ]  Game Character system (inheritance-based)

---

## 2. ⚡ AsyncIO (Asynchronous Programming)

### Core Concepts

- [ ]  Event loop
- [ ]  `async` / `await`
- [ ]  Coroutines
- [ ]  Tasks & concurrency

### Practice

- [ ]  API Fetch Program
    - [ ]  Fetch multiple endpoints
    - [ ]  Handle responses
    - [ ]  Compare async vs sync

---

## 3. 🌍 Browser Automation (Playwright)

### Core Concepts

- [ ]  What browser automation is
- [ ]  Headless vs headed browsers
- [ ]  Browser contexts & pages
- [ ]  Selectors (CSS, text, XPath basics)
- [ ]  Waiting for elements (`wait_for_selector`)
- [ ]  Handling navigation & redirects

### Core Playwright Features

- [ ]  Launching browsers (Chromium, Firefox, WebKit)
- [ ]  Page interaction (click, type, scroll)
- [ ]  Form handling
- [ ]  Screenshots & PDF export
- [ ]  Handling dialogs (alerts, prompts)
- [ ]  Managing cookies & sessions

### Advanced Usage

- [ ]  Async vs sync Playwright APIs
- [ ]  Intercepting network requests
- [ ]  Scraping dynamic content
- [ ]  Handling logins & authentication flows
- [ ]  Running automated tests
- [ ]  Error handling & retries

### Practice

- [ ]  Simple Browser Bot
    - [ ]  Open a website
    - [ ]  Click buttons
    - [ ]  Fill forms
- [ ]  Web Scraper
    - [ ]  Extract page data
    - [ ]  Handle pagination
    - [ ]  Save results (CSV/JSON)
- [ ]  Auto Login Script
    - [ ]  Log into a website
    - [ ]  Store session
    - [ ]  Reuse authentication
- [ ]  Screenshot Tool
    - [ ]  Capture full-page screenshots
    - [ ]  Save images automatically

---

## 🧩 4. 🖥️ Command-Line Interfaces (`argparse`)

### Core Concepts

- [ ]  What command-line interfaces (CLI) are  
- [ ]  Why CLIs are useful (automation, scripting, tooling)  
- [ ]  Positional vs optional arguments  
- [ ]  Flags and switches (`--verbose`, `--output`)  
- [ ]  Data types for arguments (`int`, `str`, etc.)  
- [ ]  Default values and required arguments  
- [ ]  Help messages (`-h/--help`)

---

### Core argparse Features

- [ ]  Creating a parser (`ArgumentParser`)  
- [ ]  Adding arguments (`add_argument`)  
- [ ]  Parsing input (`parse_args`)  
- [ ]  Boolean flags (`store_true`)  
- [ ]  Setting choices (`choices=[...]`)  
- [ ]  Grouping arguments (optional vs required groups)  
- [ ]  Custom help descriptions

---

### Advanced Usage

- [ ]  Subcommands (e.g., `git commit`, `git push`)  
- [ ]  Argument validation and constraints  
- [ ]  Parsing multiple values (lists)  
- [ ]  Reading arguments from files  
- [ ]  Environment variable integration  
- [ ]  Custom error handling  
- [ ]  Structuring larger CLI tools

---

### Practice

- [ ]  **Greeter CLI**  
- [ ]  Accept a name as input  
- [ ]  Add optional `--uppercase` flag  
- [ ]  Print customized greeting

---

## 5. ⚙️ Subprocess (System Interaction)

### Core Concepts

- [ ]  Running external commands
- [ ]  `subprocess.run()`
- [ ]  `subprocess.Popen()`
- [ ]  Capture output/errors

### Practice

- [ ]  External Program Launcher
    - [ ]  Open applications
    - [ ]  Execute shell commands
    - [ ]  Log outputs

---

## 6. 🔌 Sockets (Networking Basics)

### Core Concepts

- [ ]  Client-server architecture
- [ ]  TCP sockets
- [ ]  Send/receive data
- [ ]  `encode()` / `decode()`

### Practice

- [ ]  Chat Application
    - [ ]  Server setup
    - [ ]  Multiple clients
    - [ ]  Messaging system
    - [ ]  Basic commands (`/quit`, etc.)

## 7. 🔐 Cryptography

### Core Concepts

- [ ]  What cryptography is (confidentiality, integrity, authentication)
- [ ]  Symmetric vs asymmetric encryption
- [ ]  Hashing vs encryption (key differences)
- [ ]  Common algorithms (AES, RSA, SHA family)
- [ ]  Encoding vs encryption (Base64 vs real crypto)
- [ ]  Randomness & secure key generation
- [ ]  Salting & why it matters

### Python Tools & Libraries

- [ ]  `hashlib` (SHA256, SHA512, etc.)
- [ ]  `secrets` (secure token generation)
- [ ]  `os.urandom()`
- [ ]  `cryptography` library basics
- [ ]  `bcrypt` for password hashing

### Practical Security Concepts

- [ ]  Password hashing best practices
- [ ]  Secure storage of secrets
- [ ]  Basic encryption/decryption workflow
- [ ]  Avoiding common mistakes (hardcoded keys, weak hashes)

### Practice

- [ ]  Password Hasher Tool
    - [ ]  Hash user passwords
    - [ ]  Verify password input
    - [ ]  Add salting
- [ ]  File Encryptor
    - [ ]  Encrypt a file
    - [ ]  Decrypt the file
    - [ ]  Handle keys securely
- [ ]  Secure Notes App (CLI)
    - [ ]  Save encrypted notes
    - [ ]  Read/decrypt notes
    - [ ]  Password-protected access

---

## 8. 🌐 Flask (Web Development)

### Core Concepts

- [ ]  Routing (`@app.route`)
- [ ]  Request & response handling
- [ ]  Configuration files
- [ ]  Templates (Jinja2 basics)

### Working with Data

- [ ]  File handling (upload/read/write)
- [ ]  SQLite3 basics
- [ ]  SQLAlchemy & ORM

### Authentication & Security

- [ ]  User registration & login
- [ ]  Password hashing
- [ ]  Session management
- [ ]  Basic web security practices

### Project

- [ ]  Simple Login Web App
    - [ ]  User registration
    - [ ]  Login system
    - [ ]  SQLite database
    - [ ]  Protected routes
    - [ ]  Basic UI templates

---
