# Linux File Searching with `find`, `locate`, and `grep`

## Overview

Linux provides several powerful tools for finding files and searching inside files:

- `find` → search for files and directories by name, type, size, date, etc.
- `locate` → quickly search a database of file locations
- `grep` → search for text inside files

---

# 1. The `find` Command

## Basic Syntax

```bash
find [location] [options] [search_term]
```

Example:

```bash
find ~ -name "file.txt"
```

Searches the home directory for `file.txt`.

---

# 2. Search by File Extension

Use `*` as a wildcard.

## Find PDF files

```bash
find ~ -name "*.pdf"
```

## Find images

```bash
find ~ -name "*.jpg"
```

## Find videos

```bash
find ~ -name "*.mp4"
```

The `*` means "any characters before the extension".

---

# 3. Ignore Uppercase/Lowercase

Linux is case-sensitive.

These are different:

```
photo.jpg
Photo.JPG
PHOTO.JPG
```

Use `-iname` to ignore case:

```bash
find ~ -iname "*.jpg"
```


# Mount Android (GVFS/MTP)

1. Connect the phone via USB.
    
2. Unlock it and select **File Transfer (MTP)**.
    
3. Open the phone once in the file manager (this triggers the GVFS mount).
    
4. Access it from the terminal:
    

```bash
ls /run/user/$UID/gvfs
cd "/run/user/$UID/gvfs/mtp:host=.../Internal shared storage"
```

Use `find /run/user/$UID/gvfs -maxdepth 2` to locate the exact mount path if needed.

You can also make it even shorter if you're aiming for a quick command reference.

---

# 4. Search Only Files

Search only regular files:

```bash
find ~ -type f -name "*.pdf"
```

Search only directories:

```bash
find ~ -type d -name "Downloads"
```

---

# 5. Searching Phone Storage

After connecting a phone using USB:

1. Enable **File Transfer (MTP)** mode.
2. Check where it is mounted:

```bash
ls /media
```

or:

```bash
ls /media/$USER
```

Example search:

```bash
find /media/$USER -type f -iname "*.jpg"
```

Search PDFs:

```bash
find /media/$USER -type f -iname "*.pdf"
```

---

# 6. Search the Entire System

Search from the root directory:

```bash
sudo find / -name "*.pdf"
```

`sudo` allows searching protected directories.

---

# 7. Search by File Size

Files larger than 100 MB:

```bash
find ~ -type f -size +100M
```

Files smaller than 10 KB:

```bash
find ~ -type f -size -10k
```

---

# 8. Search by Modification Date

Files modified in the last 7 days:

```bash
find ~ -type f -mtime -7
```

Files modified more than 30 days ago:

```bash
find ~ -type f -mtime +30
```

---

# 9. The `locate` Command

`locate` is faster than `find` because it uses a database.

Install:

```bash
sudo apt update
sudo apt install plocate
```

Update database:

```bash
sudo updatedb
```

Search:

```bash
locate filename.pdf
```

Example:

```bash
locate "*.jpg"
```

Note:

- Faster than `find`
- May not find recently created files until `updatedb` is run

---

# 10. Search Inside Files with `grep`

`find` searches filenames.  
`grep` searches file contents.

Example:

```bash
grep -R "password" ~
```

Useful options:

```bash
grep -Ri "hello" .
```

Options:

|Option|Meaning|
|---|---|
|`-R`|Search recursively through folders|
|`-i`|Ignore uppercase/lowercase|

---

# Useful Commands Cheat Sheet

|Task|Command|
|---|---|
|Find a file by name|`find ~ -name "file.txt"`|
|Find an extension|`find ~ -name "*.pdf"`|
|Ignore case|`find ~ -iname "*.jpg"`|
|Find only files|`find ~ -type f`|
|Find only folders|`find ~ -type d`|
|Search entire system|`sudo find /`|
|Fast filename search|`locate filename`|
|Search text inside files|`grep -R "text" folder`|

---

# Most Useful Pattern to Remember

```bash
find /path/to/search -type f -iname "*.extension"
```

Examples:

```bash
find /home -type f -iname "*.txt"
```

```bash
find /media/$USER -type f -iname "*.mp3"
```

```bash
find / -type f -iname "*.jpg"
```

---

# Quick Tip

When you do not know where a file is:

1. Start with your home directory:

```bash
find ~ -iname "*filename*"
```

2. If nothing appears, search mounted storage:

```bash
find /media -iname "*filename*"
```

3. For the whole machine:

```bash
sudo find / -iname "*filename*"
```

---

## `find` filename patterns — quick notes

The basic syntax is:

```bash
find <where> -type f -iname "<pattern>"
```

For example:

```bash
find ~ -type f -iname "*.png"
```

This searches your home directory (`~`) for files ending in `.png`, ignoring capitalization.

### Wildcards

- `*` → any number of characters
- `?` → exactly one character
- `[abc]` → one character that is `a`, `b`, or `c`

### Examples

**Find all PNG files:**

```bash
find ~ -type f -iname "*.png"
```

**Find filenames containing `report`:**

```bash
find ~ -type f -iname "*report*.pdf"
```

Matches things like:

```text
report.pdf
my-report.pdf
annual_report_2026.pdf
```

**Find files starting with photo:**

```bash
find ~ -type f -iname "photo*"
```

**Find files ending with .jpg or .jpeg:**

```bash
find ~ -type f \( -iname "*.jpg" -o -iname "*.jpeg" \)
```

**Find an exact filename:**

```bash
find ~ -type f -iname "myfile.png"
```

**Find files with one unknown character:**

```bash
find ~ -type f -iname "photo?.png"
```

This could match:

```text
photo1.png
photo2.png
photoA.png
```

but not:

```text
photo12.png
```

### `-name` vs `-iname`

`-name` is **case-sensitive**:

```bash
find ~ -type f -name "*.PNG"
```

`-iname` is **case-insensitive**:

```bash
find ~ -type f -iname "*.png"
```

So `-iname` is often more convenient when you don't care about capitalization.

### ⭐ Most useful pattern to remember

If you want to search for a word anywhere in a filename:

```bash
find ~ -type f -iname "*word*"
```

For example:

```bash
find ~ -type f -iname "*invoice*"
```

And remember to **quote the pattern** (`"*invoice*"`), so your shell doesn't expand the `*` before `find` sees it.

---
