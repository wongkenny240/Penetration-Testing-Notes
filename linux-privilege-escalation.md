# Post Exploitation - Linux

#### Information Gathering

Key information
* OS release
* Kernel Version
* Available users and current user privileges
* SUID files
* View the installed packages to check for outdated versions

#### OS Version

OS release:
> lsb_release -a

Kernel version
> uname -a

Is there a printer?
> lpstat -a

#### Application & Services
> ps -aux
> ps -ef
> top
> cat /etc/service

a = show processes for all users
u = display the process's user/owner
x = also show processes not attached to a terminal


Determine which services are running as root

> ps aux | grep root
> ps -ef | grep root

Determine what applications are installed and their version
> ls -alh /usr/bin/
> ls -alh /sbin/
> dpkg -l
> rpm -qa
> ls -alh /var/cache/apt/archivesO
> ls -alh /var/cache/yum/
> yum list | grep installed


#### Direction on Privilege Escalation
* Exploit against system
* Exploit against services
* Brute force credentials

SUID files
> find / -perm -u=s -type f 2>/dev/null

Check program version
> [/usr/local/bin/nmap --version]

Pop a shell
> !sh


#### Create an exploit file
> touch exploit.c
> vim exploit.c

Compile
> gcc exploit.c -o exploit

Run
> ./exploit


