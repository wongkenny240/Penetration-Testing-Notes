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

####Definition

***Active fingerprinting*** is the process of transmitting packets to a remote host and analysing corresponding replies.

***Passive fingerprinting*** is the process of analysing packets from a host on a network. In this case, fingerprinter acts as a sniffer and doesn't put any traffic on a network


### Passive Information Gathering

Domain Name Registration: `whois [example.com]`

Find IP Address: `host [www.example.com]`

Zone transfer: `host -l [www.example.com] [DNS server]`

### Active Information Gathering

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

Conversion from XML to HTML (<span style="color:red">xsltproc</span>):`xsltproc myscan.xml -o myscan.html`

### Service Version Detection

Determine service/version info:  `-sV`

### OS Detection

OS Detection: `-O`

### Nmap scripts

nmap scripts are put in `/usr/share/nmap/scripts`

run default script: `-sC`

run specific script: `--script <filename>|<catergory>|<directories>`

run help menu of specific script: `--script-help <nameOfScript>`

### Different Scan Technique

TCP SYN Scan 

> -sS

* half-open scanning
* send a SYN packet and wait for response
* if SYN/ACK or SYN -> port is listening (**open**)
* if RST -> port is non-listener (**closed**)
* if no response or ICMP unreachable error is received, port is marked as filtered

TCP connect scan
>-sT

* complete conneciton
* decent IDS will catch/ system log will record
* for user without raw packet privileges only

UDP scan
> sU

* DNS (53), SNMP (161/162), DHCP (67/68) are common UDP port
* ICMP port unreachable error (type 3, code 3) -> **closed**
* ICMP unreachable errors (type 3, codes 0,1,2,9,10,13) -> **filtered**
* response -> **open**
* no response -> **open| filtered**

XMAS scan 
>-sX

* send a packet with FIN, URG, PSH flags
* no response -> **open** (ignore the packet)
* RST/ACK -> **closed**
* only work on target that follow RFC 793 implementation
* **not work against Windows**

FIN scan
>-sF

* send a packet with FIN only
* same response and limitation as XMAS

NULL scan
>-sN

* send a packet with no flags set.

IDLE scan

* send a SYN packet with a spoofed IP address 
* also call zombie scan

IP protocol scan

>-sO

* determine which IP protocols (TCP, ICMP, IGMP) are supported by target machines

###Other scanning tools
***Superscan (Active)*** is connect-based port scanning software designed to detect open TCP and UDP ports on a target computer, determine which services are running on those ports, and run queries such as whois, ping, ICMP traceroute, and Hostname lookups.

***NBTScan (Active)*** is a command-line tool that scans for open NETBIOS nameservers on a local or remote TCP/IP network, and this is a first step in finding of open shares.

***hping2 (Active)*** is a tool that can perform OS fingerprinting such as TCP, User Datagram Protocol (UDP), ICMP, and raw-IP ping protocols, traceroute mode, and the ability to send files between the source and target system. 

* can be used to send custom ICMP, UDP, TCP packets
* SA flag -> port open
* RA flag -> port closed

***SNMP Scanner (Active) *** allows you to scan a range or list of hosts performing ping, DNS and SNMP queries.

***p0f (passive)*** is a tool that utilizes an array of sophisticated, purely passive traffic fingerprinting mechanisms to identify the players behind any incidental TCP/IP communications (often as little as a single normal SYN) without interfering in any way. It is used when NMap probes are blocked. 

***NetworkMiner (passive)***

***Satori (passive)***




