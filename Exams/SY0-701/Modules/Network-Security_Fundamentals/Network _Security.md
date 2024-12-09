## Legacy Firewalls
hardware platform or software platform or both that controls the flow of traffic between a trusted network and an untrusted network
### Packet Filtering Firewalls
First-gen packet filtering firewalls (port-based firewalls)
+ Operate up to L4
+ inspects individual packet headers IP SRC, IP DST, PORT, and protocol (TCP, UDP, ICMP) against firewall rulles to allow, block or drop packets.
+ Inspect and handle each packet individually, with no information about context or session.
### Stateful Packet Inspection Firewalls
Second-gen statefull pakcet inspection (dynamic packet filtering) firewalls are fast. \
However, they are port-based and highly dependent on the trustworthiness of the two hosts, because individual packets aren’t inspected after the connection is established.
+ Operate up to L4.
+ *During session establishment only*, inspects individual packet headers IP SRC, IP DST, PORT, and protocol (TCP, UDP, ICMP) against firewall rulles to allow, block or drop packets.
+ Maintain state information about the communication sessions established between hosts on two different networks.
+ **After a permitted connection is established, the firewall allows traffic flow without further inspection** of individual packets during the session.
### Application Firewalls
Third-gen application firewalls (application-layer gateways, proxy-based firewalls, reverse-proxy firewalls).
+ Operate up to L7 and control access to specific applications and services on the network.
+ Requests are sent from the originating host to a proxy server, which analyzes the contents of the data packets and, if the request is permitted, sends a copy of the original data packets to the destination host.
+ inspect L7 traffic, to identify and block specified content, malware, exploits, websites, and applications or services that use hiding techniques such as encryption and non-standard ports.
+ Proxy servers can also be used to implement strong user authentication and web application filtering and to mask the internal network from untrusted networks.
- significant negative impact on the overall performance of the network.

## Intrusion Detection and Prevention (IDS, IPS)
IDSs and IPSs provide real-time monitoring of network traffic and perform deep-packet inspection and analysis of network activity and data. \
IDSs and IPSs examine both the packet header and the payload of network traffic, both can be signature or behavior based.
+  knowledge-based (signature-based):
    + Knowledge-based systems have lower false-alarm rates than behavior-based systems
    + must be continually updated with new attack signatures.
- behavior-based (statistical-anomaly-based) systems:
    - uses a baseline of normal network activity to identify unusual patterns or levels of network activity that might indicate an intrusion attempt.
    - better at detecting new attacks against unknown vulnerabilities.
    - much higher false-positive rate than knowledge-based systems.

```
                 [Red team]
                 {Internet}
                 [Firewall]
                 [  IPS   ] *inline network boundry
                     |
[mangmt system]--[  Switch ]--[ IDS ]
                 ( Network )--[Server]
```

### IDS
+ Is considered a passive system
+ Monitors and analyzes network activity
+ Sends alerts about potential attacks and vulnerabilities on the network
Disadvantages:
- Doesn’t perform any preventive action to stop an attack

### IPS
+ Is considered an active system
+ Performs all of the functions of an IDS
+ Automatically blocks or drops suspicious pattern-matching activity on the network in real time
Disadvantages:
- Must be placed inline along a network boundary and is thus directly susceptible to attack itself
- Can trigger false alarms that inadvertently block authorized users and applications and must be properly identified and filtered
- A false positive occurs when legitimate traffic is improperly identified as malicious traffic.
- Can be used to deploy a denial-of-service (DoS) attack by flooding the IPS, thus blocking connections until no connection or bandwidth is available






      
