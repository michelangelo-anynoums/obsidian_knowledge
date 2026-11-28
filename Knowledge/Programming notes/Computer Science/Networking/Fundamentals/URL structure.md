# 🌐 URL Structure

> A **URL (Uniform Resource Locator)** is the address used to locate a resource on the internet.

## 🔍 1. Anatomy of a URL

```
https://www.example.com:8080/blog/article?id=10#comments
```

![[Pasted image 20261128082833.png|596]]

## 🔍 1. Anatomy of a URL

```http
https://www.example.com:8080/blog/article?id=10#comments
```

|Component|Example|Purpose|
|---|---|---|
|Scheme|`https`|Defines the communication protocol|
|Subdomain|`www`|Identifies a subdivision of a domain|
|Domain name|`example`|Identifies the website|
|TLD|`.com`|Defines the domain extension|
|Port|`8080`|Identifies the server service endpoint|
|Path|`/blog/article`|Locates a resource|
|Query|`?id=10`|Sends additional parameters|
|Fragment|`#comments`|Points to a section of a page|

---

## 🧩 2. URL Components Explained

### ① Scheme (Protocol)

Defines **how the browser communicates** with the server.

```
http://example.com
https://example.com
```

- `http` → HyperText Transfer Protocol.
- `https` → HTTP Secure (encrypted communication using TLS).

💡 HTTPS protects data exchanged between the browser and server.

### ② Subdomain (`www`)

A subdomain is an additional section of a domain.

```
www.example.com
blog.example.com
shop.example.com
```

- `www` → Traditionally used for the website.
- `blog` → Could host a blog.
- `shop` → Could host an online store.

**Why use it?**

To organize different services or sections under the same domain.

💡 `www` is optional. A website can work perfectly without it.

```
https://example.com
https://www.example.com
```

Both can lead to the same website.

### ③ Domain Name

The domain is the human-readable name used to access a website.

```
example.com
```

- `example` → Registered domain name.
- `.com` → Top-Level Domain (TLD).

**Why use it?**

Computers communicate using IP addresses, but domain names are easier for humans to remember.

```
example.com → IP address
```

DNS (Domain Name System) translates domain names into IP addresses.

### ④ Top-Level Domain (TLD)

The TLD is the last part of a domain name.

```
example.com
example.org
example.net
example.es
```

|TLD|Common association|
|---|---|
|`.com`|Commercial / general use|
|`.org`|Organizations|
|`.net`|Originally network-related|
|`.edu`|Educational institutions (US)|
|`.gov`|US government|
|`.es`|Spain|
|`.uk`|United Kingdom|

**Why use it?**

It provides a domain namespace and can indicate a domain's intended category or geographic association.

💡 `.com` originally meant commercial, but today it is widely used by businesses, individuals and organizations.

### ⑤ Port

Identifies a specific service or endpoint on a server.

```
https://example.com:8080
```

Common ports:

|Port|Protocol|
|---|---|
|`80`|HTTP|
|`443`|HTTPS|
|`21`|FTP|
|`22`|SSH|

💡 HTTP normally uses port `80`, and HTTPS uses port `443`. Browsers usually hide these default ports.

### ⑥ Path

Identifies the location of a resource on a website.

```http
https://example.com/blog/article
```

```
/               → Root
/blog           → Blog section
/article        → Specific resource
```

**Why use it?**

To organize and access different pages, files or resources.

### ⑦ Query Parameters

Send additional information to the server through the URL.

```http
https://example.com/search?q=javascript&page=2
```

```
?              → Starts query string
q=javascript   → Search term
&              → Separates parameters
page=2         → Page number
```

**Why use them?**

- Search queries
- Filtering results
- Sorting products
- Pagination

### ⑧ Fragment (Anchor)

Points to a specific section within a page.

```http
https://example.com/guide#installation
```

```
#installation → Target section
```

**Why use it?**

To navigate directly to a particular section without manually scrolling.

---

## ⚡ 3. Important URL Characters

|Character|Meaning|
|---|---|
|`://`|Separates scheme from authority|
|`.`|Separates domain labels|
|`/`|Separates path segments|
|`:`|Introduces a port|
|`?`|Starts query string|
|`&`|Separates query parameters|
|`=`|Assigns parameter values|
|`#`|Starts fragment|
|`%20`|Encoded space|

## 🧠 4. How Everything Works Together

```http
https://www.example.com/products?id=25
│       │   │       │   │        │
│       │   │       │   │        └─ Query parameter
│       │   │       │   └─ Path
│       │   │       └─ TLD
│       │   └─ Domain name
│       └─ Subdomain
└─ Scheme
```

**Behind the scenes:**

1. 🌐 The browser reads the URL.
2. 🔎 DNS resolves the domain name into an IP address.
3. 🔒 The browser establishes a connection using HTTPS.
4. 📡 The browser sends an HTTP request.
5. 📄 The server responds with the requested resource.

---

## 🎥 5. Recommended Videos

1. **URI, URL and URN explained**
    - [▶️ Watch on YouTube](https://www.youtube.com/watch?v=vpYct2npKD8&t=79s)
2. **URL structure explained**
    - [▶️ Watch on YouTube](https://www.youtube.com/watch?v=5Jr-_Za5yQM)

---

**💡 Remember:** DNS finds the server, the domain identifies the website, the path identifies the resource, and query parameters provide additional information.

