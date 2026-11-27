# 🌐 NGINX + Let's Encrypt + Domain Name

> [!abstract] 🎯 Goal Set up an NGINX web server accessible through a domain name, secured with a free SSL/TLS certificate from Let's Encrypt.

## 1. 🌍 Domain configuration

First, point your domain to your public IP address.

**DNS records:**

| Type | Name  | Value            |
| ---- | ----- | ---------------- |
| A    | `@`   | `YOUR_PUBLIC_IP` |
| A    | `www` | `YOUR_PUBLIC_IP` |

Example:

```d
example.com      → 203.0.113.10
www.example.com  → 203.0.113.10
```

_Wait for DNS propagation before continuing._

## 2. 📦 Install NGINX

```bash
sudo apt update
sudo apt install nginx -y
```

Start and enable NGINX:

```bash
sudo systemctl enable --now nginx
```

Check its status:

```bash
sudo systemctl status nginx
```

## 3. 📁 Create website directory

```bash
sudo mkdir -p /var/www/example.com/html
```

Create a simple website:

```bash
sudo nano /var/www/example.com/html/index.html
```

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Website</title>
</head>
<body>
    <h1>Hello from NGINX! 🚀</h1>
</body>
</html>
```

## 4. ⚙️ Configure NGINX

Create a virtual host:

```bash
sudo nano /etc/nginx/sites-available/example.com
```

Add the configuration:

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name example.com www.example.com;

    root /var/www/example.com/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Enable the website:

```bash
sudo ln -s /etc/nginx/sites-available/example.com \
/etc/nginx/sites-enabled/
```

Test and reload:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 5. 🔐 Install Let's Encrypt

Install Certbot and its NGINX plugin:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Request your SSL certificate:

```bash
sudo certbot --nginx \
-d example.com \
-d www.example.com
```

Certbot automatically:

- Obtains the certificate.
- Configures HTTPS in NGINX.
- Installs the certificate paths.
- Can enable HTTP → HTTPS redirection.

## 6. 🔑 Certificate locations

Let's Encrypt stores certificates here:

```text
/etc/letsencrypt/live/example.com/
```

Important files:

|File|Purpose|
|---|---|
|`fullchain.pem`|SSL certificate + intermediate certificates|
|`privkey.pem`|Private key|
|`cert.pem`|Domain certificate|
|`chain.pem`|Intermediate certificate chain|

> Typical NGINX HTTPS configuration:

```nginx|
server {
    listen 443 ssl;
    listen [::]:443 ssl;

    server_name example.com www.example.com;

    root /var/www/example.com/html;
    index index.html;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

_Certbot normally adds this configuration automatically when using the NGINX plugin._

## 7. ♻️ Automatic certificate renewal

Let's Encrypt certificates are short-lived, so automatic renewal is important.

> Check renewal:

```bash
sudo certbot renew --dry-run
```

Check the renewal timer:

```bash
systemctl status certbot.timer
```

Certbot normally installs automatic renewal through a systemd timer or another scheduled mechanism.

## 8. 🧪 Final tests

Check NGINX:

```bash
sudo nginx -t
```

Check HTTPS:

```bash
curl -I https://example.com
```

Check certificate details:

```bash
sudo certbot certificates
```

Open your browser:

```
https://example.com
```

---

## 🧠 Final architecture

```
       🌍 INTERNET
              |
              v
        example.com
              |
              v
          PUBLIC IP
              |
              v
          🔥 NGINX
            SERVER
              |
       +------+------+
       |             |
       v             v
    HTTP :80     HTTPS :443
       |             |
       |        🔐 SSL/TLS
       |        Let's Encrypt
       |             |
       +------+------+
              |
              v
       /var/www/example.com/
              |
              v
          index.html
```

> [!success] ✅ Result Your website is now accessible through your own domain name using HTTPS, with NGINX serving the website and Let's Encrypt providing the SSL/TLS certificate.

**Remember:** Keep your private key (`privkey.pem`) secure. Never share it or expose it publicly.

---
