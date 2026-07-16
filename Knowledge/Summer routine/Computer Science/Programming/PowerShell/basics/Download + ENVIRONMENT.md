## 🧾 PowerShell Download & Execution – Quick Notes

### ⚡ PowerShell – Common Download Methods

---

### 1. `Invoke-WebRequest`

```powershell
Invoke-WebRequest -Uri "https://example.com/file.exe" -OutFile "file.exe"
```

**Notes:**

- Built-in and easy to use
    
- Supports headers, authentication, etc.
    
- Slower for large files
    
- Alias: `iwr`
    

---

### 2. `New-Object` (WebClient)

```powershell
$client = New-Object System.Net.WebClient
$client.DownloadFile("https://example.com/file.exe", "file.exe")
```

**Notes:**

- Faster than `Invoke-WebRequest`
    
- Lightweight and simple
    
- Deprecated in newer .NET versions, but still widely used
    

---

### 3. BITS Transfer (`Start-BitsTransfer`)

```powershell
Start-BitsTransfer -Source "https://example.com/file.exe" -Destination "file.exe"
```

**Notes:**

- Uses Background Intelligent Transfer Service (BITS)
    
- Resumable and reliable for large files
    
- Works in background
    
- Slower startup but efficient for unstable networks
    

---

## 🏆 Which Method Is Better?

|Method|Best Use Case|
|---|---|
|`Invoke-WebRequest`|Simple scripts, quick downloads|
|`WebClient`|Speed and simplicity|
|`Start-BitsTransfer`|Large files, unstable connections|

👉 **Recommendation:**

- Use **WebClient** for speed
    
- Use **BITS** for reliability
    
- Avoid `Invoke-WebRequest` for heavy downloads
    

---

## 🖥️ Running PowerShell from Batch (`.bat`)

### Basic Execution

```bat
powershell -Command "Get-Process"
```

---

### Run Script File

```bat
powershell -ExecutionPolicy Bypass -File script.ps1
```

---

### Silent / Hidden Execution

#### Hidden Window

```bat
powershell -WindowStyle Hidden -Command "Get-Process"
```

#### Fully Silent (No Output)

```bat
powershell -WindowStyle Hidden -ExecutionPolicy Bypass -File script.ps1 >nul 2>&1
```

---

## 🌍 Environment Variables (PowerShell & Batch)

### PowerShell Variables

```powershell
$env:COMPUTERNAME   # Hostname
$env:USERNAME       # Current user
$env:USERPROFILE    # User home directory
$env:TEMP           # Temp folder
$env:PATH           # System path
```

---

### Batch (CMD) Variables

```bat
%COMPUTERNAME%   REM Hostname
%USERNAME%       REM Current user
%USERPROFILE%    REM User home directory
%TEMP%           REM Temp folder
%PATH%           REM System path
```

---

### 🧠 Notes

- PowerShell uses `$env:VAR` syntax
    
- Batch uses `%VAR%` syntax
    
- Same underlying environment variables, different access methods
    

---

## ✅ Quick Summary

- **Fast download:** `WebClient`
    
- **Reliable download:** `Start-BitsTransfer`
    
- **Simple download:** `Invoke-WebRequest`
    
- **Batch execution:** `powershell` with flags
    
- **Env vars:** `$env:VAR` (PowerShell) vs `%VAR%` (Batch)
    

---

## ➕ Additional Notes – Multi-line Execution & Navigation

---

## 🧩 1. Running Multiple PowerShell Commands from Batch

### Option 1: Inline (semicolon-separated)

```bat
powershell -Command "Get-Date; Get-Process; Write-Output 'Done'"
```

---

### Option 2: Use a Script File (Recommended)

```bat
powershell -ExecutionPolicy Bypass -File script.ps1
```

**Example `script.ps1`:**

```powershell
Get-Date
Get-Process
Write-Output "Done"
```

---

### Option 3: Multi-line via `^` (line continuation in batch)

```bat
powershell -Command ^
"Get-Date; ^
Get-Process; ^
Write-Output 'Done'"
```

---

### 🧠 Notes

- `;` separates commands in PowerShell
    
- `^` allows multi-line formatting in `.bat`
    
- Script files are cleaner and easier to maintain
    

---

## 📁 2. Navigating to Downloads & Desktop

### PowerShell

#### Using Environment Variables

```powershell
cd $env:USERPROFILE\Downloads
cd $env:USERPROFILE\Desktop
```

#### Using .NET (more robust)

```powershell
cd ([Environment]::GetFolderPath("Downloads"))
cd ([Environment]::GetFolderPath("Desktop"))
```

---

### Batch (CMD)

```bat
cd %USERPROFILE%\Downloads
cd %USERPROFILE%\Desktop
```

---

### 🧠 Notes

- `$env:USERPROFILE` / `%USERPROFILE%` points to user home
    
- Works across most Windows setups
    
- The `.NET` method is safer if folder names differ (localization, etc.)
    

---

## ✅ Quick Summary

- **Multiple commands:** use `;`, `^`, or `.ps1` script
    
- **Best practice:** use script files for anything non-trivial
    
- **Navigation:**
    
    - PowerShell → `$env:USERPROFILE\Downloads`
        
    - Batch → `%USERPROFILE%\Downloads`
        

---
