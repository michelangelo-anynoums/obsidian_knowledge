---

tags:

- http
- headers
- content-type
- user-agent
- javascript

aliases:

- MIME Types & User Agents

---

# 🌐 Content-Type & User-Agent

## 1. 📦 Content-Type

The `Content-Type` header specifies the media type of an HTTP message body.

### 📝 Text & Web Documents

|Content-Type|Description|
|---|---|
|`text/plain`|Plain text|
|`text/html`|HTML documents|
|`text/css`|CSS stylesheets|
|`text/csv`|CSV files|
|`text/xml`|XML documents|
|`text/markdown`|Markdown text|
|`text/calendar`|Calendar data|
|`text/event-stream`|Server-Sent Events|
|`text/javascript`|JavaScript source|
|`text/tab-separated-values`|TSV files|

### 📊 Application & Data Formats

|Content-Type|Description|
|---|---|
|`application/json`|JSON data|
|`application/ld+json`|JSON-LD|
|`application/xml`|XML data|
|`application/xhtml+xml`|XHTML documents|
|`application/javascript`|JavaScript (legacy media type)|
|`application/pdf`|PDF documents|
|`application/rtf`|Rich Text Format|
|`application/zip`|ZIP archives|
|`application/gzip`|Gzip archives|
|`application/x-tar`|TAR archives|
|`application/x-7z-compressed`|7z archives|
|`application/vnd.rar`|RAR archives|
|`application/octet-stream`|Arbitrary binary data|
|`application/wasm`|WebAssembly|
|`application/sql`|SQL text|
|`application/graphql-response+json`|GraphQL responses|
|`application/problem+json`|JSON error details|
|`application/manifest+json`|Web app manifests|
|`application/x-www-form-urlencoded`|URL-encoded form data|
|`application/vnd.api+json`|JSON:API|
|`application/vnd.oasis.opendocument.text`|OpenDocument text|
|`application/vnd.oasis.opendocument.spreadsheet`|OpenDocument spreadsheet|

### 📑 Microsoft Office & Documents

|Content-Type|Description|
|---|---|
|`application/msword`|Legacy Word `.doc`|
|`application/vnd.openxmlformats-officedocument.wordprocessingml.document`|Word `.docx`|
|`application/vnd.ms-excel`|Legacy Excel `.xls`|
|`application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`|Excel `.xlsx`|
|`application/vnd.ms-powerpoint`|Legacy PowerPoint `.ppt`|
|`application/vnd.openxmlformats-officedocument.presentationml.presentation`|PowerPoint `.pptx`|
|`application/epub+zip`|EPUB ebooks|
|`application/wasm`|WebAssembly modules|

### 🖼️ Images

|Content-Type|Description|
|---|---|
|`image/jpeg`|JPEG images|
|`image/png`|PNG images|
|`image/gif`|GIF images|
|`image/webp`|WebP images|
|`image/avif`|AVIF images|
|`image/svg+xml`|SVG vector images|
|`image/bmp`|Bitmap images|
|`image/tiff`|TIFF images|
|`image/x-icon`|ICO icons|
|`image/vnd.microsoft.icon`|Microsoft icon format|
|`image/heic`|HEIC images|
|`image/heif`|HEIF images|
|`image/apng`|Animated PNG|
|`image/jxl`|JPEG XL images|

### 🎵 Audio

|Content-Type|Description|
|---|---|
|`audio/mpeg`|MP3 audio|
|`audio/mp4`|MP4 audio|
|`audio/aac`|AAC audio|
|`audio/ogg`|Ogg audio|
|`audio/opus`|Opus audio|
|`audio/wav`|WAV audio|
|`audio/webm`|WebM audio|
|`audio/flac`|FLAC audio|
|`audio/midi`|MIDI audio|
|`audio/x-m4a`|M4A audio (commonly used)|

### 🎬 Video

|Content-Type|Description|
|---|---|
|`video/mp4`|MP4 video|
|`video/webm`|WebM video|
|`video/ogg`|Ogg video|
|`video/mpeg`|MPEG video|
|`video/quicktime`|QuickTime video|
|`video/x-msvideo`|AVI video|
|`video/x-matroska`|Matroska / MKV video|
|`video/3gpp`|3GPP video|
|`video/mp2t`|MPEG transport stream|

### 📦 Forms, Uploads & Multipart

|Content-Type|Description|
|---|---|
|`multipart/form-data`|HTML forms and file uploads|
|`multipart/mixed`|Multiple parts of different types|
|`multipart/alternative`|Alternative representations|
|`multipart/related`|Related resources, often HTML and images|
|`multipart/byteranges`|Partial content ranges|

### 🔤 Fonts

|Content-Type|Description|
|---|---|
|`font/woff`|WOFF fonts|
|`font/woff2`|WOFF2 fonts|
|`font/ttf`|TrueType fonts|
|`font/otf`|OpenType fonts|
|`application/vnd.ms-fontobject`|Embedded OpenType fonts|

### 🔐 Security, Authentication & Cryptography

|Content-Type|Description|
|---|---|
|`application/jwt`|JWT (registered media type)|
|`application/jose`|JOSE objects|
|`application/jose+json`|JOSE JSON serialization|
|`application/pkcs8`|PKCS #8 private-key information|
|`application/pkcs10`|Certificate signing requests|
|`application/pkix-cert`|X.509 certificates|
|`application/pkix-crl`|Certificate revocation lists|
|`application/pgp-encrypted`|PGP encrypted data|
|`application/pgp-signature`|PGP signatures|
|`application/cose`|CBOR Object Signing and Encryption|
|`application/cbor`|CBOR binary data|

### 📡 Other Common Types

|Content-Type|Description|
|---|---|
|`model/gltf+json`|glTF 3D models in JSON|
|`model/gltf-binary`|Binary glTF models|
|`model/obj`|OBJ 3D models (commonly used, registration varies)|
|`chemical/x-pdb`|Legacy PDB chemical data|
|`application/geo+json`|GeoJSON data|
|`application/vnd.google-earth.kml+xml`|KML geographic data|
|`application/wasm`|WebAssembly binaries|

### 🧩 Content-Type Parameters

A media type may include parameters:

```js
Content-Type: application/json; charset=utf-8
Content-Type: text/html; charset=UTF-8
Content-Type: multipart/form-data; boundary=----FormBoundary123
```

**Important:** `application/json` normally uses UTF-8, and a `charset` parameter is generally unnecessary for JSON. Multipart boundaries are generated by the client library or browser when appropriate.

---

## 2. 🦊 User-Agent

The `User-Agent` request header historically identifies the client software, browser, version, and sometimes operating system.

### 🌐 Google Chrome

**Windows**

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36
```

**macOS**

```
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36
```

**Linux**

```
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36
```

**Android**

```
User-Agent: Mozilla/5.0 (Linux; Android 15; Pixel 9) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Mobile Safari/537.36
```

### 🦊 Mozilla Firefox

**Windows**

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:143.0) Gecko/20100101 Firefox/143.0
```

**macOS**

```
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:143.0) Gecko/20100101 Firefox/143.0
```

**Linux**

```
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:143.0) Gecko/20100101 Firefox/143.0
```

### 🧭 Microsoft Edge

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36 Edg/140.0.0.0
```

Edge includes Chromium-compatible tokens and the `Edg/` identifier.

### 🍎 Apple Safari

**macOS**

```
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.0 Safari/605.1.15
```

**iPhone**

```
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 18_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.0 Mobile/15E148 Safari/604.1
```

**iPad**

```
User-Agent: Mozilla/5.0 (iPad; CPU OS 18_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.0 Mobile/15E148 Safari/604.1
```

### 📱 Other Browsers

**Opera**

```
User-Agent: Mozilla/5.0 (...) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36 OPR/125.0.0.0
```

**Samsung Internet**

```
User-Agent: Mozilla/5.0 (Linux; Android 15; SM-S938B) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/28.0 Chrome/140.0.0.0 Mobile Safari/537.36
```

**Brave**

```
User-Agent: Mozilla/5.0 (...) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36
```

Brave commonly uses a Chrome-like User-Agent and may not explicitly identify itself in that string.

### 🖥️ Other Clients

**curl**

```
User-Agent: curl/8.10.0
```

**Python Requests**

```
User-Agent: python-requests/2.32.3
```

**Wget**

```
User-Agent: Wget/1.21.4
```

**Node.js**

```
User-Agent: node
```

**Googlebot**

```
User-Agent: Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)
```

**Bingbot**

```
User-Agent: Mozilla/5.0 (compatible; bingbot/2.0; +http://www.bing.com/bingbot.htm)
```

**Postman**

```
User-Agent: PostmanRuntime/7.43.0
```

**Insomnia**

```
User-Agent: insomnia/10.3.0
```

> [!warning] User-Agent examples Versions and tokens above are illustrative. Real strings vary by release, platform, configuration, and privacy settings. User-Agent strings can be spoofed and should not be treated as reliable proof of browser identity.

---

## 3. ⚡ JavaScript Fetch Examples

### Send JSON

```js
fetch("/api/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify({ name: "Alex" })
});
```

### Read a Response

```js
const response = await fetch("/api/data");

console.log(response.headers.get("Content-Type"));

const data = await response.json();
```

### Set a Custom User-Agent?

```js
fetch("/api/data", {
  headers: {
    "Content-Type": "application/json",
    "User-Agent": "MyCustomClient/1.0"
  }
});
```

> [!warning] Browser limitation Browsers prohibit JavaScript from freely setting the `User-Agent` header. The example above does **not** reliably override it in browser `fetch()`. In Node.js or other non-browser HTTP clients, custom User-Agent headers are generally possible.

---

