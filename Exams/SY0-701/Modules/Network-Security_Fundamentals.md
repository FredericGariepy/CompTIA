Network fundamentals review

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

## Domain Name System (DNS)


































