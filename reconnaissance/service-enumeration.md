# Service Enumeration
## FTP

### Nmap

'''
nmap -sV -Pn -vv -p [PORT] --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221 [IP_address]

'''

### Hydra
Check for username and password

'''
hydra -s [PORT] -C ./wordlists/ftp-default-userpass.txt -u -f [IP_address] ftp
'''
