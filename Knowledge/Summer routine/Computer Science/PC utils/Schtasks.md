## 🗂️ schtasks (Windows Task Scheduler via CMD)

## 📌 What it is

`schtasks` lets you **create, manage, and automate scheduled tasks** from the command line or batch scripts.

---

## ⚙️ Basic Syntax

```Bash
schtasks /<command> [options]
```

---

## 🧱 Core Commands

## ➕ Create a Task

```Bash
schtasks /create /tn "TaskName" /tr "C:\path\script.bat" /sc daily /st 10:00
```

### Common options:

- `/tn` → Task name
- `/tr` → Task to run (script/program)
- `/sc` → Schedule type:
    - `minute`, `hourly`, `daily`, `weekly`, `monthly`, `once`, `onlogon`, `onstart`
- `/st` → Start time (HH:MM, 24h)
- `/sd` → Start date (MM/DD/YYYY)
- `/ru` → Run as user (`SYSTEM` for highest privileges)
- `/rl` → Run level:
    - `LIMITED`
    - `HIGHEST`

---

## ❌ Delete a Task

```Bash
schtasks /delete /tn "TaskName" /f
```

- `/f` → Force (no confirmation)

---

## ▶️ Run a Task Manually

```Bash
schtasks /run /tn "TaskName"
```

---

## ⏹️ End a Running Task

```Bash
schtasks /end /tn "TaskName"
```

---

## 📋 Query Tasks

```Bash
schtasks /query
```

### Useful variants:

```Bash
schtasks /query /tn "TaskName"  
schtasks /query /fo LIST  
schtasks /query /fo TABLE  
schtasks /query /v
```

---

## ✏️ Modify a Task

```Bash
schtasks /change /tn "TaskName" /st 14:00
```

---

## 🔁 Scheduling Examples

## Daily at 9:00

```Bash
schtasks /create /tn "DailyBackup" /tr "backup.bat" /sc daily /st 09:00
```

## Every 5 minutes

```Bash
schtasks /create /tn "Monitor" /tr "monitor.bat" /sc minute /mo 5
```

## At system startup

```Bash
schtasks /create /tn "StartupTask" /tr "script.bat" /sc onstart /ru SYSTEM
```

## At user logon

```Bash
schtasks /create /tn "LoginTask" /tr "script.bat" /sc onlogon
```

---

## 🔐 Run with Highest Privileges

```Bash
schtasks /create /tn "AdminTask" /tr "script.bat" /sc daily /st 12:00 /rl HIGHEST
```

---

## 📤 Output Formats

- `/fo TABLE` → Default table
- `/fo LIST` → Detailed list
- `/fo CSV` → Exportable

---

## ⚠️ Tips

- Use full paths in `/tr`
- Quote paths with spaces
- Combine with `.bat` scripts for automation
- Use `/ru SYSTEM` for background/system tasks
- Check Task Scheduler GUI (`taskschd.msc`) for debugging

---

## 🧠 Quick Cheat Sheet

```Bash
:: Create  
schtasks /create /tn "Name" /tr "script.bat" /sc daily /st 10:00  
  
:: Run  
schtasks /run /tn "Name"  
  
:: Delete  
schtasks /delete /tn "Name" /f  
  
:: List  
schtasks /query /fo TABLE  
  
:: Modify  
schtasks /change /tn "Name" /st 12:00
```