**Windows User, Password, and Group Policy – Essential Commands**

---

### 🔹 1. User Management

**Create a new user**

```
net user username password /add
```

**Create user without password**

```
net user username /add
```

**Delete a user**

```
net user username /delete
```

**List all users**

```
net user
```

**View user details**

```
net user username
```

---

### 🔹 2. Password Management

**Change a user's password**

```
net user username newpassword
```

**Force user to change password at next login**

```
net user username /logonpasswordchg:yes
```

**Set password to never expire**

```
wmic UserAccount where Name='username' set PasswordExpires=FALSE
```

---

### 🔹 3. Group Management

**Add user to Administrators group**

```
net localgroup Administrators username /add
```

**Remove user from Administrators group**

```
net localgroup Administrators username /delete
```

**List members of a group**

```
net localgroup Administrators
```

**Create a new local group**

```
net localgroup groupname /add
```

**Add user to a custom group**

```
net localgroup groupname username /add
```

---

### 🔹 4. Permissions (NTFS)

**Grant full control to a user on a folder**

```
icacls "C:\path\to\folder" /grant username:F
```

**Grant modify permission**

```
icacls "C:\path\to\folder" /grant username:M
```

**Remove permissions**

```
icacls "C:\path\to\folder" /remove username
```

**View current permissions**

```
icacls "C:\path\to\folder"
```

---

### 🔹 5. Group Policy (Local)

**Open Local Group Policy Editor**

```
gpedit.msc
```

**Update Group Policy**

```
gpupdate /force
```

**View applied policies**

```
gpresult /r
```

**Detailed policy report (HTML)**

```
gpresult /h report.html
```

---

### 🔹 6. Advanced (PowerShell Alternatives)

**Create new user**

```
New-LocalUser "username" -Password (ConvertTo-SecureString "password" -AsPlainText -Force)
```

**Add user to Administrators**

```
Add-LocalGroupMember -Group "Administrators" -Member "username"
```

**List local users**

```
Get-LocalUser
```

---

### 🔹 Notes

- Run commands in **Command Prompt (Admin)** or **PowerShell (Admin)**.
    
- Replace `username`, `password`, and paths with actual values.
    
- Some commands require administrative privileges.
    

---