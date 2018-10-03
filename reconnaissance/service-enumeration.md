# Service Enumeration
## 21: FTP

### Nmap

```
nmap -sV -Pn -vv -p [PORT] --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221 [IP_address]
```

ftp-anon.nse: Attempt to gain access without authentication or through the anonymous user account by way of nmap. This often allows full access to almost all files and folders on a host

### Hydra
Check for username and password

```
hydra -s [PORT] -C ./wordlists/ftp-default-userpass.txt -u -f [IP_address] ftp
```
### Other
Check xml, ini, log, and txt files for user passwords/hashes. Passwords and user logs are often left inside of these files which may lead to web or SSH access.

## 22: SSH
### Hydra
Manual password bruteforcing

-l (single username) or -L (username list)
-p (single password) or -P (password list)
-t (number) - number of tasks to run, similar to multi-threading but instead reduces the amount of tasks running (default, 16)
-f - stop the scanner once a valid username and password combo is found
-v - verbosity mode (displays any extra output during the scan)

```
hydra -l username -P password_list.txt 192.168.168.168 -f -v ssh
```

## 80/443/8080: HTTP/HTTPS

### Netcat
Banner Grabbing

```
nc -v -n -w1 [IP] [PORT]
```

### Curl 

```
curl -i [ip_addr]
```

### X11 Screenshot

```
bash ./scripts/x11screenshot.sh [ip_addr]
```

### CeWL

```
 cewl http://[ip_addr]:[port_num]/index.html -m 6 -w cewl.lst
```

### w3m
w3m can be utilized to quickly grab the robots.txt from a website

```
w3m -dump [ip_addr]/robots.txt
```

### DirBuster

