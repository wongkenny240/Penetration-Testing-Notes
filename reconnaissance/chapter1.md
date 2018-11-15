# Information Gathering

The recon-phase is usually divided up into two phases.+

1. Passive information gathering / OSINT This is when you check out stuff like:
   * Web information
   * Email Harvesting
   * Whois enumeration
2. Active information gathering
   * ICMP Ping
   * TCP/UDP Scan

This is when you start scanning the target with your different tools.

#### Definition

_**Active fingerprinting**_ is the process of transmitting packets to a remote host and analysing corresponding replies.

_**Passive fingerprinting**_ is the process of analysing packets from a host on a network. In this case, fingerprinter acts as a sniffer and doesn't put any traffic on a network

## Passive Information Gathering

Domain Name Registration: `whois [example.com]`

Find IP Address: `host [www.example.com]`

Zone transfer: `host -l [www.example.com] [DNS server]`

## Active Information Gathering


## netdiscover

Network discovery - discover internal IP addresses

```
netdiscover -i etho
```

## masscan

Scan for a selection of ports (-p22,80,445) across a given subnet (192.168.1.0/24):

```
masscan -p22,80,445 192.168.1.0/24
```

scan a range of ports using the dash

```
masscan 10.11.0.0/16 -p22-25
```

scan a class B subnet for the top 100 ports

```
masscan 10.11.0.0/16 ‐‐top-ports 100
```
By default, masscan scans at a rate of 100 packets per second, which is quite slow. To increase that, simply supply the -rate option and specify a value.

```
masscan 10.11.0.0/16 ‐‐top-ports 100 -rate 100000
```

First, you can just use the standard Unix redirector to send output to a file:

```
masscan 10.11.0.0/16 ‐‐top-ports 100 > results.txt
```

- -oX filename: Output to filename in XML.
- -oG filename: Output to filename in Grepable format.
- -oJ filename: Output to filename in JSON format.


## Nmap

First Stage of Enumeration

`nmap -sP 10.0.0.0/24`

`nmap -p 1-65535 -sV -sS -T4[target]`

### Basic Command

Port: `-p 1-1024`

Fast Mode: `-F`

UDP Port: `-p U:53`

### Scan from file

Scan a list of IP addresses:`nmap -iL ip-addresses.txt`

### Output formats

Normal output \(screen\): `-oN`

grep:`-oG`

XML: `-oX`

Conversion from XML to HTML \(xsltproc\):`xsltproc myscan.xml -o myscan.html`

### Service Version Detection

Determine service/version info: `-sV`

### OS Detection

OS Detection: `-O`

### Nmap scripts

nmap scripts are put in `/usr/share/nmap/scripts`

run default script: `-sC`

run specific script: `--script <filename>|<catergory>|<directories>`

run help menu of specific script: `--script-help <nameOfScript>`

### Different Scan Technique

TCP SYN Scan

```text
 -sS
```

* half-open scanning
* send a SYN packet and wait for response
* if SYN/ACK or SYN -&gt; port is listening \(**open**\)
* if RST -&gt; port is non-listener \(**closed**\)
* if no response or ICMP unreachable error is received, port is marked as filtered

TCP connect scan

```text
 -sT
```

* complete conneciton
* decent IDS will catch/ system log will record
* for user without raw packet privileges only

UDP scan

```text
 -sU
```

* DNS \(53\), SNMP \(161/162\), DHCP \(67/68\) are common UDP port
* ICMP port unreachable error \(type 3, code 3\) -&gt; **closed**
* ICMP unreachable errors \(type 3, codes 0,1,2,9,10,13\) -&gt; **filtered**
* response -&gt; **open**
* no response -&gt; **open\| filtered**

XMAS scan

```text
 -sX
```

* send a packet with FIN, URG, PSH flags
* no response -&gt; **open** \(ignore the packet\)
* RST/ACK -&gt; **closed**
* only work on target that follow RFC 793 implementation
* **not work against Windows**

FIN scan

```text
 -sF
```

* send a packet with FIN only
* same response and limitation as XMAS

NULL scan

```text
 -sN
```

* send a packet with no flags set.

IDLE scan

* send a SYN packet with a spoofed IP address 
* also call zombie scan

IP protocol scan

```text
 -sO
```

* determine which IP protocols \(TCP, ICMP, IGMP\) are supported by target machines


### Logging
`tee filename` reads from stdin and writes to stdout and a file, so all the output of your command shows up in your terminal as normal, but it's also logged to a file.

```
nmap -sS -A --top-ports 1000 target.ip | tee nmap.txt 
```

### Other scanning tools

_**Superscan \(Active\)**_ is connect-based port scanning software designed to detect open TCP and UDP ports on a target computer, determine which services are running on those ports, and run queries such as whois, ping, ICMP traceroute, and Hostname lookups.

_**NBTScan \(Active\)**_ is a command-line tool that scans for open NETBIOS nameservers on a local or remote TCP/IP network, and this is a first step in finding of open shares.

_**hping2 \(Active\)**_ is a tool that can perform OS fingerprinting such as TCP, User Datagram Protocol \(UDP\), ICMP, and raw-IP ping protocols, traceroute mode, and the ability to send files between the source and target system.

* can be used to send custom ICMP, UDP, TCP packets
* SA flag -&gt; port open
* RA flag -&gt; port closed

_**SNMP Scanner \(Active\)**_ allows you to scan a range or list of hosts performing ping, DNS and SNMP queries.

_**p0f \(passive\)**_ is a tool that utilizes an array of sophisticated, purely passive traffic fingerprinting mechanisms to identify the players behind any incidental TCP/IP communications \(often as little as a single normal SYN\) without interfering in any way. It is used when NMap probes are blocked.

_**NetworkMiner \(passive\)**_

_**Satori \(passive\)**_

