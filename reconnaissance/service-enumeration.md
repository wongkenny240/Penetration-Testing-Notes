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

## 80/443/8080: HTTP/HTTPS

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

![Open DirBuster](../.gitbook/assets/image%20%284%29.png)

![Choose a wordlist](../.gitbook/assets/image%20%282%29.png)

![Result](../.gitbook/assets/image%20%283%29.png)

### wafw00f 

 Wafw00f identifies if a particular web address is behind a web application firewall.
 
 #### http

```
wafw00f http://[IP]:[PORT], "http,https,ssl,soap,http-proxy,http-alt"
```


 #### https
 
```
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

## 137/139/445: NetBIOS/SMB

### enum4linux

Do Everything, runs all options apart from dictionary based share name guessing


```
enum4linux -a [ip_addr]

```


Lists usernames, if the server allows it - (RestrictAnonymous = 0)

```
enum4linux -U [ip_addr]
```

