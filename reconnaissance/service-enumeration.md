# Service Enumeration

## 21: FTP

### Nmap

```text
nmap -sV -Pn -vv -p [PORT] --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221 [IP_address]
```

ftp-anon.nse: Attempt to gain access without authentication or through the anonymous user account by way of nmap. This often allows full access to almost all files and folders on a host

### Hydra

Check for username and password

```text
hydra -s [PORT] -C ./wordlists/ftp-default-userpass.txt -u -f [IP_address] ftp
```

### Other

Check xml, ini, log, and txt files for user passwords/hashes. Passwords and user logs are often left inside of these files which may lead to web or SSH access.

## 22: SSH

### Hydra

Manual password bruteforcing

-l \(single username\) or -L \(username list\) -p \(single password\) or -P \(password list\) -t \(number\) - number of tasks to run, similar to multi-threading but instead reduces the amount of tasks running \(default, 16\) -f - stop the scanner once a valid username and password combo is found -v - verbosity mode \(displays any extra output during the scan\)

```text
hydra -l username -P password_list.txt 192.168.168.168 -f -v ssh
```

## 25/465/587: SMTP

### iSMTP

Test a list of IPs from a file \(-f smtp-ips.txt\) enumerating usernames from a dictionary file \(-e /usr/share/wordlists/metasploit/unix\_users.txt\):

```text
ismtp -f smtp-ips.txt -e /usr/share/wordlists/metasploit/unix_users.txt
```

## 80/443/8080: HTTP/HTTPS

### Nikto

Scanning Webservers for vulnerabilities

Against a host

```text
nikto -host  [hostname or IP]
```

Against multiple host

```text
nmap -p80 192.168.0.0/24 -oG – | nikto -h –
```

### GoBuster

```text
gobuster -u [URL] -w [wordlists]
```

Useful wordlists

```text

```

### Netcat

Banner Grabbing

```text
nc -v -n -w1 [IP] [PORT]
```

### Curl

```text
curl -i [ip_addr]
```

### X11 Screenshot

```text
bash ./scripts/x11screenshot.sh [ip_addr]
```

### CeWL

```text
 cewl http://[ip_addr]:[port_num]/index.html -m 6 -w cewl.lst
```

### w3m

w3m can be utilized to quickly grab the robots.txt from a website

```text
w3m -dump [ip_addr]/robots.txt
```

### DirBuster

![Open DirBuster](../.gitbook/assets/image%20%285%29.png)

![Choose a wordlist](../.gitbook/assets/image%20%282%29.png)

![Result](../.gitbook/assets/image%20%283%29.png)

### wafw00f

Wafw00f identifies if a particular web address is behind a web application firewall.

#### http

```text
wafw00f http://[IP]:[PORT], "http,https,ssl,soap,http-proxy,http-alt"
```

#### https

```text
wafw00f https://[IP]:[PORT], "http,https,ssl,soap,http-proxy,http-alt"
```

### Tips

* PHP pages: Check for the presence of common php default pages and folders such as:

  /phpliteadmin

  /dashboard

  /admin

  /admin.php

  /login

  /login.php

* If PHP is found, check the phpinfo.php file. On occasion hidden credentials will be located at the very bottom of the page
* Check the /robots.txt file for hidden folders
* Look for comments in the HTML source code. Programmers sometimes stick usernames, passwords, and other hints in there that may give you a way into the box

## 135: RPC

rpcinfo can be utilized to enumerate RPC services.

```text
rpcinfo -p [IP]
```

## 137/139/445: NetBIOS/SMB

### enum4linux

enum4linux is an alternative to enum.exe on Windows, enum4linux is used to enumerate Windows and Samba hosts.

Do Everything, runs all options apart from dictionary based share name guessing

```text
enum4linux -a [ip_addr]
```

Lists usernames, if the server allows it - \(RestrictAnonymous = 0\)

```text
enum4linux -U [ip_addr]
```

Pull a full list of users if you can obtain credentials

```text
enum4linux -u administrator -p password -U [ip_addr]
```

Pulls usernames from the default RID range \(500-550,1000-1050\)

```text
enum4linux -r [ip_addr]
```

Pull usernames using a custom RID range

```text
enum4linux -R 600-660 [ip_addr]
```

Perform a dictionary attack, if the server doesn't let you retrieve a share list

```text
enum4linux -s shares.txt [ip_addr]
```

Pulls OS information using smbclient, this can pull the service pack version on some versions of Windows

```text
enum4linux -o [ip_addr]
```

### Impacket's samrdump.py

An application that communicates with the Security Account Manager Remote interface from the MSRPC suite. It lists system user accounts, available resource shares and other sensitive information exported through this service.

```text
 ./samrdump.py [[domain/] username [:password] @] [Target IP Address]
```

![](../.gitbook/assets/image%20%289%29.png)

```text
./samrdump.py [ip_addr] [port]/SMB
```

### smbenum

```text
bash ./scripts/smbenum.sh [ip_addr]
```

### smbmap

#### List Shares & Check null sessions

```text
smbmap -H [ip]
```

If you get credentials, can re-run to show more details

```text
smbmap -H [ip] -d [domain] -u [user] -p [password]
```
e.g `smbmap -u victim -p s3cr3t -H 192.168.86.61`

### Nmap NSE Script

### List Shares
#### smb-enum-shares

Nmap can be utilized to enumerate shares via SMB.

```text
nmap -p [port] --script=smb-enum-shares [IP] -vvvvv
```

#### smb-enum-groups

Nmap can be utilized to enumerate groups via SMB.

```text
nmap -p [port] --script=smb-enum-groups [IP] -vvvvv
```

#### smb-enum-sessions

Nmap can be utilized to enumerate logged in users via SMB.

```text
nmap -p [port] --script=smb-enum-sessions [IP] -vvvvv
```

#### smb-enum-policies

Nmap can be utilized to password policies via SMB.

```text
nmap -p [port] --script=smb-enum-domains [IP] -vvvvv
```

### Check for Vulnerability
#### smb-vulnerability

Nmap can be utilized to check SMB services for known vulnerabilities.

```text
nmap -sV -Pn -vv -p [PORT] --script=smb-vuln* --script-args=unsafe=1 [IP]
```

### smbclient 

#### List shares 

```text
smbclient -L \\[ip]
```

Output

```text
Server time is Sat Aug 10 15:58:27 1996
Timezone is UTC+10.0
Password: 
Domain=[WORKGROUP] OS=[Windows NT 3.51] Server=[NT LAN Manager 3.51]

Server=[ZIMMERMAN] User=[] Workgroup=[WORKGROUP] Domain=[]

        Sharename      Type      Comment
        ---------      ----      -------
        ADMIN$         Disk      Remote Admin
        public         Disk      Public 
        C$             Disk      Default share
        IPC$           IPC       Remote IPC
        OReilly        Printer   OReilly
        print$         Disk      Printer Drivers


This machine has a browse list:

        Server               Comment
        ---------            -------
        HOPPER               Samba 1.9.15p8
        KERNIGAN             Samba 1.9.15p8
        LOVELACE             Samba 1.9.15p8
        RITCHIE              Samba 1.9.15p8
        ZIMMERMAN
```

#### Check null sessions
Connect the share

```text
smbclient \\\\[ip]\\[share name]
```

### RPCClient

#### Check null sessions

```text
bash -c "echo 'srvinfo' | rpcclient [ip_addr] -U%"
```

or 

```text
rpcclient -U "" -N [ip]

```

#### smb-enum-users-rpc

Users can be enumerated through SMB services via RPCClient.

```text
bash -c "echo 'enumdomusers' | rpcclient [IP] -U%"
```

#### rpcinfo

```text
rpcinfo -p [ip_address]
```

## 161: SNMP

### snmpwalk

```text
snmpwalk -c public -v1 [ip_addr]
```

### snmpcheck

```text
snmpcheck -t [ip_addr]
```

## 3389: RDP

### rdp-sec-check

```text
perl ./scripts/rdp-sec-check.pl [ip_addr]:[port]
```

### nmap NSE script

```text
nmap -p 3389 --script rdp-enum-encryption <ip>
```

### ncrack

Ncrack can be utilized to brute force RDP services

```text
ncrack -vv --user administrator -P /usr/share/wordlists/rockyou.txt rdp://[ip addr]
```

