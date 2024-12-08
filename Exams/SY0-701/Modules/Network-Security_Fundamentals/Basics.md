Network fundamentals Basics review

## Routing
| | |
|-|-|
|Convergence| Time required for all routers to update their routing table with most current information.|
|Flapping|When a **route** or **interface** repeatedly changes state (Up, Down, Up, Down, ...) over a short period fon time.|
|Backhauling| Sending network traffic to a central data center (or headquarters) before it reaches its final destination.|


## Static Routing
Routes are created manually on router (or other network device).
- If static route is *down*, traffic can not be automatically re-routed unless alternate route was configured.
- If static route is *congested*, trafic can not be automatically rerouted over less congested alternative route.
+ Practical for *special case* e.g.: DST is used as backup route, DST is reachable only through 1 router.
+ Low bandwifth requirements, (no broadcast)
+ Security where traffic can route only to DST specified in static route table.

## Dynamic Routing (*classes*: distance vector, link state, path vector)
Dynamic routing protocol can automatically lean new/alternate routes, determine best route to DST. \
Routing table is updated periodically with current routing information.

### Distance vector routing (Dynamic):
Makes routing decision based on:
+ Distance (hop count , or other metric)
+ Vector (exit router interface)
- *Without* Convergence, some routers will be unaware of network topology changes and send trafic to invalid DST.
- *Durring* Convergence, routing information exchange slows down the network, can take several minutes.

Routing Information Protocol (RIP), a distance-vector routing protocol, uses hop count as its routing metric. \
RIP prevents network loops by:
- **hop limit of 15**. RIP implements 15 hop limit, this also limits the side of networks RIP can support.
- **Split Horizon**. Prevent router to advertise a route back out through the same interface from which the route was learned. https://geek-university.com/split-horizon-explained/
- **Triggered Updates**. When change is detected, update gets sent immediately instead of waiting (30 sec.) to send periodic RIP update.
- **Route Poisoning**. Set hop count on ad route to 16, effectively advertises the route as unreachable (hop count > hop limit).
- **Hold Down Timers**. Helps with Flapping. When router receives information that DST hop >= 16 (is unreachable ), a 180s timer (default) will start and *route updates are only accepted from router that originally advertised the route*. https://geek-university.com/holddown-timer-explained/


### Link State (Dynamic)
Link-state protocol requires every router to calculate and maintain a complete map, or routing table, of the entire network. \
periodically transmit updates that contain information about adjacent connections, or link states, to all other routers in the network.
- Compute-Intensive
- Link states considers: link speed, delay, load, reliability, cost (arbitrary weight or metric)
+ Calculate most efficient route to DST
+ Convergence occurs very fast (seconds)

Open Shortest Path First (OSPF) is a link state routing procol in large enterprise networks.
+ OSPF routes network traffic within a single autonomous system (AS).
+ OSPF networks are divided into areas identified by 32-bit area identifiers.
+ Area identifiers can (but don’t have to) correspond to network IP addresses and can duplicate IP addresses without conflicts.

### Path Vector (Dynamic)
Similar to Distance-vector, withOut hop limit scale issue (15). \
+ **Border Gateway Protocol (BGP)** is a path-vector used between separate autonomous systems (AS).
+ **BGP is the core protocol used by internet service providers (ISPs) and network service providers (NSPs)**, as well as on very large private IP networks.

## Local Area Network (LAN)
A star topology is ideal for practically any size environment and is the most commonly used basic LAN topology. \
A mesh topology may be used throughout the network or only for the most critical network components such as routers, switches, and servers to eliminate performance bottlenecks and single points of failure. \
Equipment in LAN:
+ bridges
+ hubs
+ repeaters
+ switches
+ wireless APs

## Wide Area Network (WAN)
Connection of LANs or other WANs. \
Each router has a data plane, which holds the information, and a control plane, which tells the data where to go. \
Where data flows is typically determined by a network engineer or administrator who writes rules and policies. \
Equipment in WAN:
+ servers
+ firewalls
+ modems
+ routers
+ virtual private network (VPN) gateways
+ WAN switches. 

### Software-defined WAN (SD-WAN)
SD-WAN separates the control and management processes from the underlying networking hardware, making them available as software that can be easily configured and deployed. \
A centralized control plane means network administrators can write new rules and policies, and then configure and deploy them across an entire network at once.
+ WAN managers can create and update security rules in real time as network requirements change, because each device is centrally managed (routing based on application policies).
+ SD-WAN with zero-touch provisioning, automates deployment and configuration processes, this reduces complexity, resources, and operating expenses required to turn up new sites.
+ SD-WAN avoids backhauling by sending traffic directly to the cloud.

### Virtual Local-Area Networks (VLANs)
- VLANs segment broadcast domains in a LAN, typically into logical groups (such as business departments). \
- VLANs are created on network switches. 

### Wireless / Personal Area Networks (WPANs / PANs)
Connect an individual’s electronic devices (laptops, smartphone, virtual personal assitants (Alexa, Siri, ...)) and wearables.

## Fully qualified domain name (FQDN) ... Parts of URL
| Scheme | Subdomain | Second-level domain| Top-level domain| Subdirectory |
| - | - | - | - | - |
|https:// | www. | spamhaus. | org | /reputation-statistics/cctlds/domains/ |

## Domain Name System (DNS)
Transalte domain name to IP. \
![DNS Lookup Process](https://cf-assets.www.cloudflare.com/slt3lc6tev37/1NzaAqpEFGjqTZPAS02oNv/bf7b3f305d9c35bde5c5b93a519ba6d5/what_is_a_dns_server_dns_lookup.png)

### DNS Record Types (A, AAAA, CNAME, MX, PTR, SOA, NS, TXT)
+ **A (IPv4) or AAAA (IPv6)** address maps a domain or subdomain to an IP address or multiple IP addresses.
+ **Canonical Name (CNAME)** maps a domain or subdomain to another hostname.
+ **Mail Exchanger (MX)** specifies the hostname or hostnames of email servers for a domain.
```
C:\Users\BlueTeam>nslookup -type=MX google.com
Non-authoritative answer:
google.com      MX preference = 10, mail exchanger = smtp.google.com
```
+ **Pointer (PTR)** points to a CNAME. For reverse DNS lookup. *"What's the domain of IP 8.8.8.8?"* \
`nslookup 8.8.8.8`
+ **Start of Authority (SOA)** specifies authoritative information about a DNS zone such as primary name server, email address of the domain administrator, and domain serial number.
```
C:\Users\BlueTeam>nslookup -type=SOA google.com
Non-authoritative answer:
google.com
        primary name server = ns1.google.com
        responsible mail addr = dns-admin.google.com
        serial  = 703767055
        refresh = 900 (15 mins)
        retry   = 900 (15 mins)
        expire  = 1800 (30 mins)
        default TTL = 60 (1 min)
```
+ **Name Server (NS)** record specifies an authoritative name server for a given host. 
```
C:\Users\BlueTeam>nslookup -type=NS example.com
Non-authoritative answer:
example.com     nameserver = a.iana-servers.net
example.com     nameserver = b.iana-servers.net
````
+ **Text (TXT)** stores text-based information.


### Side notes
Tips on a getting a good domain
- Stay away from hyphens in your domain
- Stay away from numbers in your domain
- Stay away from words that are numbers (five, ten, etc.), in your domain (I find that telling people your domain with these can complicate things; i.e., 'is that a 5 or f.i.v.e.?)
- Stay away from any of these TLDs (these change over time - dig around this site): https://www.spamhaus.org/statistics/tlds/
- Pick a TLD / registrar with solid WHOIS privacy capabilities
- Pick a reputable registrar (... you'll have 1M opinions on this topic)
- Don't buy a domain at the same place where you host your website
- Setup auto-renew
- Buy a domain for several years out (10yrs. +)

## IoT
Palo Alto Networks Unit 42 threat intelligence team (2024):
- "...the general security posture of IoT devices is declining.."
- 98% of all IoT device traffic is *unencrypted*.
- 57% of IoT devices are vulnerable to medium- or high-severity attacks.
- 40% of medical imaging devices run on unsupported operating systems.
- 65% of healthcare organizations have experienced a security incident involving imaging devices.
- 72% percent of healthcare VLANs mix IoT and IT assets.

### Cellular
+ **2G/2.5G**: Due to the low cost of 2G modules, relatively long battery life, and large installed base of 2G sensors and M2M applications, 2G connectivity remains a prevalent and viable IoT connectivity option.
+ **3G**: IoT devices with 3G modules use either Wideband Code Division Multiple Access (W-CDMA) or Evolved High Speed Packet Access (HSPA+ and Advanced HSPA+) to achieve data transfer rates of between 384Kbps and 168Mbps.
+ **4G/Long-Term Evolution (LTE)**: 4G/LTE networks enable real-time IoT use cases, such as autonomous vehicles, with 4G LTE Advanced Pro delivering speeds in excess of 3Gbps and less than 2 milliseconds of latency.
+ **5G**: Ultra-low latency, massive connectivity and scalability for IoT devices, more efficient use of licensed spectrum, and network slicing for application traffic prioritization. 
### Satellite
+ **C-band**: C-band satellite operates in the 4 to 8 gigahertz (GHz) range. It is used in some Wi-Fi devices and cordless phones, as well as surveillance and weather radar systems. 
+ **L-band**: L-band satellite operates in the 1 to 2GHz range. It is commonly used for radars, global positioning systems (GPSs), radio, and telecommunications applications.

### Short-Range Wireless
+ **Wi-Fi/802.11**: The Institute of Electrical and Electronics Engineers (IEEE) defines the 802 LAN protocol standards. 802.11 is the set of standards used for Wi-Fi networks typically operating in the 2.4GHz and 5GHz frequency bands. Some of the most common implementations today include: 
    - 802.11**n** (Wi-Fi 4) operates on 2.4GHz and 5GHz bands at ranges from 54 megabits per second (Mbit/s) to 600Mbit/s.
    - 802.11**ac** (Wi-Fi 5), operates on the 5GHz band at ranges from 433Mbit/s to 3.46 gigabits per second (Gbit/s).
    - 802.11**ax** (Wi-Fi 6), operates on the 2.4GHz and 5GHz bands (And *all bands between 1 and 6GHz*, when they become available for 802.11 use) at ranges up to 11Gbit/s. 

+ **Zigbee/802.14**: ZigBee is a low-cost, low-power wireless mesh network protocol based on the IEEE 802.15.4 standard. ZigBee is the dominant protocol in the low-power networking market, with a large installed base in industrial environments and smart home products.
+ **Adaptive Network Technology + (ANT+)**: ANT+ is a proprietary multicast wireless sensor network technology primarily used in personal wearables, such as sports and fitness sensors.
+ **Internet Protocol version 6 (IPv6) over Low-Power Wireless Personal Area Networks (6LoWPAN)**: 6LoWPAN allows IPv6 traffic to be carried over low-power wireless mesh networks. 6LoWPAN is designed for nodes and applications requiring wireless internet connectivity at relatively low data rates in small form factors, such as smart light bulbs and smart meters.
+ **Bluetooth/Bluetooth Low-Energy (BLE)**: Bluetooth is a low-power, short-range communications technology primarily designed for point-to-point communications between wireless devices in a hub-and-spoke topology. BLE (also known as Bluetooth Smart or Bluetooth 4.0+) devices consume significantly less power than Bluetooth devices and can access the internet directly through 6LoWPAN connectivity.
+ **Z-Wave**: Z-Wave is a low-energy wireless mesh network protocol primarily used for home automation applications such as smart appliances, lighting control, security systems, smart thermostats, windows and locks, and garage doors.

### Low-Power Wide-Area Networks (LP-WAN) and Wireless Wide Area Network (WWAN)
+ **Narrowband IoT (NB-IoT)**: NB-IoT provides low cost, long battery life, and high connection density for indoor applications. It uses a subset of the LTE standard in the 200 kilohertz (kHz) range.
+ **LoRa**: The LoRa Alliance is driving the Long-Range Wide-Area Network (LoRaWAN) protocol as the open global standard for secure, carrier-grade IoT low-power wide-area (LPWA) connectivity, primarily for large-scale public networks with a single operator.
+ **Sigfox**: Sigfox provides subscription-based global cellular LPWA connectivity for IoT devices. The Sigfox network relies on Ultra Narrowband (UNB) modulation and operates in unlicensed sub-GHz frequency bands.
+ **Worldwide Interoperability for Microwave Access (WiMAX)**: WiMAX is a family of wireless broadband communications standards based on the IEEE 802.16 standards. WiMAX applications include portable mobile broadband connectivity, smart grids and metering, and internet failover for business continuity.

### Identity of Things (IDoT)
IDoT refers to identity and access management (IAM) solutions for the IoT. \
IDOT solutions manage human-to-device, device-to-device, and/or device-to-service/system IAM by: 
- Establishing a naming system for IoT devices.
- Determining an identity lifecycle for IoT devices, ensuring that it can be modified to meet the projected lifetime of IoT devices.
- Creating a well-defined process for registering IoT devices. The type of data that the device will be transmitting and receiving should shape the registration process.
- Defining security safeguards for data streams from IoT devices.
- Outlining well-defined authentication and authorization processes for admin local access to connected devices.
- Creating safeguards for protecting different types of data, making sure to create privacy safeguards for personally identifiable information (PII).
