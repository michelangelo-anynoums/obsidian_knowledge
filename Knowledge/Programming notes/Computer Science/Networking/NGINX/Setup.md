# 🌐 NGINX — Quick Teaching Notes

> [!abstract] What is NGINX? **NGINX** is a web server that can also work as a reverse proxy, load balancer, and HTTP cache.

![[Pasted image 20261107071958.png|532]]

> [!question] Where to download?
>  Official reference: [download NGINX](https://nginx.org/)
## 1. ⚙️ Basic commands

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl status nginx
```

Check configuration:

```bash
sudo nginx -t
```

## 2. 📁 Important paths

|Path|Purpose|
|---|---|
|`/etc/nginx/`|Main configuration|
|`/etc/nginx/nginx.conf`|Main config file|
|`/etc/nginx/sites-available/`|Available websites|
|`/etc/nginx/sites-enabled/`|Enabled websites|
|`/var/www/html/`|Default web content|
|`/var/log/nginx/`|Access and error logs|

## 3. 🧱 Basic server block

A **server block** defines how NGINX handles requests for a website.

```nginx
server {
    listen 80;
    server_name example.com;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- `listen`: Port to accept connections.
- `server_name`: Domain name.
- `root`: Website directory.
- `index`: Default page.
- `location`: Rules for specific URLs.
- `try_files`: Checks whether requested files exist.

## 4. 🔀 Reverse proxy

A reverse proxy receives client requests and forwards them to an application server.

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:3000;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

> [!important] 💡 Example: NGINX receives traffic on port `80` and forwards it to a Node.js application on port `3000`.

## 5. 📍 Location rules

Control how NGINX handles different URL paths.

```nginx
location / {
    # Default route
}

location /images/ {
    root /var/www;
}

location /api/ {
    proxy_pass http://127.0.0.1:3000;
}

location = /health {
    return 200 "OK";
}
```

Common modifiers:

|Modifier|Meaning|
|---|---|
|`=`|Exact match|
|`^~`|Prefer prefix match|
|`~`|Case-sensitive regex|
|`~*`|Case-insensitive regex|

## 6. ⚖️ Load balancing

Distributes incoming requests across multiple application servers.

```nginx
upstream backend {
    server 127.0.0.1:3000;
    server 127.0.0.1:3001;
    server 127.0.0.1:3002;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend;
    }
}
```

> [!important] 💡 NGINX distributes requests between the configured servers.

## 7. 🔒 HTTPS basics

Redirect HTTP traffic to HTTPS:

```nginx
server {
    listen 80;
    server_name example.com;

    return 301 https://$host$request_uri;
}
```

HTTPS server:

```nginx
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /etc/ssl/cert.pem;
    ssl_certificate_key /etc/ssl/key.pem;
}
```

## 8. 🛠️ Configuration workflow

After modifying a configuration file:

```bash
# 1. Test configuration
sudo nginx -t

# 2. Reload NGINX
sudo systemctl reload nginx

# 3. Check status
sudo systemctl status nginx
```

View logs:

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

## 🧠 Remember

|Concept|Purpose|
|---|---|
|Web server|Serves static files|
|Reverse proxy|Forwards requests to applications|
|Load balancer|Distributes traffic|
|SSL/TLS|Encrypts connections|
|Server block|Defines website configuration|
|Location|Defines URL handling rules|
|Upstream|Defines backend servers|

**NGINX = Web Server + Reverse Proxy + Load Balancer**

> [!fire] 📌 Main idea: NGINX sits between clients and backend applications, controlling how requests are received, processed, and forwarded.

---
