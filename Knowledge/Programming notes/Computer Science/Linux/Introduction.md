# 🐧 GNU/Linux

> [!abstract] Overview **GNU/Linux** is a family of free, open-source, Unix-like operating systems built around the **Linux kernel**. It combines the GNU ecosystem, the Linux kernel, and other software to provide a complete operating system.

![[Linux_picture.webp|463]]

## 01 · History & Origins

|Year|Milestone|
|---|---|
|1983|**Richard Stallman** launches the GNU Project.|
|1985|The Free Software Foundation (FSF) is founded.|
|1991|**Linus Torvalds** announces the Linux kernel.|
|1992|Linux adopts the GNU GPL license.|
|1993|Debian and Slackware are established.|
|2004|Ubuntu is first released.|

### Key People & Organizations

- **Richard Stallman** — Founded the GNU Project and pioneered the free software movement.
- **Linus Torvalds** — Created the Linux kernel and continues to oversee its development.
- **Alan Cox** — One of the early major Linux kernel developers.
- **Ian Murdock** — Founded the Debian project.
- **Patrick Volkerding** — Created Slackware Linux.
- **Mark Shuttleworth** — Founded Canonical and launched Ubuntu.
- **The Free Software Foundation (FSF)** — Promotes software freedom and maintains GNU-related projects.
- **The Linux Foundation** — Supports the Linux ecosystem and collaborative open-source development.

## 02 · GNU/Linux vs. Linux

> [!important] Important distinction **Linux is the kernel, not the entire operating system.**

|Component|Purpose|
|---|---|
|GNU|Provides essential system utilities, tools and libraries.|
|Linux|Kernel responsible for hardware and system resources.|
|Shell|Interprets commands and provides a command-line interface.|
|Core utilities|Essential commands such as `ls`, `cp`, `mv` and `cat`.|
|Applications|Browsers, editors, development tools and more.|
|Desktop environment|Graphical interface, such as GNOME or KDE Plasma.|

**GNU/Linux = Linux kernel + GNU software + other system components.**

Not every Linux-based operating system uses GNU components. Android, for example, uses the Linux kernel but has a different user-space ecosystem.

## 03 · Core Concepts

|Concept|Description|
|---|---|
|**Kernel**|Manages hardware, memory, processes and devices.|
|**Shell**|Command interpreter (Bash, Zsh, Fish).|
|**Terminal**|Interface used to interact with a shell.|
|**Filesystem**|Organizes files and directories in a hierarchy.|
|**Root (****`/`****)**|The top-level directory of the filesystem.|
|**Root user**|Administrator account with unrestricted privileges.|
|**Package manager**|Installs, updates and removes software.|
|**Repository**|Collection of software packages.|
|**Daemon**|Background service running on the system.|
|**Process**|An instance of a running program.|
|**Distro**|Complete operating system assembled around a kernel and software ecosystem.|

### Important Directories

|Directory|Purpose|
|---|---|
|`/`|Filesystem root|
|`/home`|Personal user directories|
|`/root`|Root user's home directory|
|`/etc`|System configuration|
|`/bin`|Essential user commands|
|`/usr`|Applications, libraries and shared resources|
|`/var`|Logs and variable data|
|`/tmp`|Temporary files|
|`/dev`|Device files|
|`/proc`|Virtual process and kernel information|
|`/boot`|Bootloader and kernel files|

## 04 · Major GNU/Linux Distributions

A **distribution (distro)** packages the Linux kernel, system utilities, software, package management and configuration into a usable operating system.

|Distribution|First release|Main characteristics|
|---|---|---|
|**Debian**|1993|Stability, community-driven and extensive repositories.|
|**Slackware**|1993|Traditional Unix philosophy and simplicity.|
|**Red Hat Enterprise Linux**|2002|Enterprise support and long-term stability.|
|**Gentoo**|2002|Source-based packages and extensive customization.|
|**Arch Linux**|2002|Minimalism, rolling releases and user control.|
|**Ubuntu**|2004|Accessibility, desktop and server environments.|
|**Fedora**|2003|Modern technologies and upstream innovation.|
|**Linux Mint**|2006|Beginner-friendly desktop experience.|
|**openSUSE**|2005|Administration tools and enterprise-oriented technologies.|

### Distribution Families

- **Debian-based:** Debian, Ubuntu, Linux Mint, Pop!_OS.
- **Red Hat-based:** Fedora, RHEL, Rocky Linux, AlmaLinux.
- **Arch-based:** Arch Linux, EndeavourOS, Manjaro.
- **Independent:** Gentoo, Slackware, NixOS, Void Linux.

## 05 · Package Managers

Package managers automate software installation, updates and removal.

|Ecosystem|Package manager|Format|
|---|---|---|
|Debian / Ubuntu|`APT`|`.deb`|
|Fedora / RHEL|`DNF`|`.rpm`|
|Arch Linux|`Pacman`|`.pkg.tar.zst`|
|openSUSE|`Zypper`|`.rpm`|
|Gentoo|`Portage`|Source packages|

Other universal packaging systems:

- **Flatpak** — Sandboxed desktop applications.
- **Snap** — Universal application packaging.
- **AppImage** — Portable application bundles.

## 06 · Desktop Environments

The desktop environment provides the graphical user interface (GUI).

- **GNOME** — Modern, streamlined and productivity-focused.
- **KDE Plasma** — Highly customizable and feature-rich.
- **XFCE** — Lightweight and resource-efficient.
- **LXQt** — Minimal and lightweight.
- **Cinnamon** — Traditional desktop layout.
- **MATE** — Continuation of the classic GNOME 2 experience.

> [!tip] Desktop environment ≠ Window manager A desktop environment provides a complete graphical experience. A window manager primarily controls application windows.

## 07 · Essential Technologies

|Technology|Purpose|
|---|---|
|**GRUB**|Common bootloader for GNU/Linux systems.|
|**systemd**|System initialization and service management.|
|**Wayland**|Modern display-server protocol.|
|**X11 / Xorg**|Traditional graphical display system.|
|**Bash**|Widely used command-line shell.|
|**OpenSSH**|Secure remote access and administration.|
|**Git**|Distributed version control.|
|**GCC**|GNU Compiler Collection.|
|**glibc**|GNU C Library, used by many Linux distributions.|
|**udev**|Manages device events and device nodes.|

## 08 · Essential Commands

|Command|Function|
|---|---|
|`pwd`|Show current directory.|
|`ls`|List files and directories.|
|`cd`|Change directory.|
|`mkdir`|Create directories.|
|`touch`|Create empty files or update timestamps.|
|`cp`|Copy files.|
|`mv`|Move or rename files.|
|`rm`|Remove files.|
|`cat`|Display file contents.|
|`grep`|Search text patterns.|
|`find`|Search for files and directories.|
|`chmod`|Change permissions.|
|`chown`|Change ownership.|
|`sudo`|Execute commands with elevated privileges.|
|`man`|Read command documentation.|
|`ps`|Display running processes.|
|`systemctl`|Manage systemd services.|

## 09 · Software Freedom & Licensing

GNU/Linux is strongly associated with the Free Software and Open Source movements.

**Four essential software freedoms (GNU):**

1. Run the program for any purpose.
2. Study how it works and modify it.
3. Redistribute copies.
4. Distribute modified versions.

### Important Licenses

- **GNU GPL** — Copyleft license that preserves software freedoms.
- **MIT License** — Permissive and simple.
- **Apache 2.0** — Permissive license with explicit patent provisions.
- **BSD Licenses** — Permissive open-source licenses.

> [!info] Free software ≠ necessarily free of charge The word _free_ refers primarily to freedom, not price.

## 10 · Why GNU/Linux?

- **Open source:** Inspect, modify and distribute source code.
- **Security:** Strong permission model and extensive security tooling.
- **Stability:** Widely used in servers and critical infrastructure.
- **Customization:** Control over almost every system component.
- **Performance:** Works across everything from embedded devices to supercomputers.
- **Development:** Excellent ecosystem for programming, automation and DevOps.
- **Community:** Global collaboration and knowledge sharing.

## 11 · Where Is GNU/Linux Used?

- **Servers & Cloud:** Web hosting, databases and cloud infrastructure.
- **Supercomputers:** Dominates the TOP500 supercomputer ecosystem.
- **Embedded Systems:** Routers, IoT devices and industrial equipment.
- **Cybersecurity:** Penetration-testing and digital-forensics distributions.
- **Development:** Programming, containers and CI/CD.
- **Desktop Computing:** Personal computers and workstations.
- **Mobile:** Android uses the Linux kernel.

---

> [!quote] Philosophy "Free software is a matter of liberty, not price." — Richard Stallman

