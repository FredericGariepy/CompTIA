## Firewalls
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

## Web Content Filters
Seee [Basic URL filtering mechanism (w/ Squid Proxy)](https://github.com/FredericGariepy/CompTIA/blob/main/Exams/SY0-701/CertPreps/Prep_20.md)

## Virtual Private Networks (VPN)
A VPN creates a secure, encrypted connection (or tunnel) across the internet between two endpoints.
+ site-to-site VPN establishes a secure connection between two organizations' networks, usually geographically separated.
+ A client VPN establishes a secure connection between a user and an organization's network

1. The VPN client connects to a VPN server, such as a firewall, router, or VPN appliance (or concentrator).
2. After a VPN tunnel is established, a remote user can access network resources, such as file servers, printers, and Voice over IP (VoIP) phones, as if they were physically in the office.

### VPN Composition

**Layer 2 Tunneling Protocol (L2TP)**
- L2TP is supported by most operating systems (including mobile devices).
- Although **L2TP provides NO Encryption** *by itself*, it is *considered secure when used with IPsec*.

**Secure Socket Tunneling Protocol (SSTP)**
- Microsoft created SSTP as a VPN tunnel for transporting PPP or L2TP traffic through an SSL 3.0 channel.
- SSTP is primarily used for secure remote client VPN access, rather than for site-to-site VPN tunnels.

**OpenVPN**
- OpenVPN is a highly secure, open-source VPN implementation that uses SSL/TLS encryption for key exchange.
- OpenVPN uses up to 256-bit encryption and can run over TCP or UDP.
- Although OpenVPN is not natively supported by most major operating systems, it has been ported to most major operating systems, including mobile device operating systems.

**Microsoft Point-to-Point Encryption (MPPE)**
- MPPE encrypts data in Point-to-Point Protocol (PPP) based dial-up connections and PPTP VPN connections.
- MPPE uses the RSA RC4 encryption algorithm to provide data confidentiality and supports 40-bit and 128-bit session keys.

### Point-to-Point Tunneling Protocol (PPTP) (OLD)
+ PPTP is a basic VPN protocol that uses TCP port 1723 to establish communication with the VPN peer.
+ PPTP then creates a Generic Routing Encapsulation (GRE) tunnel that transports encapsulated Point-to-Point Protocol (PPP) packets between the VPN peers.
+ PPTP is easy to set up and fast.
- However, PPTP is perhaps the least secure VPN protocol, so it is now seldom used.

**PPP VPN Use cases**
PPTP is commonly used with Password Authentication Protocol (PAP), Challenge-Handshake Authentication Protocol (CHAP), or Microsoft CHAP versions 1 and 2 (MS-CHAP v1/v2), **all of which have well-known security vulnerabilities**, to authenticate tunneled PPP traffic.

***Extensible Authentication Protocol Transport Layer Security  (EAP-TLS)**
+ (EAP-TLS) is a more secure authentication protocol for PPTP.
- However, EAP-TLS requires a public key infrastructure (PKI) and is therefore more difficult to set up

### Internet Protocol Security (IPsec)
IPsec is most commonly used in site-to-site or device-to-device VPN connections. \
IPsec is a secure communications protocol that authenticates and encrypts IP packets in a communication session. \
+ IPsec VPN requires compatible VPN client software to be installed on the endpoint device.
+ A group password or key is required for configuration
+ Client-server IPsec VPNs typically require user action to initiate the connection, such as launching the client software and logging in with a username and password. 
- Security association (SA) in IPsec defines how two or more entities use IPsec to securely communicate over the network.
- A single Internet Key Exchange (IKE) SA is established between communicating entities to initiate the IPsec VPN tunnel.
- Separate IPsec SAs are then established for each communication direction in a VPN session. 
+ IPsec VPN can be configured to force all of the user’s internet traffic back through an organization’s firewall (degrades performance).
- **Split tunneling** can be configured to allow internet traffic from the device to go directly to the internet but route other types of traffic through the IPsec tunnel (acceptable protection, less degration).
- split tunneling configuration can create a “side door” into the organization’s network, perfonal firewall is necessary on the endpoint.

### Secure Sockets Layer (SSL)
SSL is an asymmetric/symmetric encryption protocol that secures communication sessions. \
SSL VPN technology is the standard method of connecting remote endpoint devices back to the enterprise network.

+ **agentless SSL VPN** requires only that users launch a web browser, use HTTPS to open a VPN portal or webpage, and log in to the network with their user credentials.
- **agent-based SSL VPN** connection creates a secure tunnel between a SSL VPN client installed on a host computer/laptop and a VPN concentrator device in an organization's network. Agent-based SSL VPNs are often used to securely connect remote users to an organization's network.





















