**VeraCrypt – Short Overview + Basic Usage**

VeraCrypt is a free, open-source disk encryption software designed to secure data using strong cryptographic algorithms. It is the successor to TrueCrypt and improves on its security while maintaining similar functionality.

It allows users to:

- Create encrypted file containers (virtual drives)
    
- Encrypt entire partitions or USB drives
    
- Encrypt full system disks (including OS)
    
- Use hidden volumes for plausible deniability
    

Supported encryption algorithms include AES, Serpent, and Twofish (individually or combined).

---

**Installation (All Operating Systems)**

1. Go to the official website: [https://www.veracrypt.fr](https://www.veracrypt.fr/)
    
2. Download the version for your OS:
    
    - **Windows**: `.exe` installer
        
    - **macOS**: `.dmg` file
        
    - **Linux**: `.tar.bz2` or use package manager
        

**Windows**

- Run the installer
    
- Choose “Install”
    
- Follow setup wizard
    

**macOS**

- Open `.dmg`
    
- Drag VeraCrypt to Applications
    
- Install macFUSE if prompted (required)
    

**Linux**

- Extract archive OR install via package manager:
    
    - Ubuntu/Debian: `sudo apt install veracrypt`
        
    - Fedora: `sudo dnf install veracrypt`
        

---

**Basic Steps: Create an Encrypted Container**

1. Open VeraCrypt
    
2. Click **Create Volume**
    
3. Select **Create an encrypted file container**
    
4. Choose **Standard VeraCrypt volume**
    
5. Select file location and name
    
6. Choose encryption algorithm (AES is default)
    
7. Set volume size
    
8. Create a strong password
    
9. Format the volume (select filesystem)
    
10. Click **Format**
    

---

**Mount (Use) the Encrypted Volume**

1. Open VeraCrypt
    
2. Select a drive letter
    
3. Click **Select File** and choose your container
    
4. Click **Mount**
    
5. Enter your password
    

→ The encrypted volume now appears as a normal drive.

---

**Dismount**

- In VeraCrypt, select the mounted volume
    
- Click **Dismount**
    

---

**Notes**

- Always use a strong password (long + unique)
    
- Back up important data (encryption loss = data loss)
    
- Hidden volumes can be used for additional privacy
    

---

**Use Case Tip (Obsidian)**  
You can store your Obsidian vault inside a VeraCrypt container to keep your notes fully encrypted when not mounted.