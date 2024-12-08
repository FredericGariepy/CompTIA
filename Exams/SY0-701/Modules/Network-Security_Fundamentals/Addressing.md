### Loopback and Private Addresses
- **Loopback (or `localhost`) network addresses** are used for testing and troubleshooting.
    - 127.0.0.1 to 127.255.255.255
    - Packets sent to a loopback are immediately routed back to the source host without exiting the source host.
- **Private addresses** are reserved for use in private networks and are not routable on the internet.
    - 10.0.0.0–10.255.255.255 (Class A)
    - 172.16.0.0–172.31.255.255 (Class B)
    - 192.168.0.0–192.168.255.255 (Class C)

### Subnet Mask
number that hides the network portion of an IPv4 address, leaving only the host portion of the IP address.
In binary form, \
1: network reserved address bits, the subnet mask. \
IPv4 example: 11111111.11111111.11111111.00000000 = CIDR /24 : 255.255.255.000 \
0: available adress bit(s) : in the example (above) 2^8 possible addresses, the host portion.

### Subnetting
subnetting is splitting the portion of hosts on a network class address.
In this subnet mask example, we start with a Class 3, /24 network: \
subnetmask = 255.255.255.000 = 11111111.11111111.11111111.00000000 = CIRD /24
|Network Address| First Host|Last Host|Broadcast|
|-|-|-|-|
|192.168.40.000/24|192.168.40.1|192.168.40.126|192.168.40.127|

we take 1 bit from the host portion of this /24 in order to divide the network into two subnets. \
11111111.11111111.11111111.10000000 = CIRD /25 \
we now have:

|Subnet|Network Address| First Host|Last Host|Broadcast|
|-|-|-|-|-|
|Subnet 1|192.168.40.0/25|192.168.40.1|192.168.40.126|192.168.40.127|
|Subnet 2|192.168.40.128/25|192.168.40.129|192.168.40.254|192.168.40.255|

**Network Diagram**
```
[ 192.168.40.0/24 ]  
   ├── 192.168.40.0/25 → Subnet 1 (126 hosts)  
   └── 192.168.40.128/25 → Subnet 2 (126 hosts)
```

**Cisco Router**
```
Router> enable
Router# configure terminal
Router(config)# interface eth0
Router(config-if)# ip address 192.168.40.1 255.255.255.128
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# interface eth1
Router(config-if)# ip address 192.168.40.129 255.255.255.128
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# exit
Router# show running-config  <-- this comands will show the configs with Ethernet0 adn Ethernet1, the two subnets
...
interface Ethernet0
 ip address 192.168.40.1 255.255.255.128
 no shutdown
interface Ethernet1
 ip address 192.168.40.129 255.255.255.128
 no shutdown
```
Subnets themselfs can be further subnetted.




### IPv4
32-bit address space (4 octet).
### IPv6
128-bit address space (32 hexadecimal).
- `::` can be used to represent one or more groups of 16 bits of zeros. Can be used only once.
- Leading zeros in an individual hextet can be omitted, but each hextet must have at least one hexadecimal digit, unless `::` is used.
- **Mixed Environment**: In mixed IPv4 and IPv6 environments, the form x:x:x:x:x;x:d.d.d.d can be used, in which x represents the six high-order 16-bit hextets of the address and d represents the four low-order 8-bit octets (in standard IPv4 notation) of the address.
    - For example, 0db8:0:0:0:0:FFFF:129.144.52.38 is a valid IPv6 address.
    - Can be simplified as db8::ffff:129.144.52.38.

### Network address translation (NAT)
mapping an IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device. \
The simplest type of NAT provides a one-to-one translation of IP addresses which is used to allow host devices configured with a private IP address to send and receive traffic on the internet.
```
    [Host]---User_Net---[Firewall]---{Internet}<-->[Server]
192.168.15.69          192.51.100.22              66.254.114.41
```
|Before NAT:| | After NAT:| |
|-|-|-|-|	
|Source |	Destination	| Source |	Destination|
|192.168.15.69|	66.254.114.41| 198.51.100.22	|66.254.114.41|
|Users_Net|	interenet	|internet|	internet|

## OSI Model
|TCP/IP model| OSI Layer | #| data unit | Description | Protocols |
|-|-------|---|-|-|-|
|Application| Application   | 7 | data| identifies and establishes availability of communication partners, determines resource availability, and synchronizes communication. | FTP:20, FTP:21, HTTP:80, HTTPS:443, HTTPS:8443), IMAP:143, POP3:110, SMTP:25, SNMP:161, SMP:162, Telnet:23 |
|Application| Presentation  | 6 | data |coding and conversion functions, so data sent from one System's L7 to another System's L7 is compatible | ASCII, EBCDIC, GIF, JPEG, MPEG |
|Application| Session       | 5 | data | manages communication sessions between networked systems, including connection establishment, data transfer, and connection release. |Network File System (NFS:2049), Remote procedure call (RPC), SSH:22, Session Initiation Protocol (SIP:5060 unencrypted, SIP:5061 encrypted) |
|Transport | Transport     | 4 | TCP segment, datagram |provides transparent, reliable data transport and end-to-end transmission control. Flow control, Multiplexing, Virtual circuit management, Error checking and recovery | TCP, UDP, Stream Control Transmission Protocol (SCTP)   |
|*Internet*| Network       | 3 | packet, IP datagram | Routers operate at the Network layer of the OSI model. | IP, Routing Protocols (RIP, OSPF, BGP, EIGRP), ICMP |
|Network Access| Data Link     | 2 | Frame |witches typically operate at Layer 2 of the OSI model (although multilayer switches that operate at different layers also exist).  Logical Link Control (LLC)/ Media access control (MAC) | ARP, PPP, MLT|
|Network Access| Physical      | 1 | Frame, bit | sends and receives bits across the network medium | Ethernet, Fast Ethernet, Gigabit Ethernet, WiFi |
