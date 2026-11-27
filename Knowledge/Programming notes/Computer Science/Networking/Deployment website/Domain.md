# 🌐 Domain Names — Get & Set Up

> [!abstract] 🎯 Goal Learn how to buy a domain name, connect it to a server, and configure DNS records.

## 1. 🛒 Get a domain name

A **domain name** is your website's address.

Examples:

- `example.com`
- `myproject.dev`
- `mywebsite.es`

**Where to buy:**

- [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/)
- [Namecheap](https://www.namecheap.com/)
- [Porkbun](https://porkbun.com/)

💡 Choose a name, check availability, register it and enable auto-renewal.

## 2. ⚙️ Understand DNS

> **DNS (Domain Name System)** connects your domain to your server.

**Example:**

```d
mywebsite.com → 203.0.113.10
```

Think of DNS as the internet's phonebook.

## 3. 🔧 Configure DNS records

Open your domain registrar's DNS settings.

|Record|Purpose|Example|
|---|---|---|
|A|Domain → IPv4|`203.0.113.10`|
|AAAA|Domain → IPv6|`2001:db8::1`|
|CNAME|Alias → Domain|`www → mywebsite.com`|
|MX|Email server|`mail.example.com`|
|TXT|Verification / SPF|`v=spf1 ...`|

**Example configuration:**

```d
Type    Name    Value

A       @       203.0.113.10
CNAME   www     mywebsite.com
```

- `@` = root domain (`mywebsite.com`)
- `www` = subdomain (`www.mywebsite.com`)

_Replace example IPs with your actual server IP._

## 4. 🔗 Connect domain to hosting

Your hosting provider usually gives you one of two options:

**Option A — DNS records**

Add the A and CNAME records provided by your hosting provider.

**Option B — Nameservers**

Change your domain's nameservers to those provided by your DNS host.

```dns
ns1.provider.com
ns2.provider.com
```

> ⚠️ Nameserver changes transfer DNS management. Make sure existing email and other DNS records are preserved.

## 5. 🔒 Enable HTTPS (SSL)

HTTPS encrypts communication between visitors and your website.

A popular free option is [Let's Encrypt](https://letsencrypt.org/).

> Example using Certbot with Nginx:

```bash
sudo apt install certbot python3-certbot-nginx

sudo certbot --nginx -d mywebsite.com -d www.mywebsite.com
```

## 6. 🧪 Test your domain

Check whether DNS is resolving:

```bash
dig mywebsite.com
```

Check the HTTP response:

```bash
curl -I https://mywebsite.com
```

Check DNS propagation:

🌐 [https://dnschecker.org/](https://dnschecker.org/)

> DNS changes can take time to propagate, depending on caching and TTL settings.

---

## 🧠 Remember

```text
DOMAIN
   ↓
DNS RECORDS
   ↓
SERVER / HOSTING
   ↓
SSL CERTIFICATE
   ↓
🌐 YOUR WEBSITE
```

**Domain = Address**

**DNS = Connection**

**Hosting = Where your website lives**

**SSL = Secure connection**

✨ That's it! Your domain is registered, connected and ready to use.

---
