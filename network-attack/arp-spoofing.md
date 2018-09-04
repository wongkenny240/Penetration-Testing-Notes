# ARP Spoofing

ARP spoofing is a type of attack in which a malicious actor sends falsified ARP \(Address Resolution Protocol\) messages over a local area network. This results in the linking of an attacker’s MAC address with the IP address of a legitimate computer or server on the network. Once the attacker’s MAC address is connected to an authentic IP address, the attacker will begin receiving any data that is intended for that IP address.

Victim \(not yet compromised\) broadcast ARP Request to all hosts on the network.

Router issued ARP Response and sent towards the requesting host.

Victim pair Layer 2 MAC Address 00:11:45:02:0A:68 with the Layer 3 IP Address 192.168.1.1

Traffic will be directed to MAC Address 00:11:45:02:0A:68

![](https://github.com/wongkenny240/Penetration-Testing-Notes/tree/46f291a769efee2fa73a30a1e957eae1260ee5a5/assets/arp_1.png)

Attacker attack by sending an ARP Reply to both the router and the victim.

![](https://github.com/wongkenny240/Penetration-Testing-Notes/tree/46f291a769efee2fa73a30a1e957eae1260ee5a5/assets/arp_2.png)

Now ARP table in Router \(**192.168.1.1**\) is as below

| 192.169.1.106 | 00:DE:AD:BE:EF:01 |
| :--- | :--- |


And ARP table in Victim \(**192.168.1.106**\) is as below

| 192.169.1.1 | 00:DE:AD:BE:EF:01 |
| :--- | :--- |


00:DE:AD:BE:EF:01 is the attacker's MAC address

Further details:

[http://www.shortestpathfirst.net/2010/11/18/man-in-the-middle-mitm-attacks-explained-arp-poisoining/](http://www.shortestpathfirst.net/2010/11/18/man-in-the-middle-mitm-attacks-explained-arp-poisoining/)

