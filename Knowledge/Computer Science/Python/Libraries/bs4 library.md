## 🌿 **BeautifulSoup4 (bs4) – Quick Introduction**

**BeautifulSoup4** is a Python library used for **web scraping**. It parses HTML/XML documents and lets you easily navigate and extract data from them.

It does **not** download web pages by itself — it parses markup. You usually combine it with `requests`.

---

## 1️⃣ **Installation**

```Python
pip install beautifulsoup4  
pip install requests
```

---

## 2️⃣ **Basic Usage**

```Python
import requests  
from bs4 import BeautifulSoup

url = "https://example.com"  
response = requests.get(url)  

soup = BeautifulSoup(response.text, "html.parser")
```

🔹 `"html.parser"` is Python’s built-in parser.  
Other options:

- `"lxml"` (faster)
    
- `"html5lib"` (more tolerant)

## **Important** method:

```Python
print(soup.prettify())
```

---

## 🧠 **Core Concepts**

## 🔹 1. The `soup` Object

Represents the whole parsed document.  
You use it to search and navigate.

---

## 🔹 2. Tags

HTML elements like `<div>`, `<p>`, `<a>`.

```Python
soup.title  
soup.h1
```

Access tag attributes:

```Python
link = soup.a  
print(link['href'])
```

---

## 🔹 3. Searching the Document

### ✅ **find()**

Returns the **first match**.

```Python
soup.find("p")  
soup.find("div", class_="container")
```

---

### ✅ **find_all()**

Returns **all matches** (as a list).

```Python
soup.find_all("a")  
soup.find_all("div", class_="item")
```

Search by **attribute**.

```Python
soup.find("a", href=True)  
soup.find_all("input", type="text")
```

Search with **string=** parameter

```Python
soup.find(string="Hello")  
soup.find_all(string=True)  # all text nodes

Using a function:

soup.find_all(string=lambda text: "Python" in text)
```

---

### ✅ **select()** (CSS selectors ⭐ very powerful)

```Python
soup.select("div.item")  
soup.select("a[href]")  
soup.select("#main")
```

Returns a list.

---

### ✅ **select_one()**

```Python
soup.select_one("div.item")
```

Returns first match.

---

# 📦 **Extracting Data**

## 🔹 Get text

```Python
tag.text  
tag.get_text()
```

With cleanup:

```Python
tag.get_text(strip=True)
```

---

## 🔹 Get attributes

```Python
tag['href']  
tag.get('href')
```

Use `.get()` to avoid errors if attribute doesn’t exist.

---

## 🌳 Navigating the Tree

## Parent

```Python
tag.parent
```

## Children

```Python
tag.children  
tag.contents
```

## Siblings

```Python
tag.next_sibling  
tag.previous_sibling
```

**Better** alternative:

```Python
tag.find_next_sibling()  
tag.find_previous_sibling()
```

Search forward or backward in the document.
**find_next() / .find_previous()**

```Python
tag.find_next("div")
```

---

## 🔁 **Loop Example**

```Python
for link in soup.find_all("a"):  
    print(link.get_text(), link.get("href"))
```

---

## 🧹 **Cleaning / Modifying HTML**

Remove a tag:

```Python
tag.decompose()
```

Extract but keep in memory:

```Python
tag.extract()
```

---

## 🎯 **Most Important Methods Summary**

| Method        | Purpose              |
| ------------- | -------------------- |
| `find()`      | First match          |
| `find_all()`  | All matches          |
| `select()`    | CSS selector search  |
| `get_text()`  | Extract clean text   |
| `get()`       | Safely get attribute |
| `decompose()` | Remove tag           |
|               |                      |

---

