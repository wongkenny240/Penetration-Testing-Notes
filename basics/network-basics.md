# Network Basics

**whois** query the domain registrar's database, run on **TCP port 43**

## DNS

* convert IP address to domain names

DNS Structure

## TCP Flags \(Control Bits\)

**SYN** – The SYN, or Synchronisation flag, is used as a first step in establishing a 3-way handshake between two hosts. Only the first packet from both the sender and receiver should have this flag set.  
**ACK** – The ACK flag, which stands for “Acknowledgment”, is used to acknowledge the successful receipt of a packet. It is sent by receiver.  
**FIN** – The FIN flag, which stands for “Finished”, means there is no more data from the sender. Therefore, it is used in the last packet sent from the sender.  
**URG** – The URG flag is used to notify the receiver to process the urgent packets before processing all other packets. The receiver will be notified when all known urgent data has been received. \(RFC 6093\)  
**PSH** – The PSH flag, which stands for “Push”, is somewhat similar to the URG flag and tells the receiver to process these packets as they are received instead of buffering them.  
**RST** – The RST flag, which stands for “Reset”, is sent from the receiver to the sender when a packet is sent to a particular host that was not expecting it.  
ECE – This flag is responsible for indicating if the TCP peer is ECN capable. \(RFC 3168\)  
CWR – The CWR flag, which stands for Congestion Window Reduced, is used by the sending host to indicate it received a packet with the ECE flag set. \(RFC 3168\)  
NS \(experimental\) – The NS flag, which stands for Nonce Sum, is still an experimental flag used to help protect against accidental malicious concealment of packets from the sender. \(RFC 3540\)

## 3 way handshake

This involves a SYN sent to an TCP open port that has a service bound to it, typical examples are HTTP \(port 80\), SMTP \(port 25\), POP3 \(port 110\) or SSH \(port 22\).

* Client sends SYN
* Server returns SYN/ACK
* Client sends ACK

![](../assets/2018-03-07%2017_49_56-Start.png)

## Filtered ports or when the firewall drops a packet

![](../assets/2018-03-07%2017_50_28-Start.png)![](../assets/2018-03-07%2017_50_17-Start.png)

* no service running on the target port
* firewall block access
* no response -&gt; filtered

## Closed ports or when the firewall fails

* no service but firewall allow the connection to go through
* server response with RST/ACK -&gt;  closed

Below link for reference:

[https://hackertarget.com/nmap-tutorial/](https://hackertarget.com/nmap-tutorial/)

[https://www.keycdn.com/support/tcp-flags/](https://www.keycdn.com/support/tcp-flags/)

