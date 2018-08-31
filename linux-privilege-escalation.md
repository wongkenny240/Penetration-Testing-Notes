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


##### Determine which services are running as root

> ps aux | grep root

> ps -ef | grep root

##### Determine what applications are installed and their version
> ls -alh /usr/bin/

> ls -alh /sbin/

> dpkg -l

> rpm -qa

> ls -alh /var/cache/apt/archivesO

> ls -alh /var/cache/yum/

> yum list | grep installed

##### Determine versions of important applications
> gcc -v

> mysql --version

> java -version

> python --version

> ruby -v

> perl -v

##### Review system configurations

Syslog Configuration:
> cat /etc/syslog.conf

Web Server Configurations:
> cat /etc/chttp.conf

> cat /etc/lighttpd.conf

> cat /etc/apache2/apache2.conf

> cat /etc/httpd/conf/httpd.conf

> cat /opt/lampp/etc/httpd.conf

PHP Configuration:

> /etc/php5/apache2/php.ini

Printer (cupsd) Configuration:

> cat /etc/cups/cupsd.conf

MySQL Configuration:

> cat /etc/my.conf

Inetd Configuration:
cat /etc/inetd.conf

List All
> ls -aRl /etc/ | awk '$1 ~ /^.*r.*/'

##### Determine scheduled jobs

> crontab -l

> ls -alh /var/spool/cron

> ls -al /etc/ | grep cron

> ls -al /etc/cron*

> cat /etc/cron*

> cat /etc/at.allow

> cat /etc/at.deny

> cat /etc/cron.allow

> cat /etc/cron.deny

> cat /etc/crontab

> cat /etc/anacrontab

> cat /var/spool/cron/crontabs/root`




#### Communications and Networking


#### Confidential Information & Users
> id

> who

> w

> last

> cat /etc/passwd | cut -d: -f1    # List of users

> grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}'   # List of super users

> awk -F: '($3 == "0") {print}' /etc/passwd   # List of super users

> cat /etc/sudoers

> sudo -l

##### List Sudoers

> cat /etc/sudoers

##### Attempt to display sensitive files

> cat /etc/passwd

> cat /etc/group

> cat /etc/shadow

> ls -alh /var/mail/

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


