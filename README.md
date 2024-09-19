# 🚀 Linux System Admin / Bash Notes 🚀

# Intro
Linux systems are everywhere these days. Although there are Linux distros that have beautiful user-friendly user interfaces, many times you only have access to a terminal window.

During these notes, we'll start with the basics and build knowledge / skills needed to manage or admin a Linux system.

> [!NOTE]
> **Still Need Convincing?**
> If you are at all interested in websites, simple HTML pages, WordPress, SPA, or full-blown web-based applications they are mostly hosted on Linux machines.

# Getting Started
These notes are based on the Ubuntu 24.04 LTS distro. Other distros may vary, but for the most part this should work or at least point in you the right direction.
 

# 👉 Basics

## Help

- <a href="basics/01_help.md">Help System</a>

## 
Typically, there is a built-in manual or help system that you can use to learn more about command options.


	- help

02: file system - navigation
	- pwd
	- ls, ls -la, ll
	- cd
	- mkdir
	- rm, rm -rf

03: file system - files
	- cp, cp -a
	- mv
	- touch
	- cat
	- tail, head
	- cat > file.txt
	- nano

04: searching / finding
	- grep
	- find
	- 

05: miscellaneous
	- uptime
	- uname
	- lsb_release -a
	- hostname
	- top, htop
	- ssh
	- df, df -h
	- du
	- free, free -h
	- ps
	- kill
	- ifconfig
	- 

# 👉 Security
05: security - users
	- accounts for people and services (e.g., nginx or apache)
	- my user
		- whoami
		- home directory
		- files
			- .bashrc
		- groups
			- id <username>
	- other users
		- cat /etc/passwd or getent passwd
			- root:x:0:0:root:/root:/bin/sh
				- root - username
				- x - encrypted password is sotred
				- 0 - user ID
				- 0 - primary group ID
				- root - GECOS (may include user's full name, building, room number, contact)
				- /root - home directory for user
				- /bin/sh - login shell for the user
	- create user
		- sudo useradd -m rcravens or sudo adduser rcravens
		- sudo id rcravens
			- by default creates a new group with the same name as the username
		- sudo passwd rcravens
		- sudo usermod --shell /bin/bash rcravens
	- switching to new user
		- sudo su - rcravens
		- add "alias sudo='sudo '" to .bashrc for user
	- adding / removing user to "sudoers" list
		- sudo usermod -a -G sudo rcravens
		- sudo gpasswd --delete rcravens sudo
	- delete user
		- sudo userdel -r rcravens


06: security - groups
	- easier to manage permissions by assigning users to groups
	- groups for user
		- id <username>
		- group, group <username>
	- all groups
		- getent group
	- create / delete group
		- sudo groupadd demo
		- sudo groupmod -n test demo
		- sudo usermod -a -G test
		- sudo groupdel test

07: security - directory / file permssions
	- read (r), write (w), execute (x)
		- rwx (read, write, and execute)
		- r-- (read only)
		- rw- (read and write)
	- three levels:
		- owner: rwx
		- group: rwx
		- others: rwx
	- ls -la
		- drwx------ 2 ubuntu ubuntu 4096 Sep 10 18:44 .ssh
			- d (or -): directory (or file)
			- rwx: owner
			- ---: group
			- ---: others
			- 2: number of hard links o the directory
			- ubuntu: owner
			- ubuntu: group
			- 4096: size in bytes
			- Sep 10 18:44: date and time last modified
			- .ssh: directory or file name
	- changing permissions
		- change file permissions
			- chmod
		- change file owner
			- chown


08: server management
	- uptime
	- uname
	- lsb_release -a
	- hostname
	- top, htop
	- ssh
	- df, df -h
	- du
	- free, free -h
	- ps
	- kill
	- ifconfig
	- 


09: system updates / install / uninstall software (packages)
	- software is distrubuted as packages
	- packages are online in repositories
	- packages often have dependencies
	- package managers (depends on the distro)
		- apt: Debian and Ubuntu
			- apt, apt-get, apt-cache
			- packages have .deb
		- dnf: RHEL/CentOS 8, Fedora 22
			- dnf, yum
			- packages have .rpm
		- yum: RHEL/CentOS 7, Fedora 21
			- yum
			- .rpm
	- update the apt package index (finds newer packages / versions)
		- sudo apt update
	- upgrade packages
		- sudo apt upgrade
	- install / remove packages
		- sudo apt intall nginx
		- sudo apt remove nginx

10: services
	- 