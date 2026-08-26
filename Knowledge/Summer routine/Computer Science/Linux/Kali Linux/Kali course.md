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

==========================

Lesson 10

==========================

===========================
