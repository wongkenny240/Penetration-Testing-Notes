#Post Exploitation - Linux

####Information Gathering

Key information
* OS release
* Kernel Version
* Available users and current user privileges
* SUID files
* View the installed packages to check for outdated versions


OS release:
>lsb_release -a

Kernel version
> uname -a

Direction on Privilege Escalation
* Exploit against system
* Exploit against services
* Brute force credentials

SUID files
> find / -perm -u=s -type f 2>/dev/null

Check program version
> [/usr/local/bin/nmap --version]

Pop a shell
> !sh


####Create an exploit file
> touch exploit.c
> vim exploit.c

Compile
> gcc exploit.c -o exploit

Run
> ./exploit


