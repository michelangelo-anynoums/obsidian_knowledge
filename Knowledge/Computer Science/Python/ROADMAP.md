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
- [x]  `@classmethod`
[[classmethod]]

### Python Classes

- [x]  Understand what **dunder methods** (“double underscore methods”) are
- [x]  Learn the most common object lifecycle methods:
[[init, new and del dunder methods]]
    - [x]  `__init__`
    - [x]  `__del__`
    - [x]  `__new__`
- [x]  Learn how objects are represented:
[[str, repr dunder methods]]
    - [x]  `__str__`
    - [x]  `__repr__`
- [x]  Learn comparison and equality methods:
[[eq, ls, gt dunder methods]]
    - [x]  `__eq__`
    - [x]  `__lt__`
    - [x]  `__gt__`
- [x]  Learn operator overloading:
[[add, sub, mul dunder methods]]
    - [x]  `__add__`
    - [x]  `__sub__`
    - [x]  `__mul__`
- [x]  Learn container and iterable behavior:
[[len, iter, getitem, setitem]]
    - [x]  `__len__`
    - [x]  `__getitem__`
    - [x]  `__setitem__`
    - [x]  `__iter__`
- [x]  Learn callable and context manager objects:
[[call, enter, exit]]
    - [x]  `__call__`
    - [x]  `__enter__`
    - [x]  `__exit__`
- [x]  Understand the difference between:
    - [x]  instance attributes
    - [x]  class attributes
    - [x]  properties with `@property`

---

### Dataclasses

- [x]  Learn why Python provides the `dataclasses` module
- [x]  Create your first dataclass with `@dataclass`
- [x]  Understand automatic method generation:
    - [x]  `__init__`
    - [x]  `__repr__`
    - [x]  `__eq__`
- [x]  Learn dataclass options:
    - [x]  `frozen=True`
    - [x]  `order=True`
    - [x]  `slots=True`
- [x]  Learn default values and `field()`
- [x]  Learn `default_factory`
- [x]  Learn type hints inside dataclasses
- [x]  Convert dataclasses to dictionaries with `asdict()`
- [x]  Learn when to use:
    - [x]  normal classes
    - [x]  dataclasses
    - [x]  namedtuples
- [x]  Build small practice projects using dataclasses:
    - [x]  inventory system
    - [x]  game character stats
    - [x]  banking/account models
    - [x]  configuration objects








[[dataclasses python]]
### Practice

- [ ]  Bank Account system (deposit, withdraw, balance)
- [ ]  Library Manager (books, users, borrowing)
- [x]  Game Character system (inheritance-based)

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

# Middle Python knowledge
## 1) Core “must fully understand” Python behavior

These fix the gaps that separate junior from mid-level:

- Mutability (deep vs shallow copy, references)
- Closures + late binding (`lambda`, nested functions)
- Scope rules (LEGB in practice)
- `*args`, `**kwargs` (real usage, not just syntax)
- Object identity vs equality (`is` vs `==`)

---

## 2) OOP (real-world level)

Go beyond basic classes:

- Inheritance vs composition (when to use which)
- `@classmethod` vs `@staticmethod`
- Dunder methods (`__str__`, `__repr__`, `__len__`, etc.)
- Basic SOLID principles (especially SRP + OCP)

---

## 3) Iteration & functional tools

These appear everywhere in real code:

- Iterators vs iterables
- Generators + `yield`
- `map`, `filter`, `any`, `all`
- Comprehension mastery (list/dict/set)

---

## 4) Error handling (production style)

- Custom exceptions
- Proper use of `try/except/else/finally`
- Avoiding silent failures

---

## 5) Concurrency basics (very important gap for you)

- `asyncio` fundamentals (event loop, `await`)
- When NOT to use async
- Difference: threading vs multiprocessing vs async

---

## 6) Practical “job-ready” skills

These matter more than theory for getting hired:

- Working with APIs (requests / REST)
- File handling (JSON, CSV)
- Basic SQL (SELECT, JOIN, WHERE)
- Virtual environments + pip/poetry
- Debugging (reading stack traces properly)

---

## 7) Testing (often ignored, but important)

- `unittest` or `pytest`
- Writing simple test cases
- Why tests matter in real projects