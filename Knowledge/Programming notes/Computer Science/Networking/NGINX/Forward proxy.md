# 🌐 Nginx Forward Proxy — Reference Guide

> [!abstract] Overview A **forward proxy** allows clients to access external websites through an Nginx server.
> 
> Nginx supports:
> 
> - ✅ **HTTP forwarding** — available in stock Nginx.
> - 🔒 **HTTPS tunneling (CONNECT)** — requires an additional module or native tunnel support.

![[Pasted image 20261118072036.png|489]]

---

## 🌍 1. HTTP Forward Proxy — Stock Nginx

### ⚙️ Configuration

```nginx
server {
    listen 8888;
    resolver 8.8.8.8;

    location / {
        proxy_pass http://$http_host$request_uri;
        proxy_set_header Host $http_host;
        
        # Optional
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### 📝 Directive Explanation

| Directive                                  | Purpose                                                                      |
| ------------------------------------------ | ---------------------------------------------------------------------------- |
| `listen 8888`                              | Port clients use for proxy connections.                                      |
| `resolver 8.8.8.8`                         | Runtime DNS resolution, required because `$http_host` is dynamic.            |
| `proxy_pass http://$http_host$request_uri` | Reconstructs the target URL using the client's Host header and original URI. |


### 🧪 Testing

**Test HTTP forwarding:**

```bash
curl -x http://127.0.0.1:8888 http://example.com
```

**Check the proxy's public IP:**

```bash
curl -x http://127.0.0.1:8888 http://ifconfig.me
```

> [!tip] Expected result The second command should display the public IP address of the proxy server.

---

## 🔒 3. HTTPS Tunneling — Open Source Module

### 📌 Why is an additional module needed?

> [!question] Stock Nginx does not handle the HTTP `CONNECT` method.
When a client requests an HTTPS connection, it sends:

```http
CONNECT example.com:443 HTTP/1.1
```

Stock Nginx typically responds:

```http
HTTP/1.1 405 Method Not Allowed
```

**Solution:** Use the community module:

🔗 [chobits/ngx_http_proxy_connect_module](https://github.com/chobits/ngx_http_proxy_connect_module)

> [!abstract] This module adds CONNECT tunneling support to open-source Nginx.

### 🛠️ Build and Installation

**Step 1 — Download the source code**

```bash
# Option 1
wget https://nginx.org/download/nginx-1.27.0.tar.gz
tar -xzf nginx-1.27.0.tar.gz

# Option 2
git clone https://github.com/chobits/ngx_http_proxy_connect_module
```

**Step 2 — Apply the patch and compile**

Choose the patch that matches your Nginx version.

```bash
cd nginx-1.27.0

patch -p1 < ../ngx_http_proxy_connect_module/patch/proxy_connect_rewrite_102101.patch

./configure --add-module=../ngx_http_proxy_connect_module

make && make install
```

> [!warning] Important — Patch selection The patch version must match your Nginx source version.
> 
> Check the module's README for the correct version-to-patch mapping.
> 
> The `_rewrite_` variant enables `set` / `rewrite_by_lua` in the CONNECT path.

### ⚙️ Configuration

```nginx
server {
    listen 8888;
    resolver 8.8.8.8;

    # --- HTTPS CONNECT tunnel ---
    proxy_connect;

    proxy_connect_allow            443 563;
    proxy_connect_connect_timeout  10s;
    proxy_connect_read_timeout     10s;
    proxy_connect_send_timeout     10s;

    # --- Plain HTTP forwarding ---
    location / {
        proxy_pass http://$http_host$request_uri;
        proxy_set_header Host $http_host;
    }
}
```

### 📝 Directive Explanation

|Directive|Purpose|
|---|---|
|`proxy_connect`|Enables the CONNECT method handler.|
|`proxy_connect_allow 443 563`|Whitelists upstream ports that the tunnel can access.|
|`proxy_connect_connect_timeout`|Connection timeout.|
|`proxy_connect_read_timeout`|Tunnel read timeout.|
|`proxy_connect_send_timeout`|Tunnel send timeout.|

### 🧪 Testing HTTPS Tunneling

```bash
curl -v -x http://127.0.0.1:8888 https://example.com
```

**Expected output (simplified):**

```test
> CONNECT example.com:443 HTTP/1.1
< HTTP/1.1 200 Connection Established
* TLS 1.3 connection established
```

### 🌐 Browser Configuration

Set your system or browser proxy to:

```http
http://127.0.0.1:8888
```

Both HTTP and HTTPS traffic can now use the proxy.

---

## 🚀 4. Native HTTPS Tunneling — `tunnel_pass`

**Available in NGINX Plus and supported Nginx 1.31+ builds.**

> [!important] Starting with Nginx 1.31.0, native CONNECT pass-through is available through the `ngx_http_tunnel_module`.
No third-party patching is required.

### ⚙️ Configuration

```bash
server {
    listen 3128;

    # --- Access control ---
    allow 10.0.0.0/8;
    allow 127.0.0.1;
    deny all;

    # --- Native CONNECT tunnel ---
    tunnel_pass;
}
```

### 🔍 How It Works

By default, `tunnel_pass` forwards traffic to:

```http
$host:$request_port
```

> [!important] The client's CONNECT target is used automatically.
You can further restrict upstream destinations using:

```nginx
tunnel_allow_upstream $allowed_networks $allowed_port $allowed_host;
```

> [!warning] Important `tunnel_pass` is available in NGINX Plus and in applicable open-source Nginx 1.31+ builds.
> 
> For open-source builds, verify that the module is compiled in:
> 
> 
> ```
> nginx -V
> ```
> 
> Look for:
> 
> 
> ```
> --with-http_tunnel_module
> ```

---

## 🛡️ 5. Security Hardening

> [!danger] Security Warning An open forward proxy can be abused by unauthorized users.
> 
> Never expose a forward proxy publicly without appropriate access controls.

### 🔐 Recommended Security Measures

|Control|Configuration|
|---|---|
|IP Whitelist|`allow` / `deny`|
|Authentication|`auth_basic` + `htpasswd`|
|Port Restriction|`proxy_connect_allow`|
|Domain Blocklist|`map $http_host` + access rules|
|TLS on Proxy Link|`listen 8888 ssl` + client certificate verification|

### ⚙️ Example Configuration


```nginx
server {
    listen 8888;

    # --- Access control ---
    allow 10.0.0.0/8;
    allow 127.0.0.1;
    deny all;

    # --- Basic authentication ---
    auth_basic "Proxy";
    auth_basic_user_file /etc/nginx/.htpasswd;

    # --- DNS ---
    resolver 8.8.8.8;

    # --- HTTPS tunneling ---
    proxy_connect;
    proxy_connect_allow 443;

    proxy_connect_connect_timeout 10s;
    proxy_connect_read_timeout 10s;
    proxy_connect_send_timeout 10s;

    # --- HTTP forwarding ---
    location / {
        proxy_pass http://$http_host$request_uri;
        proxy_set_header Host $http_host;
    }
}
```

> [!tip] Security Checklist
> 
> - [ ] Restrict access to trusted IP addresses.
> - [ ] Enable authentication where appropriate.
> - [ ] Restrict allowed CONNECT ports.
> - [ ] Consider blocking unwanted destination domains.
> - [ ] Use TLS when clients connect over an untrusted network.
> - [ ] Test access controls before exposing the proxy.

---

## 🔗 References

- [Nginx Official Documentation](https://nginx.org/en/docs/)
- [ngx_http_proxy_connect_module — GitHub](https://github.com/chobits/ngx_http_proxy_connect_module)
- [Nginx Download](https://nginx.org/en/download.html)


