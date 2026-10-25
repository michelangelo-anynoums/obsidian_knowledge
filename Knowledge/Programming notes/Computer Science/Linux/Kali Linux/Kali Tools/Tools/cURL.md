# 🌐 cURL — Complete Cheat Sheet

> [!abstract] Overview **cURL** = Client URL  
> A CLI tool for downloading files, communicating with APIs, and transferring data over the network.

## 01 — ⚡ Basic Requests

```bash
# GET — retrieve a webpage
curl https://example.com

# Show response headers only
curl -I https://example.com

# Follow redirects
curl -L https://example.com

# Show detailed connection information
curl -v https://example.com

# Silent mode (hide progress and errors)
curl -s https://example.com

# Silent mode but still show errors
curl -sS https://example.com
```

## 02 — 📥 Download Files

### Basic download

```bash
# Save using the remote filename
curl -O https://example.com/file.zip

# Save with a custom filename
curl -o archive.zip https://example.com/file.zip
```

### Specify the destination folder

```bash
# Linux / macOS
curl -o ~/Downloads/file.zip https://example.com/file.zip

# Windows PowerShell
curl.exe -o "C:\Users\Alex\Downloads\file.zip" https://example.com/file.zip

# Linux / macOS — save into a specific directory
curl -o /home/alex/Documents/report.pdf https://example.com/report.pdf
```

> [!tip] Important `-o` specifies the **full destination path and filename**. The destination folder must already exist.

### Download into a folder using the original filename

```bash
# Linux / macOS
curl -o ~/Downloads/file.zip https://example.com/file.zip
```

If the server filename is known and you want to preserve it, use `-O` with a URL that includes the filename:

```bash
cd ~/Downloads
curl -O https://example.com/file.zip
```

### Follow redirects and download

```bash
curl -L -o app.zip https://example.com/download
```

### Resume an interrupted download

```bash
curl -C - -O https://example.com/large-file.zip
```

### Show download progress

```bash
curl --progress-bar -L -o file.zip https://example.com/file.zip
```

## 03 — 📤 Upload Files

```bash
# Upload a file using multipart form data
curl -F "file=@document.pdf" https://example.com/upload

# Upload with an additional field
curl -F "file=@photo.jpg" -F "description=My photo" \
  https://example.com/upload
```

> [!note] The server must support the upload endpoint and expected form fields.

## 04 — 🔗 HTTP Methods

### GET — retrieve data

```bash
curl https://api.example.com/users
```

### POST — create or submit data

```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Alex","age":25}'
```

### PUT — replace or update a resource

```bash
curl -X PUT https://api.example.com/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"John","age":30}'
```

### PATCH — partially update a resource

```bash
curl -X PATCH https://api.example.com/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"Alex"}'
```

### DELETE — delete a resource

```bash
curl -X DELETE https://api.example.com/users/1
```

> [!warning] Note These examples use placeholder API endpoints. Real servers may require authentication, different data fields, or specific permissions.

## 05 — 📨 Headers & Authentication

### Add a custom header

```bash
curl -H "Accept: application/json" \
  https://api.example.com/users
```

### Bearer token

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://api.example.com/users
```

### Basic authentication

```bash
curl -u username:password https://example.com/protected
```

### Custom User-Agent

```bash
curl -A "MyApp/1.0" https://example.com
```

> [!warning] Security Avoid putting real passwords or tokens directly in shell history. Never share credentials in notes or public repositories.

## 06 — 🧪 API Testing

### Pretty-print JSON

```bash
curl -sS https://api.example.com/users | jq .
```

### Display the HTTP status code

```bash
curl -sS -o /dev/null -w "%{http_code}\n" \
  https://example.com
```

### Display headers and response body

```bash
curl -i https://example.com
```

### Save the response to a file

```bash
curl -o response.json https://api.example.com/users
```

### Set a timeout

```bash
curl --connect-timeout 5 --max-time 15 https://example.com
```

- `--connect-timeout 5` — allow up to 5 seconds to establish a connection.
- `--max-time 15` — limit the entire transfer to 15 seconds.

## 07 — 🧰 Useful Flags

|Flag|Description|
|---|---|
|`-X`|Specify the HTTP method|
|`-H`|Add a request header|
|`-d`|Send request data|
|`-F`|Send multipart form data|
|`-I`|Fetch headers only|
|`-i`|Include response headers|
|`-L`|Follow redirects|
|`-O`|Save using the remote filename|
|`-o`|Save to a specified path|
|`-C -`|Resume a download|
|`-s`|Silent mode|
|`-S`|Show errors with silent mode|
|`-v`|Verbose output|
|`-u`|Basic authentication|
|`-A`|Set User-Agent|
|`-w`|Format output using transfer information|
|`-k`|Skip TLS certificate verification|
|`--max-time`|Set the total timeout|

## 08 — 🛠️ Troubleshooting

```bash
# Inspect the request and connection
curl -v https://example.com

# Check only the response headers
curl -I https://example.com

# Follow redirects
curl -L https://example.com

# Fail on HTTP errors (curl 7.76.0+)
curl --fail https://example.com

# Fail on HTTP errors without hiding error output
curl -sS --fail https://example.com
```

> [!warning] TLS certificates Avoid `-k` in production. It disables TLS certificate verification and can expose the connection to interception.

## 09 — 🧠 Quick Memory

|Goal|Command|
|---|---|
|Download a file|`curl -O URL`|
|Choose filename/path|`curl -o PATH URL`|
|Resume download|`curl -C - -O URL`|
|Send JSON|`curl -H "Content-Type: application/json" -d '{}' URL`|
|Follow redirects|`curl -L URL`|
|Check status code|`curl -sS -o /dev/null -w "%{http_code}\n" URL`|
|Debug connection|`curl -v URL`|

---
