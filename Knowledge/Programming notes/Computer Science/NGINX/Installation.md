# 🐧 Ubuntu Server + NGINX — First Setup

> [!abstract] Goal Install Ubuntu Server, prepare the system, install NGINX and publish a simple website.

## 1. 💿 Download Ubuntu Server

Official download:

🔗 [https://ubuntu.com/download/server](https://ubuntu.com/download/server)

- Download the Ubuntu Server LTS ISO.
- Create a bootable USB using [Rufus](https://rufus.ie/) or [Balena Etcher](https://etcher.balena.io/).
- Boot your computer or virtual machine from the USB/ISO.
- Follow the Ubuntu installation wizard.

💡 For learning, you can also install Ubuntu Server inside VirtualBox.

## 2. ⚙️ Install Ubuntu Server

During installation:

1. Select language and keyboard.
2. Configure network (DHCP is fine for beginners).
3. Choose storage and install Ubuntu.
4. Create your username and password.
5. Enable OpenSSH Server if you want remote access.
6. Finish installation and reboot.

## 3. 🔐 First login

Log in with your credentials.

Check Ubuntu version:

```bash
lsb_release -a
```

Check IP address:

```bash
ip addr
```

Check available disk space:

```bash
df -h
```

## 4. 🔄 Update Ubuntu

Always update the system first.

```bash
sudo apt update
sudo apt upgrade -y
```

Install useful tools:

```bash
sudo apt install curl wget nano git ufw -y
```

## 5. 🔥 Configure firewall

Enable SSH before enabling the firewall if you use remote access.

```bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

sudo ufw enable
sudo ufw status
```

- `22` → SSH
- `80` → HTTP
- `443` → HTTPS

## 6. 🌐 Install NGINX

Install:

```bash
sudo apt install nginx -y
```

Start and enable:

```bash
sudo systemctl enable --now nginx
```

Check status:

```bash
sudo systemctl status nginx
```

Test configuration:

```bash
sudo nginx -t
```

## 7. 🧪 Test NGINX

Find your server IP:

```bash
hostname -I
```

Open your browser:

```http
http://YOUR_SERVER_IP
```

You should see the default NGINX welcome page.

## 8. 📁 Create your first website

Create a directory:

```bash
sudo mkdir -p /var/www/mywebsite
```

Create an HTML file:

```bash
sudo nano /var/www/mywebsite/index.html
```

Add:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First Website</title>
</head>
<body>
    <h1>Hello from Ubuntu! 🚀</h1>
    <p>NGINX is working correctly.</p>
</body>
</html>
```

Save with `CTRL + O`, Enter, then `CTRL + X`.

## 9. ⚙️ Configure NGINX

Create a server configuration:

```bash
sudo nano /etc/nginx/sites-available/mywebsite
```

Add:

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/mywebsite;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Enable the website:

```bash
sudo ln -s /etc/nginx/sites-available/mywebsite \
/etc/nginx/sites-enabled/
```

Disable the default website:

```bash
sudo rm /etc/nginx/sites-enabled/default
```

Test and reload:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 10. ✅ Final test

Open:

```bash
http://YOUR_SERVER_IP
```

You should see:

```text
**Hello from Ubuntu! 🚀**

Your first website is online!
```

## 11. 🛠️ Useful NGINX commands

|Command|Purpose|
|---|---|
|`sudo systemctl start nginx`|Start|
|`sudo systemctl stop nginx`|Stop|
|`sudo systemctl restart nginx`|Restart|
|`sudo systemctl reload nginx`|Reload config|
|`sudo systemctl status nginx`|Check status|
|`sudo nginx -t`|Test configuration|

View logs:

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

---

## 🧠 Understand what you built

```
       🌍 INTERNET / BROWSER
                 |
                 | HTTP :80
                 |
          🐧 UBUNTU SERVER
                 |
              NGINX
                 |
          /var/www/mywebsite
                 |
              index.html
```

|Component|Function|
|---|---|
|Ubuntu Server|Operating system|
|SSH|Remote server access|
|UFW|Firewall|
|NGINX|Web server|
|HTML|Website content|

> [!tip] Remember Ubuntu runs the server, NGINX handles incoming web requests, and HTML provides the content.


---
