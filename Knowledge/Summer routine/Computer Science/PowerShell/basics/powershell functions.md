
## **PowerShell Functions — A Beginner Introduction**

## What is a function?

A **function** is a named block of code that performs a task and can be reused.

Instead of repeating the same commands:

- You write them once
    
- Give them a name
    
- Call them whenever you need
    

Think of a function like a **button** 🔘  
Press the button → PowerShell runs the code inside.

---

## Run **PowerShell** script in the **TERMINAL:**

```Powershell
powershell.exe -ExecutionPolicy Bypass -File "C:\Path\To\YourScript.ps1"
```


---


## Basic function structure

```Powershell
function Function-Name { 
	# code goes here 
}
```

Example:

```Powershell
function Say-Hello { Write-Host "Hello, PowerShell!" }
```

Call it:

`Say-Hello`

Output:

`Hello, PowerShell!`

---

## Adding parameters (input)

Parameters let your function **accept values** from the user.

```Powershell
function Say-Hello {     
	param ($Name)      
	Write-Host "Hello, $Name!" 
}
```

Call it:

`Say-Hello -Name "Alex"`

Output:

`Hello, Alex!`

---

## What is `param`?

The `param` block:

- Defines what inputs the function accepts
    
- Always goes at the **top** of the function
    

`param (     $Variable1,     $Variable2 )`

---

## Typed parameters (`[string]`, `[int]`, etc.)

You can **tell PowerShell what kind of data** a parameter should be.

```Powershell
param ( [string]$Name )
```

This means:

> “`$Name` should be text.”

### Common types

|Type|Meaning|Example|
|---|---|---|
|`[string]`|Text|`"Hello"`|
|`[int]`|Whole numbers|`42`|
|`[bool]`|True / False|`$true`|
|`[string[]]`|Multiple strings|`"PC1","PC2"`|

---

## Example with typed parameters

```Powershell
function Show-User {     
	param (         
		[string]$Username,         
		[int]$Age     
	)      
	Write-Host "User: $Username"     
	Write-Host "Age: $Age" 
}
```

Call it:

`Show-User -Username "Sam" -Age 30`

---

## Why parameter types matter

Using types helps PowerShell:

- Catch errors early
    
- Auto-convert values safely
    
- Make your function easier to understand
    

Example:

`[int]$Age`

Passing `"abc"` will fail, but `25` will work.

---

## Mandatory parameters

You can force the user to supply a value:

```Powershell
function Say-Hello {     
	param (
		[Parameter(Mandatory)]         
		[string]$Name     
	)      
	Write-Host "Hello, $Name!" 
}
```

If you forget `-Name`, PowerShell will prompt you for it.

---

## Returning values from a function

Functions can **return data**, not just print text.

```Powershell
function Add-Numbers {
	param (      
		[int]$A,         
		[int]$B     
	)      
	$A + $B 
}
```

Use it:

`$result = Add-Numbers -A 5 -B 7 $result`

Output:

`12`

PowerShell returns the **last expression automatically**.

---

## Real-world example: check service status

```Powershell
function Get-ServiceStatus {     
	param (         
		[string]$ServiceName     
	)      
	Get-Service -Name $ServiceName 
}
```

Call it:

`Get-ServiceStatus -ServiceName "wuauserv"`

---

## Naming conventions (important!)

PowerShell uses **Verb-Noun** naming:

✅ Good:

- `Get-Time`
    
- `Set-Config`
    
- `Test-Connection`
    

❌ Avoid:

- `myFunc`
    
- `doStuff`
    
- `hello123`
    

You can see approved verbs with:

`Get-Verb`

---

## Where functions live

Functions exist:

- In the current PowerShell session
    
- In a `.ps1` script
    
- In your PowerShell profile
    
- Inside modules (later topic)
    

If you close PowerShell, session-only functions disappear.

---

## Full simple example

```Powershell
function Get-Greeting {
     param (
	     [string]$Name,         
	     [bool]$Formal     
     )      
     if ($Formal) {
	     "Good day, $Name."     
     } else { 
	     "Hi $Name!"     
	     } 
}
```

Call it:

```Powershell
Get-Greeting -Name "Alex" -Formal $true
```

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Summer routine/Computer Science/PowerShell/Introduction|Introduction]]
