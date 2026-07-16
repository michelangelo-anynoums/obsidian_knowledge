## 🧠 Python `encode()` and `decode()` — Quick Notes

### 📌 What are they?

- `encode()` and `decode()` are built-in methods used to convert between:
    
    - **str (text / Unicode)** ↔ **bytes (binary data)**
        

---

### 🔄 `encode()` — _String → Bytes_

- Converts a Python string (`str`) into a bytes object.
    
- You must specify an **encoding format** (default is `'utf-8'`).
    

```python
text = "hello"
b = text.encode("utf-8")

print(b)        # b'hello'
print(type(b))  # <class 'bytes'>
```

✅ Use when:

- Writing data to a file in binary mode
    
- Sending data over a network
    
- Interacting with APIs or systems that expect bytes
    

---

### 🔁 `decode()` — _Bytes → String_

- Converts bytes back into a Python string.
    

```python
b = b"hello"
text = b.decode("utf-8")

print(text)     # "hello"
print(type(text))  # <class 'str'>
```

✅ Use when:

- Reading binary data and you want readable text
    
- Receiving data from files, sockets, or external sources
    

---

### 🔤 Common Encodings

- `'utf-8'` (most common, recommended)
    
- `'ascii'` (limited, older)
    
- `'latin-1'` (used in some legacy systems)
    

---

### ⚠️ Important Notes

- Encoding and decoding must match!
    

```python
text = "café"
b = text.encode("utf-8")

# Correct:
print(b.decode("utf-8"))  # café

# Incorrect:
# print(b.decode("ascii"))  # ❌ UnicodeDecodeError
```

---

### 💡 Mental Model

- `str` = human-readable text
    
- `bytes` = machine-readable raw data
    

👉 `encode()` = "pack text into bytes"  
👉 `decode()` = "unpack bytes into text"

---

### 🧪 Quick Roundtrip Example

```python
original = "Python 🐍"

encoded = original.encode("utf-8")
decoded = encoded.decode("utf-8")

print(encoded)  # b'Python \xf0\x9f\x90\x8d'
print(decoded)  # Python 🐍
```

---

### 📝 One-line Summary

> `encode()` turns text into bytes, and `decode()` turns bytes back into text — using a specific character encoding like UTF-8.

---