## 🔐 SSH (Secure Shell) – Short Introduction

**SSH (Secure Shell)** is a secure network protocol used to **remotely access and control another computer over a network**. It encrypts all communication, making it safe from eavesdropping and tampering. SSH is widely used by system administrators, developers, and cybersecurity professionals to manage servers, transfer files, and automate tasks.

SSH works on a **client–server model**:

- **Client** = your computer (where you type commands)
    
- **Server** = the remote machine you connect to
    

By default, SSH uses **TCP port 22**.

---

## 🧠 Very Important SSH Concepts (Basics)


- **Encryption** – Protects data during transfer
    
- **Authentication** – Proves who you are (password or key-based)
    
- **SSH Keys** – A more secure login method using public/private keys
    
- **Port** – Default port: 22 (can be changed for security)
    

---

## Essential SSH Commands (Linux / Kali)

These are the core commands beginners must know:

### 1. Connect to a remote system

`ssh username@ip_address`

Example:

`ssh root@192.168.1.10`

---

### 2. Connect using a custom port

`ssh -p 2222 username@ip_address`

---

### 3. Generate SSH key pair

`ssh-keygen`

---

### 4. Copy your public key to a server

`ssh-copy-id username@ip_address`

---

### 5. Check SSH service status (on Linux)

`sudo systemctl status ssh`

---

### 6. Start SSH service

`sudo systemctl start ssh`

---

### 7. Stop SSH service

`sudo systemctl stop ssh`

---

## Using SSH on **Windows 11**

❗ SSH is **NOT Linux-only** — Windows 11 supports SSH natively.

### Option 1: Built-in SSH in Windows 11 (Recommended)

Windows 11 already includes an SSH client.

Open **PowerShell** or **Command Prompt** and type:

`ssh username@ip_address`

Example:

`ssh kali@192.168.1.100`

If it works, SSH is already installed.