# 🔐 Windows Hash Cracking

> ⚠️ For authorized labs, CTFs, and systems you own.

## 1. Windows Passwords 🔑

This applies primarily to **local Windows accounts**.

Windows does not store the plaintext password. Instead, it stores an **NT hash** (often casually called an _NTLM hash_).

```Bash
Password
   ↓
NT hashing
   ↓
NT hash
   ↓
Stored in SAM
```

When you log in, Windows takes the password you entered, calculates its NT hash, and compares it with the stored value.

```Bash
User types a password
			↓
Windows converts it to NT hash
			↓
Compare user password and stored NT hash
			↓
Stored NT hash == calculated user password?
			↓
Yes? Access granted!
No? Access denied!
```

### What is an NT hash?

An NT hash is essentially:

```text
MD4(UTF-16LE(password))
```

It is **not encryption** — it is a hash. However, NT hashes are relatively fast to calculate, which makes offline password cracking practical when a hash has been obtained.

📍 Local account information is stored in:

```text
C:\Windows\System32\config\SAM
```

The **SYSTEM** registry hive is also required when extracting the protected hashes:

```text
C:\Windows\System32\config\SYSTEM
```

> 💡 Domain accounts are different: their password hashes are normally handled by Active Directory rather than the local SAM.

---

## 2. Getting SAM + SYSTEM 🗄️

If you have sufficient administrative access, you can obtain copies of the:

```bash
reg save HKLM\sam.save sam.save
			↓
reg save HKLM\system.save system.save
```

registry hives and analyze them offline.

There are also classic techniques involving `utilman.exe` that abuse the Windows login screen to obtain SYSTEM-level access.

---

## 3. Extracting Hashes 💻

On Kali Linux, **Impacket** provides `secretsdump.py`.

For offline SAM + SYSTEM files:

```bash
impacket-secretsdump.py -sam sam.save -system system.save LOCAL
```

Result:

```bash
SAM + SYSTEM
     ↓
secretsdump
     ↓
Username : NT hash (LOCAL)
```

---

## 4. Cracking with Hashcat ⚡

Hashcat uses mode **1000** for NT hashes.

Example using a wordlist:

```bash
hashcat -m 1000 hashes.txt wordlist.txt
```

The basic idea:

```text
Candidate password
        ↓
    NT hash
        ↓
   Compare with
   target hash
        ↓
      Match ✓
```

Useful attack types include:

- 📖 Dictionary
    
- 🧩 Rules
    
- 🎭 Mask
    
- 🔨 Brute force
    

---

## 5. The Whole Process 🚀

```text
Windows local account
        ↓
      SAM
        ↓
   SAM + SYSTEM
        ↓
   secretsdump
        ↓
     NT hash
        ↓
     Hashcat
        ↓
 Password recovered
```

---
