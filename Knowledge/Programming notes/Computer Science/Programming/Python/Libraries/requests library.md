# 🗂️ **==Requests== – Resume**

## 🧩 **What It Is?**

`requests` is a popular ==Python== library used to send ==HTTP requests==
in a simple, human-friendly way.  It abstracts away the complexity of handling low-level networking code, making it easy to interact with web APIs and retrieve data from the web.

---

## 📥 **Installation**

```Python
pip install requests # install essential library
```

---

## 🚀 **Basic Usage**

### **GET request**

```Python
import requests
response = requests.get("https://httpbin.org/get") 
print(response.status_code) # status code
print(response.json()) # response object
```

### **POST request**

```Python
payload = {"name": "Alice", "age": 25} # dictionary
response = requests.post("https://httpbin.org/post", json=payload) 
print(response.json())
```

----

### **Important concept**

```Python
response.raise_for_status() # raises for an exception
```

---

## 🔑 **Most Essential Features**

- **Simple HTTP methods**: `get()`, `post()`, `put()`, `delete()`, `head()`, `patch()`
    
- **Automatic JSON support**: `response.json()`
    
- **Status info**: `response.status_code`, `response.ok`
    
- **Headers**:
    
    `response.headers`
    
- **Send headers**:
    
    `requests.get(url, headers={"Authorization": "Bearer TOKEN"})`
    
- **Query parameters**:
    
    `requests.get(url, params={"page": 2})`
    
- **Timeouts**:
    
    `requests.get(url, timeout=5)`
    
- **Session objects** (keep cookies, reuse connections):
    
    `session = requests.Session()`

---
## 📄 **Sending Payload Files**

### **Upload a file**

```Python
import requests  
files = {"file": open("example.txt", "rb")} # open file as bytes
response = requests.post("https://httpbin.org/post", files=files) 
print(response.json())
```

## ⬇️ **Download a File (Basic)**

```Python
url = "https://example.com/file.txt" # declare url
response = requests.get(url) # make a request
with open("file.txt", "wb") as file: # open file as wb (write bytes)
	file.write(response.content) # write content
```

✔️ Best for **small files**

---

## ⬇️ **Download Large Files (Streaming – Recommended)**

```Python
url = "https://example.com/large_file.zip" # declare url
response = requests.get(url, stream=True) # add param: stream=True
with open("large_file.zip", "wb") as file: # open file as wb (write bytes)
	for chunk in response.iter_content(chunk_size=8192): # loop over chunks
		file.write(chunk) # write each chunk into the file
print(f"Status: {response.status_code}") # print status code
```

✔️ Uses less memory  
✔️ Safer for large files

---
## Why streaming downloads matter

By default, ==requests== **downloads the entire response into memory**.

That’s bad for:

- large files
    
- slow connections
    
- low-memory systems
    

**Streaming** lets you download the file **chunk by chunk**.

---

## Basic streaming download (recommended way)

```Python
import requests

url = "https://example.com/large_file.zip"  

with requests.get(url, stream=True) as r:     
	r.raise_for_status()  # fail early if error      
	
	with open("large_file.zip", "wb") as f:         
		for chunk in r.iter_content(chunk_size=8192):  
			if chunk:  # filters out keep-alive chunks
			f.write(chunk)
```

### What’s happening

- **stream=True** → don’t download everything at once
    
- **iter_content()** → yields bytes incrementally
    
- **chunk_size=8192** → 8 KB per chunk (good default)
    

---

## Streaming with a Session (best practice)

```Python
session = requests.Session()  

with session.get(url, stream=True) as r:     
	with open("file.zip", "wb") as f:         
		for chunk in r.iter_content(8192):
			f.write(chunk)
```

Why this is better:

- connection reuse
    
- cookies / headers preserved
    
- faster for multiple downloads

---

## 🧾 **Sending Headers**

### **Custom headers**

```Python
import requests  
headers = { 
    "Authorization": "Bearer YOUR_TOKEN", 
    "User-Agent": "MyApp/1.0" } # headers object

response = requests.get("https://httpbin.org/get", headers=headers) 
print(response.json())
```

---

## 📦 **POST with JSON + Headers**

```Python
payload = {
    "username": "bob", 
    "active": True } 
    
headers = {
    "Content-Type": "application/json" }  
    
response = requests.post("https://httpbin.org/post", json=payload, headers=headers)
print(response.status_code)
```

---
# **Most Important HTTP Headers**

## 🔸 **Content-Type**

Tells the server what type of data you're sending.

- `application/json` – JSON payload
    
- `application/x-www-form-urlencoded` – HTML form data
    
- `multipart/form-data` – file uploads

```Python
headers = {
    "Content-Type": "application/json",       # type of data you're sending
    "Accept": "application/json",             # type of data you expect back
    "Authorization": "Bearer YOUR_TOKEN",     # auth token or API key
    "User-Agent": "MyApp/1.0",                # identifies your client/app
    "Accept-Language": "en-US",               # preferred response language
    "Cache-Control": "no-cache",              # disable caching
    "Cookie": "sessionid=12345"               # manually send cookies
}
```
```Python
response = requests.get("https://httpbin.org/get", headers=headers)
```

# **How to Use ==Proxies== with requests:**

To use a ==proxy== with the `requests` library in Python, you simply need to pass a dictionary containing the ==proxy URL== to the `proxies` parameter in the `requests.get()`, `requests.post()`, or other HTTP methods.

#### Example Code:

```Python
import requests  

# Define your proxy 
proxies = { 'http': 'http://your_proxy_ip:port', # http protocol
            'https': 'https://your_proxy_ip:port' } # httpS protocol
 
# Make a request using the proxy 
response = requests.get('http://example.com', proxies=proxies)  

# Check the response 
print(response.text)
```

#  **Free Proxy Sources:**

You can find ==free proxy lists== online (though reliability and speed may vary). Here are a few sites that provide free proxies:

- ==Free Proxy List==
    
- ==ProxyScrape==
    
- ==Spys.one==
    
- ==SSLProxies==

# **Example with a Real Proxy:**

```Python
import requests  
# Example of a free proxy (these may not always 
# work or be fast, so test them beforehand)

proxies = { 'http': 'http://51.38.82.223:8888', # http protocol 
            'https': 'https://51.38.82.223:8888' } # httpS protocol

# Make a request using the proxy 
try:     
    response = requests.get('http://httpbin.org/ip', proxies=proxies, timeout=5) # timeout is optional here
    
	# This will show your IP address as seen by the server 
    print("Response from the server:")     
    print(response.text)  
    
except requests.exceptions.RequestException as e:     
    print(f"Error: {e}")
```

---

## Sessions in **requests**

A **session** (`requests.Session`) lets you persist data across multiple HTTP requests—most commonly **cookies**, but also headers and connection pooling.

Think of it as: _“Act like the same browser for multiple requests.”_

### Why use sessions?

- Automatically **store & send cookies**
    
- Reuse TCP connections (faster)
    
- Share headers across requests
    

### Example

```Python
import requests  

session = requests.Session()  
session.get("https://example.com/login") 

response = session.get("https://example.com/dashboard")
```

If the first request sets a cookie (like a login token), the second request sends it automatically.

---

## Cookies

Cookies are small key–value pairs sent by the server and stored by the client to maintain state (e.g. login, preferences).

### Cookies without a session

```Python
r = requests.get("https://example.com", cookies={"lang": "en"})
```

Sent **once**, not remembered.
### Cookies with a session

```Python
session = requests.Session() 
session.cookies.set("lang", "en")  

session.get("https://example.com")
```

Now the cookie is **persisted** and sent with every request in that session.

---


Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]