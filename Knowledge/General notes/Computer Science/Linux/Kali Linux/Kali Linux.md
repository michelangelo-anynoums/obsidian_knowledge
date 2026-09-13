# 🐧 Linux (Kali) — Course Notes

> [!INFO]  
> **Course:** Linux (Kali)  
> **Lessons:** 1–10  
> **Source:** YouTube course  
> **Reference:** https://youtu.be/VbEx7BPTOE

![[Pasted image 20260913070829.png|564]]

---

# 1. 📁 Navigation & Basic File System

## `pwd`

Prints the **current working directory**.

```bash
pwd
```

> [!TIP]  
> Think of `pwd` as **"Where am I?"**

---

## `ls`

Lists files and directories.

```bash
ls
ls -l       # Long/detailed listing
ls -a       # Show hidden files
```

Common aliases:

```bash
ll          # Usually an alias for ls -l
la          # Usually an alias for ls -a
```

> [!NOTE]  
> `ll` and `la` are commonly configured as aliases, but they are **not universal Linux commands**.

---

## `cd`

Changes the current directory.

```bash
cd [directory]
cd ..       # Move up one directory
cd ../..    # Move up two directories
cd ../../.. # Move up three directories
cd -        # Return to the previous directory
cd          # Go to the user's home directory
```

Useful variables:

```bash
$PWD        # Current working directory
$OLDPWD     # Previous working directory
```

---

## `tree`

Displays directories and files in a tree structure.

```bash
tree
```

---

# 2. 👤 Users, Groups & Permissions

## `whoami`

Displays the current username.

```bash
whoami
```

---

## `id`

Displays user and group information.

```bash
id
```

---

## Creating Users

### `adduser`

Creates a new user interactively.

```bash
sudo adduser [username]
```

### `useradd`

Creates a user.

```bash
sudo useradd [username]
sudo useradd -m [username]
```

> [!NOTE]  
> `-m` creates the user's home directory.

---

## Changing a Password

```bash
sudo passwd [username]
```

---

## Changing User Properties

### Change the user's shell

```bash
sudo usermod [username] --shell /bin/bash
```

### Rename a user

```bash
sudo usermod -l [new_name] [old_name]
```

### Display help

```bash
usermod --help
```

---

## Switching Users

```bash
su - [username]
```

Switch to another user with their login environment.

```bash
sudo su -
```

Switch to a root login shell.

```bash
exit
logout
```

> [!WARNING]  
> Be careful when working as `root`. Commands executed as root can modify or delete critical system files.

---

## Deleting Users

```bash
sudo userdel [username]
```

---

# 3. 👥 Groups

## Create a Group

```bash
sudo groupadd [group_name]
```

---

## View Groups

```bash
cat /etc/group
```

---

## Add a User to a Group

```bash
sudo usermod -aG [group_name] [username]
```

> [!IMPORTANT]  
> `-aG` means **append** the user to the supplementary group.  
> The `-a` is important because omitting it can replace the user's existing supplementary groups.

---

## Delete a Group

```bash
sudo groupdel [group_name]
```

---

# 4. 🔐 Important User Files

## `/etc/passwd`

Contains information about local user accounts.

```bash
cat /etc/passwd
```

---

## `/etc/shadow`

Contains password-related authentication information.

```bash
sudo cat /etc/shadow
```

> [!WARNING]  
> `/etc/shadow` is sensitive and normally readable only by root or privileged processes.

---

## User Home Directory

Normally located at:

```text
/home/[username]
```

---

# 5. 🔑 Sudo Configuration

## `visudo`

Safely edits the sudo configuration.

```bash
sudo visudo
```

> [!IMPORTANT]  
> Prefer `visudo` instead of directly editing `/etc/sudoers`, because it checks the configuration for syntax errors.

---

# 6. 📄 Files & Directories

## Creating Files

### `touch`

Creates an empty file or updates its timestamp.

```bash
touch file
```

---

## Reading Files

### `cat`

Displays the contents of a file.

```bash
cat file
```

---

## Writing to Files

### `cat >`

Writes input to a file, **overwriting** the existing contents.

```bash
cat > file
```

Press `CTRL + D` when finished.

---

### `cat << EOF`

Creates a file using a here-document.

```bash
cat << EOF > file
text
another line
EOF
```

---

### `echo`

Writes text to a file.

```bash
echo "text" > file
```

Use `>>` to append instead of overwrite:

```bash
echo "text" >> file
```

> [!WARNING]  
> `>` overwrites the file.  
> `>>` appends to the file.

---

## Creating Directories

```bash
mkdir directory
```

Create nested directories:

```bash
mkdir -p directory/subdirectory/another
```

---

## Moving Files

```bash
mv file directory
```

`mv` can also be used to rename files:

```bash
mv old_name new_name
```

---

## Copying Files

```bash
cp file directory
```

Copy directories recursively:

```bash
cp -r directory destination
```

---

## Removing Files

```bash
rm file
```

Remove directories and their contents recursively:

```bash
rm -rf directory
```

> [!DANGER]  
> `rm -rf` is powerful and potentially destructive. Double-check the path before pressing Enter.

---

## Removing Empty Directories

```bash
rmdir directory
```

---

# 7. 🔎 Finding Commands & Getting Help

## `which`

Shows the location of a command executable.

```bash
which [command]
```

Example:

```bash
which python
```

---

## `man`

Displays the manual page for a command.

```bash
man [command]
```

Example:

```bash
man ls
```

---

## Command Help

Many commands support:

```bash
[command] -h
[command] --help
```

> [!NOTE]  
> `--help` is generally more consistent than `-help`, but supported options depend on the command.

---

## `apropos`

Searches manual-page descriptions for a keyword.

```bash
apropos [description]
```

Example:

```bash
apropos network
```

> [!TIP]  
> Use `apropos` when you know **what you want to do** but don't know the command name.

---

# 8. 🖥️ System Information

## `hostname`

Displays or works with the system's hostname.

```bash
hostname
```

---

## `uname`

Displays system information.

```bash
uname
uname -r    # Kernel release
uname -a    # All available information
```

---

## `who`

Shows users currently logged into the system.

```bash
who
```

---

## `whoami`

Shows the current effective username.

```bash
whoami
```

---

# 9. ⚙️ Processes

## `ps`

Displays running processes.

```bash
ps
```

More detailed process information:

```bash
ps aux
```

Processes belonging to a specific user:

```bash
ps -u [username]
```

---

## `pstree`

Displays processes in a tree structure.

```bash
pstree
```

---

## `pgrep`

Finds processes by name or other attributes.

```bash
pgrep [process]
```

---

## `top`

Interactive display of running processes and system resource usage.

```bash
top
```

---

## `htop`

An interactive and more user-friendly process viewer.

```bash
htop
```

> [!NOTE]  
> `htop` may need to be installed separately.

---

# 10. 🛑 Managing Processes

## `kill`

Sends a signal to a process.

```bash
kill [PID]
```

Example:

```bash
kill 1234
```

---

## List Available Signals

```bash
kill -l
```

---

## Stop a Process

Signal `19` is `SIGSTOP` on Linux:

```bash
kill -19 [PID]
```

---

## Forcefully Kill a Process

```bash
kill -9 [PID]
```

> [!WARNING]  
> `SIGKILL` (`-9`) immediately terminates a process and does not allow it to clean up normally. Try a regular `kill` first when appropriate.

---

## `pkill`

Kills processes based on their name or other criteria.

```bash
pkill -9 [process]
```

---

# 11. 🔄 Jobs & Background Processes

## Run a Command in the Background

```bash
[command] &
```

Example:

```bash
sleep 60 &
```

---

## `jobs`

Shows jobs started by the current shell.

```bash
jobs
```

---

## `CTRL + Z`

Suspends the currently running foreground process/job.

---

## `bg`

Continues a suspended job in the background.

```bash
bg [job_ID]
```

---

## `fg`

Brings a background/suspended job to the foreground.

```bash
fg [job_ID]
```

> [!NOTE]  
> Job IDs shown by `jobs` normally use `%1`, `%2`, etc., while process IDs (PIDs) are different numbers.

---

# 12. 🧩 Services & `systemctl`

`systemctl` is used to manage **systemd services and units**.

## Start a Service

```bash
sudo systemctl start [service]
```

---

## Stop a Service

```bash
sudo systemctl stop [service]
```

---

## Restart a Service

```bash
sudo systemctl restart [service]
```

---

## Reload a Service

```bash
sudo systemctl reload [service]
```

Reload configuration without completely restarting the service, when supported.

---

## Reload or Restart

```bash
sudo systemctl reload-or-restart [service]
```

---

## Check Service Status

```bash
systemctl status [service]
```

---

## Check Whether a Service Is Active

```bash
systemctl is-active [service]
```

---

## Enable a Service at Boot

```bash
sudo systemctl enable [service]
```

---

## Disable a Service at Boot

```bash
sudo systemctl disable [service]
```

---

## List Units

```bash
systemctl list-units
```

List all units, including inactive ones:

```bash
systemctl list-units --all
```

---

## List Installed Unit Files

```bash
systemctl list-unit-files
```

> [!IMPORTANT]  
> `list-unit-files` is the correct command for listing installed systemd unit files.

---

# 13. 🌐 Networking

## `ifconfig`

Displays/configures network interfaces.

```bash
ifconfig
```

> [!NOTE]  
> `ifconfig` is an older tool. Modern Linux systems generally use the `ip` command instead.

---

## `ip`

Modern command for viewing and managing network configuration.

```bash
ip
```

Common examples:

```bash
ip addr
ip link
ip route
```

---

## `netstat`

Displays network connections and related information.

```bash
netstat
```

> [!NOTE]  
> `netstat` is considered legacy on many modern Linux distributions. `ss` is generally preferred.

---

## `ss`

Displays socket/network information.

```bash
ss
```

---

## `ping`

Tests network connectivity to a host.

```bash
ping [host/IP]
```

Example:

```bash
ping 8.8.8.8
```

---

# 14. 💾 Hardware & Open Files

## `lsblk`

Lists block devices such as disks and partitions.

```bash
lsblk
```

---

## `lsusb`

Lists connected USB devices.

```bash
lsusb
```

---

## `lsof`

Lists open files and can help identify which processes are using files, ports, etc.

```bash
lsof
```

---

# 15. 🌍 Localhost & Web Servers

## `127.0.0.1`

The IPv4 loopback address, commonly referred to as **localhost**.

```text
127.0.0.1 = localhost
```

---

## Python HTTP Server

Start a simple HTTP server in the current directory:

```bash
python -m http.server [port]
```

Example:

```bash
python -m http.server 8000
```

---

## PHP Development Server

```bash
php -S 127.0.0.1:[port]
```

Example:

```bash
php -S 127.0.0.1:8000
```

---

## Apache

Start the Apache web server:

```bash
sudo systemctl start apache2
```

---

# 16. 🌐 `curl`

`curl` transfers data to/from URLs and is commonly used for testing web services.

## Request a URL

```bash
curl [URL]
```

---

## Download to a File

```bash
curl -o [filename] [URL]
```

---

## Display HTTP Headers

```bash
curl -I [URL]
```

---

## Verbose Output

```bash
curl -v [URL]
```

> [!TIP]  
> `curl -v` is useful when troubleshooting HTTP connections because it displays additional connection and request information.

---

# 17. 📥 `wget`

Downloads files from URLs.

```bash
wget [URL]
```

---

# 18. 📦 Package Management — APT

APT is the package-management system commonly used on Debian-based distributions such as Kali Linux.

## Update Package Lists

```bash
sudo apt update
```

> [!NOTE]  
> `apt update` refreshes package information. It does **not** upgrade installed packages.

---

## Upgrade Installed Packages

```bash
sudo apt upgrade
```

---

## Full Upgrade

```bash
sudo apt full-upgrade
```

`full-upgrade` may install/remove packages when necessary to complete upgrades.

---

## Install a Package

```bash
sudo apt install [package]
```

---

## Fix Broken Dependencies

```bash
sudo apt --fix-broken install
```

---

## Search for a Package

```bash
apt search [package]
```

---

## Show Package Information

```bash
apt show [package]
```

---

## List Packages

```bash
apt list
```

Installed packages:

```bash
apt list --installed
```

---

## Remove a Package

```bash
sudo apt remove [package]
```

---

## Purge a Package

```bash
sudo apt purge [package]
```

> [!NOTE]  
> `remove` removes the package but may leave configuration files.  
> `purge` also removes package configuration files.

---

## Edit APT Sources

```bash
sudo apt edit-sources
```

---

## `aptitude`

An alternative package-management interface for Debian-based systems.

```bash
aptitude
```

---

# 19. 📦 `dpkg`

`dpkg` is a lower-level Debian package-management tool.

Install a local `.deb` package:

```bash
sudo dpkg -i [package.deb]
```

> [!WARNING]  
> `dpkg` does not automatically resolve all dependencies. `apt` can generally handle dependency resolution more conveniently.

---

# 20. 📦 Snap Packages

Install `snapd`:

```bash
sudo apt install snapd
```

Install an application using Snap:

```bash
sudo snap install --classic [application]
```

---

# 21. 🐍 Python Packages

Install dependencies listed in `requirements.txt`:

```bash
pip3 install -r requirements.txt
```

> [!TIP]  
> In modern Python projects, using a virtual environment is often preferable:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

# 22. 🐙 Git

## Clone a Repository

Downloads a Git repository to the local machine.

```bash
git clone [URL]
```

Example:

```bash
git clone https://github.com/user/project.git
```

---

# 23. 🖥️ Terminal & Shell

> [!IMPORTANT]  
> A **terminal emulator** is the graphical application/window that provides access to a shell.  
> A **shell** (such as Bash) interprets commands and runs programs.

Common Linux shells include:

```text
bash
zsh
sh
fish
```

---

# 24. ⌨️ Terminal Keyboard Shortcuts

## Screen / Command Line

```text
CTRL + L
```

Clear the terminal screen.

```text
CTRL + A
```

Move to the beginning of the command line.

```text
CTRL + E
```

Move to the end of the command line.

```text
CTRL + U
```

Delete from the cursor to the **beginning** of the line.

```text
CTRL + K
```

Delete from the cursor to the **end** of the line.

```text
CTRL + Y
```

Restore/yank previously killed text.

```text
ALT + BACKSPACE
```

Delete the previous word.

---

## Copy & Paste

```text
CTRL + SHIFT + C
```

Copy from the terminal.

```text
CTRL + SHIFT + V
```

Paste into the terminal.

> [!NOTE]  
> These shortcuts are common in Linux terminal emulators. Exact shortcuts can vary depending on the terminal application.

---

## Previous Command

```bash
!!
```

Expands to the previous command.

Example:

```bash
sudo !!
```

Runs the previous command with `sudo`.

---

## Command History Search

```text
CTRL + R
```

Search backward through previously executed commands.

---

## Open Current Command in an Editor

```text
CTRL + X, CTRL + E
```

Opens the current command line in the shell's configured editor.

---

# 25. 📖 Viewing Long Output

## `less`

Displays text one screen at a time.

```bash
less [file]
```

Useful for reading long files or command output.

---

## `tail`

Displays the end of a file.

```bash
tail [file]
```

---

## Follow a File in Real Time

```bash
tail -f [file]
```

> [!TIP]  
> `tail -f` is especially useful for watching log files as new entries are added.

---

# 26. 🔧 Aliases & `.bashrc`

## Create an Alias

```bash
alias variable="command"
```

Example:

```bash
alias ll="ls -la"
```

---

## Make an Alias Persistent

Edit `.bashrc`:

```bash
nano ~/.bashrc
```

Add your alias:

```bash
alias ll="ls -la"
```

Then reload the configuration:

```bash
source ~/.bashrc
```

> [!IMPORTANT]  
> An alias created directly with `alias` normally lasts only for the current shell session. Putting it in `.bashrc` makes it available in future Bash sessions.

---

# 27. 🧠 Essential Commands — Quick Reference

|Command|Purpose|
|---|---|
|`pwd`|Show current directory|
|`ls`|List files/directories|
|`cd`|Change directory|
|`cat`|Display file contents|
|`touch`|Create an empty file|
|`mkdir`|Create a directory|
|`cp`|Copy files/directories|
|`mv`|Move/rename files|
|`rm`|Remove files|
|`rmdir`|Remove empty directories|
|`tree`|Display directory tree|
|`whoami`|Show current user|
|`id`|Show user/group information|
|`ps`|Show processes|
|`top`|Monitor processes|
|`htop`|Interactive process monitor|
|`kill`|Send a signal to a process|
|`systemctl`|Manage systemd services|
|`ip`|Network configuration|
|`ss`|Network/socket information|
|`ping`|Test connectivity|
|`curl`|Transfer/request data from URLs|
|`wget`|Download files|
|`apt`|Manage packages|
|`dpkg`|Manage `.deb` packages|
|`git`|Version control|
|`man`|Read command manuals|
|`which`|Locate an executable|
|`apropos`|Search manual descriptions|
|`lsof`|Show open files/resources|
|`lsblk`|List storage devices|
|`lsusb`|List USB devices|

---

# 28. ⭐ Commands to Memorize First

If you're still getting comfortable with Linux, prioritize these:

### Navigation

```bash
pwd
ls
ls -la
cd
cd ..
cd -
```

### Files

```bash
touch
cat
cp
mv
rm
mkdir
```

### Users

```bash
whoami
id
su
sudo
passwd
usermod
```

### Processes

```bash
ps
top
htop
kill
jobs
bg
fg
```

### Services

```bash
systemctl status
systemctl start
systemctl stop
systemctl restart
```

### Networking

```bash
ip
ss
ping
curl
wget
```

### Packages

```bash
apt update
apt install
apt search
apt remove
apt upgrade
```

### Help

```bash
man
--help
apropos
which
```

> [!SUCCESS]  
> **Core Linux mindset:** learn what a command does, learn how to get help for it, and then practice combining simple commands together.



---


# Reference

https://youtu.be/VbEx7BPTOE

Lesson 1

=========================

pwd
ls
cd [directory]
cd ..


==========================

Lesson 2

=========================

whoami
clear or CTRL + L

Everything in Linux is a file. Every commands are files.

cat [file]
cp [file]  [copy file]
rm [file]
adduser [user name]
which [command]



==========================

Lesson 3

==========================

shell = terminal emulator

ps
su root
id
hostname
uname
uname -r
uname -a
ifconfig
ip
netstat
ss
who
whoami
lsblk
lsusb
lsof
man [command]

[command] -h or --h or --help or -help
apropos [description]


==========================

Lesson 4

=========================

adduser [user name]
cat /etc/passwd
cat /etc/shadow
/home/[user name]
useradd [user name]
passwd [user name] 
usermod -h
usermod [user name] --shell /bin/[binary (bash)]
usermod -l [new name]  [old name]
useradd [user name] -m
su - [user name] 
sudo su -
logout
exit
sudo visudo
userdel [user name]
groupadd [group name]
cat /etc/group
usermod -aG [group name]  [user name]
groupdel [group name]




==========================

Lesson 5

=========================

dpkg -i [package name]
apt [--fix-broken  (optional)] install [package name]
apt update
apt edit-sources
apt list
apt list --installed
apt show [package]
apt search [package]
apt remove [package name]
apt purge [package name]
apt upgrade
apt full-upgrade
aptitude

apt install snapd
snap install --classic [application name]

git clone [URL]

pip3 install -r requirements.txt


==========================

Lesson 6

==========================

ps
ps -aux
pstree
systemctl
systemctl stop [process]
systemctl status [process]
systemctl start [process]
systemctl restart [process]
systemctl reload-or-restart [process]
systemctl disable [process]
systemctl enable [process]
systemctl is-active [process]
systemctl is-enabled [process]
systemctl list-units
systemctl list-units --all
systemctl list-units-file


=========================

Lesson 7

=========================

ps
ps -u [user name]
pgrep [process]
kill [ID of the process]
ps -aux
top
htop
ping
sleep
jobs
CTRL + Z to put on background
bg [ID of the process]
fg [ID of the process]
kill -l
[command] & to put on background
kill -19 [ID of the process] 
pkill -9 [processes]


==========================

Lesson 8

=========================

python -m http.server [port]
php -S 127.0.0.1:[port]

127.0.0.1 = localhost

systemctl start apache2
curl [url]
curl -o [file to download]  [url]
curl -I [url]
curl -v [url]

wget [url]


==========================

Lesson 9

==========================

cd
cd ..
pwd
cd ../..
cd ../../..
cd -
`$OLDPWD`
`$PWD`
ll = ls -l
la = ls -a
alias variable="command"
nano .bashrc = adding alias
CTRL + SHIFT + C = copy
CTRL + SHIFT + V = paste
CTRL + A = go to the beginning
CTRL + E = go to the end

CTRL + U = erase the command (BEFORE the cursor)
CTRL + Y = restore the command
CTRL + K = erase the command (AFTER the cursor)
ALT + BACKSPACE  = delete one world

CTRL + X + E = open a command in a default editor
less
!! = previous command
tail
tail -f ...
CTRL + R




==========================

Lesson 10

==========================

touch file
cat file
cat > file
cat file
cat << EOF > file
echo text > file
mkdir directory
mv file directory
cp file directory
mkdir -p directory/directory...
tree
cp -r ...
rm file
rm -rf file
rmdir directory
rm --help




===========================

