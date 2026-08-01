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

Everything in Linux is a file. Every commands are file.

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

==========================

Lesson 8

=========================


==========================

Lesson 9

==========================

==========================

Lesson 10

==========================

===========================