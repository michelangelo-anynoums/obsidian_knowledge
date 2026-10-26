**PowerShell** is a task automation tool and scripting language built for Windows (and now cross-platform). This very easy introduction will cover what it is, how to run it, and a few simple commands to get you started.

## **What PowerShell is (in short)**

- A command-line shell: you type commands to control your computer.
    
- A scripting language: you can write scripts to automate multi-step tasks.
    
- Works with objects: commands produce and pass objects, not just text, which makes automation powerful.
    

## **Getting started basics**

- Open PowerShell: look for “Windows PowerShell” or “PowerShell” in your start menu and run as Administrator if you plan to change system settings.
    
- Check your version: type Get-Host or $PSVersionTable.PSVersion. This helps you know which features are available.
    
- Run a simple command: type Get-Process to list running processes. It returns objects you can pipe to other commands.
    

## **Common concepts you’ll use**

- Cmdlets: small built-in commands like Get-Process, Get-Service, Set-Location. Think of them as verbs.
    
- Pipelining: use the | character to pass output from one cmdlet to another, e.g., Get-Process | Sort-Object CPU -Descending.
    
- Variables: assign values with $name = "value" and use them later, e.g., $path = "C:\Logs"; Get-ChildItem $path.
    
- Help and learning: use Get-Help Get-Process to get details about a cmdlet, its syntax, and examples. You can also use Get-Help -Online for web-based documentation.
    

## **Your first easy script**

- Create a script file: Open a text editor and save as Hello.ps1.
    
- Write a tiny script:
    
    - Write-Output "Hello, PowerShell!"
        
    - $name = Read-Host "What is your name?"
        
    - Write-Output "Nice to meet you, $name!"
        
- Run it: In PowerShell, navigate to the folder and type .\Hello.ps1. You may need to adjust the Execution Policy once to allow running scripts.
    

## **Important notes for beginners**

- Execution policy: PowerShell can be strict about running scripts. If you see a message about scripts being disabled, you’ll typically run Set-ExecutionPolicy RemoteSigned in an elevated session, then confirm.
    
- Path and permissions: When you work with files or folders, ensure you have the correct permissions and use absolute paths if necessary.
    
- Practice minimal steps: Start with simple commands (listing files, checking services) before building longer scripts.
![[powershell_icon.webp]]
## What You Will Learn: Functions in PowerShell

- How to define a simple **function** with a name and a body of commands.
    
- How to call your function like a normal PowerShell command.
    
- How to use **parameters** so your function can accept input (like a file path or a name).
    
- How to return values from a function and capture them in variables.
    
- How functions help you avoid repeating code and keep scripts organized and readable.

[[powershell functions]]


---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
