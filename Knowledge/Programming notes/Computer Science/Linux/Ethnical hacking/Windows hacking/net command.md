# 🖥️ NET Command — Windows

> [!abstract] Overview The **net** **command** is a Windows command-line tool used to manage and inspect network resources, user accounts, services, and shared resources.
> 
> It is a collection of subcommands rather than a single operation. What it does depends on the subcommand you use.

## 🧠 How It Works

The `net` command lets you interact with different Windows networking and system-management features from CMD or PowerShell.

**Basic syntax:**

```
net <command> [options]
```

For example:

```
net view
```

Displays computers or shared resources available for network browsing.

> [!tip] Remember `net` is a family of commands. Use `net help` or `net help <command>` to discover available options.

## ⚡ Common NET Commands

### 1. Display Available Network Computers

```
net view
```

Lists computers or servers visible through Windows network browsing.

**Use it when:** You want to explore computers advertised on your local network.

> [!note] Important Network discovery, permissions, firewall settings, and SMB configuration affect what appears. An empty list does not necessarily mean no other devices exist.

### 2. Display Shared Resources on a Computer

```
net view \\COMPUTERNAME
```

Lists shared resources exposed by the specified computer.

**Example:**

```
net view \\OFFICE-PC
```

**Use it when:** You want to check which network shares a computer makes available to you.

### 3. Display Your Network Connections

```
net use
```

Displays current network connections, such as mapped drives and connections to shared folders.

**Example output:**

```
Status       Local     Remote
------------------------------------------------
OK           Z:        \\SERVER\Documents
```

**Use it when:** You need to identify mapped network drives or troubleshoot a network share connection.

### 4. Connect to a Shared Folder

```
net use Z: \\SERVER\Documents
```

Maps the shared folder to drive `Z:`.

- `Z:` — the local drive letter.
- `\\SERVER\Documents` — the remote shared folder.

**Use it when:** You want convenient access to a network share through File Explorer.

### 5. Disconnect a Network Drive

```
net use Z: /delete
```

Removes the mapped connection associated with drive `Z:`.

To disconnect all network connections managed by `net use`:

```
net use * /delete
```

> [!warning] Be careful The second command can disconnect multiple network resources. Check your active connections first.

### 6. Display Local User Accounts

```
net user
```

Lists local user accounts on the computer.

To inspect a specific account:

```
net user username
```

**Use it when:** You need to review account information or troubleshoot account-related issues.

### 7. Display Local Groups

```
net localgroup
```

Lists local groups on the computer.

To inspect a specific group:

```
net localgroup Administrators
```

Displays the members of the local Administrators group, subject to permissions.

**Use it when:** You need to check group membership or investigate local access permissions.

### 8. Display Windows Shares

```
net share
```

Lists shared folders and other share resources configured on your computer.

**Example:**

```
Share name   Resource
--------------------------------
Public       C:\Public
```

**Use it when:** You want to check which folders your computer shares with other users.

### 9. Display or Manage Windows Services

```
net start
```

Lists Windows services that are currently running.

To start a service:

```
net start "Service Name"
```

To stop a service:

```
net stop "Service Name"
```

**Use it when:** You need to troubleshoot a service that supports a network feature or other Windows functionality.

> [!warning] Administrator privileges Starting or stopping many services requires an elevated terminal. Stopping a service may affect applications or other users.

### 10. Display Help

```
net help
```

Displays general help for the `net` command.

For help with a particular subcommand:

```
net help use
net help user
net help share
```

**Use it when:** You need the supported syntax and options for a command.

## 🔍 Practical Example — Investigating a Network Share

Suppose you want to connect to a shared folder on an office computer.

**Step 1 — Check available computers**

```
net view
```

**Step 2 — Inspect the target computer's shares**

```
net view \\OFFICE-PC
```

**Step 3 — Map the desired share**

```
net use Z: \\OFFICE-PC\Documents
```

**Step 4 — Verify the connection**

```
net use
```

**Step 5 — Disconnect when finished**

```
net use Z: /delete
```

This workflow helps you discover, connect to, verify, and disconnect from a Windows network share.

## 🧰 Quick Reference

| Command                   | Purpose                                       |
| ------------------------- | --------------------------------------------- |
| `net view`                | Browse visible network computers or resources |
| `net view \\HOST`         | List shares on a remote computer              |
| `net use`                 | Display network connections                   |
| `net use Z: \\HOST\SHARE` | Map a network share                           |
| `net use Z: /delete`      | Disconnect a mapped drive                     |
| `net user`                | List local user accounts                      |
| `net localgroup`          | List local groups                             |
| `net share`               | List local shared resources                   |
| `net start`               | List running services                         |
| `net help`                | Display command help                          |

## 🔐 Important Notes

- Some subcommands require **administrator privileges**.
- Access to remote resources depends on permissions, credentials, firewall rules, and network configuration.
- `net view` relies on Windows network browsing mechanisms and may not discover every computer.
- Avoid putting passwords directly in commands because they may be exposed through command history or other system records.
- Commands that modify accounts, shares, connections, or services should be used carefully.

## 🔗 Related Commands

- `ipconfig` — View network configuration.
- `ping` — Test IP connectivity.
- `arp -a` — Inspect IPv4-to-MAC address mappings.
- `netstat -ano` — Inspect network connections and listening ports.
- `nslookup` — Query DNS records.
- `whoami` — Display the current user identity.
- `Get-SmbMapping` — Inspect SMB drive mappings in PowerShell.
- `Get-Service` — Inspect Windows services in PowerShell.

---
