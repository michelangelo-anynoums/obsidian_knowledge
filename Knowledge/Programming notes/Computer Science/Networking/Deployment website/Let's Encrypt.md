# 🔒 HTTPS — Setup & Configuration

> HTTPS secures communication between a browser and a website using TLS encryption and a digital certificate.

## 🧠 1. How it works


```
Browser 🌐
    │
    │ HTTPS (TLS encryption)
    ▼
Web Server
    │
    ▼
Website
```

- **HTTPS** → HTTP protected by TLS.
- **TLS Certificate** → Proves the website's identity.
- **Private Key** → Secret key stored on the server.
- **Public Key** → Included in the certificate.
- **Port 443** → Default HTTPS port.

## 📦 2. Requirements

You need:

- A domain name (e.g. `example.com`).
- A web server (Nginx or Apache).
- A server with a public IP.
- DNS pointing to your server.
- Ports `80` and `443` accessible.

## 🔑 3. Install Certbot

Certbot obtains and renews free TLS certificates from Let's Encrypt.

**Ubuntu / Debian (APT):**

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

For Apache:

```bash
sudo apt install certbot python3-certbot-apache -y
```

## 🌐 4. Configure DNS

Create DNS records at your domain provider:

|Type|Name|Value|
|---|---|---|
|A|@|SERVER_PUBLIC_IP|
|A|www|SERVER_PUBLIC_IP|

Example:

```
example.com      → 203.0.113.10
www.example.com  → 203.0.113.10
```

Replace the example IP with your actual server IP.

## ⚙️ 5. Configure Nginx

Create a website configuration:

```bash
sudo nano /etc/nginx/sites-available/example.com
```

Example HTTP configuration:

```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html;
    index index.html;
}
```

Enable the website:

```bash
sudo ln -s \
/etc/nginx/sites-available/example.com \
/etc/nginx/sites-enabled/
```

Test and reload:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 🔐 6. Generate an HTTPS certificate

For Nginx:

```bash
sudo certbot --nginx \
-d example.com \
-d www.example.com
```

For Apache:

```bash
sudo certbot --apache \
-d example.com \
-d www.example.com
```

Certbot will obtain the certificate and configure HTTPS.

## 🚀 7. Verify HTTPS

Open:

```
https://example.com
```

Check the certificate:

```bash
sudo certbot certificates
```

Test the HTTPS connection:

```bash
curl -I https://example.com
```

Check TLS using OpenSSL:

```bash
openssl s_client \
-connect example.com:443 \
-servername example.com
```

## 🔄 8. Automatic renewal

Let's Encrypt certificates are valid for 90 days.

Check automatic renewal:

```bash
sudo certbot renew --dry-run
```

Manually renew:

```bash
sudo certbot renew
```

💡 Certbot normally installs automatic renewal through a systemd timer or cron, depending on installation method.

## 🛡️ 9. Firewall configuration

Allow HTTP and HTTPS:

**UFW:**

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw status
```

Remember: TCP port `443` is used for HTTPS.

## 🔍 10. Troubleshooting

|Problem|Possible cause|
|---|---|
|Certificate error|Invalid or expired certificate|
|Connection refused|Port 443 blocked|
|Domain not found|Incorrect DNS records|
|Certbot failure|DNS or HTTP validation problem|
|Redirect loop|Incorrect proxy or HTTPS configuration|

Useful commands:

```bash
sudo nginx -t
sudo systemctl status nginx
sudo journalctl -u nginx
sudo certbot certificates
```

## 📌 11. Remember

- 🔒 HTTPS = HTTP + TLS.
- 🌐 Default HTTPS port = `443`.
- 🔑 Private keys must remain secret.
- 📜 Let's Encrypt provides free certificates.
- 🔄 Certificates need renewal.
- 🚀 Certbot automates certificate management.
- 🛡️ Use HTTPS for websites, APIs and login pages.

## 📂 Useful paths

```
/etc/letsencrypt/
├── live/
│   └── example.com/
│       ├── fullchain.pem
│       └── privkey.pem
│
└── renewal/
    └── example.com.conf
```

**Useful commands:**

```bash
sudo certbot certificates
sudo certbot renew
sudo nginx -t
sudo systemctl reload nginx
```

**Official resources:**

- Let's Encrypt: [https://letsencrypt.org/](https://letsencrypt.org/)
- Certbot: [https://certbot.eff.org/](https://certbot.eff.org/)
- Nginx: [https://nginx.org/](https://nginx.org/)
- Mozilla TLS configuration: https://ssl-config.mozilla.org/

---
