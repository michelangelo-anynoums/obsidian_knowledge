![[Pasted image 20260829125459.png|636]]

---

# Hashcat — Quick Resume

**Hashcat** is a command-line password recovery and auditing tool. It can test candidate passwords against password hashes using different attack techniques and is commonly used by security professionals to assess password strength.

> **Important:** Only use Hashcat on hashes you own or have explicit permission to audit.

## 1. Basic Syntax

```bash
hashcat [options] hashfile [wordlist]
```

A typical command looks like:

```bash
hashcat -m 0 -a 0 hashes.txt passwords.txt
```

- `-m` = hash mode
- `-a` = attack mode
- `hashes.txt` = file containing hashes
- `passwords.txt` = candidate password list

## 2. Find Hash Modes

List available hash types:

```bash
hashcat --example-hashes
```

You can also search the output for the hash type you're working with.

For example, **MD5** uses mode:

```text
0
```

So an MD5 audit could be:

```bash
hashcat -m 0 -a 0 hashes.txt passwords.txt
```

## 3. Attack Modes

The most important attack modes are:

### Dictionary attack — `-a 0`

Tests passwords from a wordlist:

```bash
hashcat -m 0 -a 0 hashes.txt passwords.txt
```

### Brute-force / mask attack — `-a 3`

Tests candidates matching a defined pattern:

```bash
hashcat -m 0 -a 3 hashes.txt '?d?d?d?d'
```

Here `?d` represents a digit, so the example tests four-digit candidates.

Useful built-in mask characters include:

```text
?l  lowercase letters
?u  uppercase letters
?d  digits
?s  special characters
?a  all supported character classes
```

Example:

```bash
hashcat -m 0 -a 3 hashes.txt '?u?l?l?l?d?d'
```

This represents a six-character pattern such as an uppercase letter, three lowercase letters, followed by two digits.

## 4. Show Recovered Passwords

After a successful recovery, display the results with:

```bash
hashcat -m 0 hashes.txt --show
```

The output generally contains the original hash and its recovered password.

## 5. Check Hashcat Status

While Hashcat is running, press:

```text
s
```

This displays information such as progress, speed, estimated time, and current attack status.

Other useful controls include:

```text
p    pause
r    resume
q    quit
```

## 6. Benchmark Your System

To see how fast your system can process different hash algorithms:

```bash
hashcat -b
```

This is useful for understanding available CPU/GPU performance before an authorized audit.

---

# Hashcat – Rules Usage

## What Are Rules?

Hashcat **rules** modify words from a wordlist to generate additional password candidates.

For example:

```text
password
```

can become:

```text
Password
password1
password123
password!
Password123
```

This can make a dictionary attack much more effective without needing a huge wordlist.

---

## Basic Usage

Use the `-r` option:

```bash
hashcat -m 22000 -a 0 handshake.hc22000 wordlist.txt -r rules/best64.rule
```

Common built-in rule files are located under:

```text
/usr/share/hashcat/rules/
```

For example:

```bash
ls /usr/share/hashcat/rules/
```

---

## Useful Example

Using the `best64.rule` ruleset:

```bash
hashcat -m 22000 -a 0 handshake.hc22000 /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule
```

This takes each word from `rockyou.txt` and applies the transformations defined in `best64.rule`.

---

## Quick Tips

- `-r` → apply a rules file.
- `best64.rule` → a good starting point for basic password auditing.
- Rules can greatly increase the number of candidates generated.
- More rules ≠ always better — larger rulesets can take considerably longer.
- You can use your own custom `.rule` file if needed.

### Simple Workflow

```text
Wordlist
   ↓
Rules
   ↓
Modified Password Candidates
   ↓
Hashcat
```

> [!tip] Start simple  
> Try `best64.rule` first. If that doesn't produce results, consider a larger or more targeted ruleset.

---

# Hashcat – Custom Charsets

## What Are Custom Charsets?

Hashcat lets you create your own character groups with `-1`, `-2`, `-3`, and `-4`.

These are useful with **mask attacks** (`-a 3`) when you want to control which characters can appear in each position.

### Built-in Character Sets

|Symbol|Meaning|
|---|---|
|`?l`|lowercase letters|
|`?u`|uppercase letters|
|`?d`|digits|
|`?s`|special characters|
|`?a`|all printable characters|
|`?b`|all bytes|

---

## Custom Groups

Define a custom charset with `-1`, `-2`, `-3`, or `-4`.

For example:

```bash
-1 ?d?d?d
```

This defines charset `?1` using the characters represented by three digit character sets.

Then use it in the mask:

```bash
?1?1?1
```

The general structure is:

```text
-1 <characters>   →  ?1
-2 <characters>   →  ?2
-3 <characters>   →  ?3
-4 <characters>   →  ?4
```

---

## Example

Suppose you want to test a pattern where the password consists of:

```text
3 digits + 3 lowercase letters
```

You could define:

```bash
-1 ?d
-2 ?l
```

and use:

```bash
?1?1?1?2?2?2
```

Complete example:

```bash
hashcat -m 22000 -a 3 handshake.hc22000 -1 ?d -2 ?l ?1?1?1?2?2?2
```

---

## Combining Character Sets

You can combine built-in sets when defining a custom charset.

For example:

```bash
-1 ?l?u
```

means `?1` contains lowercase **and** uppercase letters.

Then:

```bash
?1?1?1
```

tests three positions using that custom character set.

Another example:

```bash
-1 ?d?s
```

means `?1` contains digits and special characters.

---

## Quick Reference

```text
-1 ?d       → ?1 = digits
-2 ?l       → ?2 = lowercase
-3 ?u       → ?3 = uppercase
-4 ?s       → ?4 = special characters
```

Example pattern:

```text
-1 ?d -2 ?l
?1?1?1?2?2?2
```

Think of `-1` through `-4` as **named character groups**, and `?1` through `?4` as the groups you place inside the mask.

> [!tip] Easy way to remember  
> `-1` **defines** the group → `?1` **uses** the group.

# Hashcat – Mask Length Boundaries

## Testing a Range of Password Lengths

Use `--increment` when you want Hashcat to test multiple password lengths.

For example, to test **8–10 characters**:

```bash
hashcat -m 22000 -a 3 \
  --increment \
  --increment-min 8 \
  --increment-max 10 \
  handshake.hc22000 '?a?a?a?a?a?a?a?a?a?a'
```

Hashcat will try:

```text
8 characters
9 characters
10 characters
```

## Options

|Option|Meaning|
|---|---|
|`--increment`|Enable variable-length masks|
|`--increment-min 8`|Minimum length = 8|
|`--increment-max 10`|Maximum length = 10|

## With Custom Charsets

You can combine this with `-1` through `-4`:

```bash
hashcat -m 22000 -a 3 \
  -1 ?l?u?d \
  --increment \
  --increment-min 8 \
  --increment-max 10 \
  handshake.hc22000 '?1?1?1?1?1?1?1?1?1?1'
```

### Remember

```text
--increment-min 8
        ↓
   8 characters
        ↓
   9 characters
        ↓
  10 characters
        ↓
--increment-max 10
```

> [!tip] Simple rule  
> `--increment-min` = where to **start**  
> `--increment-max` = where to **stop**
# hcxtools – Installation & Usage with WPA Handshakes + Hashcat

## What is hcxtools?

`hcxtools` is a collection of tools for converting Wi-Fi capture files (`.cap`, `.pcap`, `.pcapng`) into formats that tools such as **Hashcat** and **John the Ripper** can use for offline password auditing.

The most important tool is:

```bash
hcxpcapngtool
```

---

## 1. Installation — Kali / Debian / Ubuntu

### Recommended: Install with APT

```bash
sudo apt update
sudo apt install hcxtools
```

Verify the installation:

```bash
hcxpcapngtool -v
```

### Alternative: Compile from Source

Install the required dependencies:

```bash
sudo apt install git build-essential libssl-dev zlib1g-dev libcurl4-openssl-dev
```

Clone and build the repository:

```bash
git clone https://github.com/ZerBea/hcxtools.git
cd hcxtools
make
sudo make install
```

---

## 2. Basic Workflow

The general workflow is:

```text
Capture (.cap / .pcapng)
        ↓
hcxpcapngtool
        ↓
.hc22000 file
        ↓
Hashcat
```

---

## 3. Convert WPA Handshake to Hashcat Format

### Basic Conversion

```bash
hcxpcapngtool -o handshake.hc22000 handshake-01.cap
```

### Conversion with ESSID Extraction

```bash
hcxpcapngtool -o handshake.hc22000 -E wordlist.txt handshake-01.cap
```

Options:

- `-o` → specifies the output hash file (`.hc22000`)
- `-E` → creates a wordlist from ESSIDs found in the capture

### Successful Conversion

Useful output to look for:

```text
EAPOL pairs written to 22000 hash file...: 1
```

or:

```text
RSN PMKID written to 22000 hash file.....: 1
```

If one of these indicates a hash was written, the conversion was successful.

---

## 4. Crack with Hashcat

### Basic

```bash
hashcat -m 22000 handshake.hc22000 /usr/share/wordlists/rockyou.txt
```

### Recommended

```bash
hashcat -m 22000 -a 0 -O -w 3 handshake.hc22000 /usr/share/wordlists/rockyou.txt
```

Where:

- `-m 22000` → WPA-PBKDF2-PMKID/EAPOL hash mode
- `-a 0` → dictionary attack
- `-O` → enable optimized kernels
- `-w 3` → use a higher workload profile

### Show Cracked Passwords

```bash
hashcat -m 22000 handshake.hc22000 --show
```

---

## 5. Useful Extra Commands

### Convert Multiple Capture Files

```bash
hcxpcapngtool -o all.hc22000 *.cap
```

### Filter Hashes

```bash
hcxhashtool -i handshake.hc22000 -o clean.hc22000
```

### Generate Candidates from an SSID

```bash
hcxeiutool -s "YourNetworkName" -p candidates.txt
```

---

## 6. Complete Example

### 1. Convert the Capture

```bash
hcxpcapngtool -o mywifi.hc22000 -E essids.txt handshake-01.cap
```

### 2. Run Hashcat

```bash
hashcat -m 22000 -a 0 -O -w 3 mywifi.hc22000 /usr/share/wordlists/rockyou.txt
```

### 3. Check the Result

```bash
hashcat -m 22000 mywifi.hc22000 --show
```

---

## Quick Tips

- Prefer the **.hc22000** format and Hashcat mode **22000** — this is the modern format for WPA-PMKID/EAPOL hashes.
- `hcxpcapngtool` can process captures containing **4-way EAPOL handshakes** and **PMKIDs**.
- Avoid modifying or "cleaning" the original `.cap` file with unrelated tools before processing it with `hcxpcapngtool`. Wireshark/tshark can be used for inspection.
- Captures can be compressed with `gzip`; `hcxpcapngtool` can read compressed capture files.
- Only perform capture analysis and password auditing on networks you own or have explicit authorization to test.

---
