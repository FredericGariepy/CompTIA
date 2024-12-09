Attacks:
+ Examples of attack software used by hackers to target IoT devices include Gafgyt, Mirai, and Muhstik botnets. \
+ Hackers can easily identify new targets by using websites such as https://www.shodan.io/
+ Network firewalls may not be able to decrypt all traffic because of regulations and laws. This restriction provides a window of opportunity for attackers to bypass a firewall’s protection to exploit a host by encrypting traffic.
     + When the endpoint decrypts the traffic, the malware is then exposed, necessitating endpoint security to prevent endpoint exploitation.

IoT:
+  machine-to-machine (M2M)
+  wide-area IoT
+ short-range IoT
+ massive-and-critical IoT
+ multi-access edge computing (MEC) devices.

Traditional endpoint security encompasses numerous security tools:
+ anti-malware software
+ personal firewalls
+ host intrusion prevention system (HIPS)
+ mobile application management (MDM) software
+ data loss prevention (DLP) software

| Term | Definition |
| - | - |
| Metamorphism | malware that is capable of changing its code and signature patterns with each iteration. |
| Polymorphism | malicious code can change in a variety of ways, including changing filenames or using encryption with variable keys, to avoid detection. |
| zero-day exploit | cyberattack that occurs against a new vulnerability that has not been fixed. |
| Malspam | unsolicited emails that direct users to malicious websites or prompt users to open attached files with hidden malware |



Antivirus software uses file signatures to discover and mitigate malware on an endpoint. \
antivirus software signatures have to be constantly updated to match new or evolving malware attacking endpoints.
- Malspam is the most popular delivery method for malware.

## Anti-Malware
**(signature-based, container-based, application allow listing, anomaly-based techniques)|**

### Signature-Based
Continuously collect malware samples, create matching signature files for those samples, and distribute those signature files as updates for their endpoint security products to all of their customers. 
+ very popular, oldest method
- Reactive countermeasure
- Before the new signature is created for the malware, the endpoint is unprotected.

**Deployment of signature-based** anti-malware software requires installing an **engine that typically has kernel-level access** to an endpoint’s system resources.
Signature-based anti-malware software scans an endpoint’s hard drive and memory based on a predefined schedule and in real time when a file is accessed.

If a known malware signature is detected, the software performs one of following three predefined actions.
- Quarantine
    - Isolates the infected file so that it cannot infect the endpoint or other files
- Alert
    - Notifies the user (and/or system administrator) that malware has been detected
- Delete
    - Removes the infected file

### Container-Based Endpoint Protection
Container-based endpoint protection wraps a protective virtual barrier around vulnerable processes while they are running. If a process is malicious, the container detects it and shuts it down, preventing it from damaging other legitimate processes or files on the endpoint.
- Computing Resources
    - typically requires a significant amount of computing resource overhead, and attacks have been demonstrated that circumvent or disable container-based protection.
- Application Support
     -  requires knowledge of how protected applications work and interact with other software components.
### Application Allow Listing
requires a positive control model in which no applications are permitted to run on the endpoint unless they are explicitly permitted by the allow list policy. \
- In practice, application allow listing requires a large administrative effort to establish and maintain a list of approved applications
- trends such as cloud and mobile computing, consumerization, and bring your own device (BYOD) and bring your own access (BYOA) policies make application allow listing extremely difficult to enforce in the enterprise.
- After an application is added to an allow list, it is permitted to run even if the application is vulnerable to exploitation.

### Anomaly-Based Detection
relies on first establishing an accurate baseline of what is considered “normal” activity. \
This approach has been around for many years and requires a very large dataset to reduce the number of false-positives.

- **Anomaly-based** detection refers to detecting patterns in datasets that do not conform to an established normal behavior.
- **heuristic/behavior-based** anomaly detection solutions rest on endpoints, using algorithms to detect unusual activity on the endpoint.
    - Heuristic-Based: detects anomalous packet and traffic patterns, such as port scans and host sweeps
    - Behavior-Based: malware detection evaluates an object based on its intended actions before it can actually execute that behavior.

## Golden Image
Endpoint security begins with a standard (“golden”) image that ensures consistent configuration of devices across the organization, which includes disabling or removing operating system features and services that are not needed (“hardening”), installing current security updates, and installing core applications.
In practice, an organization will deploy numerous golden images.

## Firewalls Types
HIPS is another approach to endpoint protection that rely on an agent installed on the endpoint to detect malware.

### Network Firewalls
Most traditional port-based network firewalls do little to protect endpoints inside the enterprise network from threats that originate from within the network, 
### Host-Based Firewalls
Personal firewalls typically operate as Layer 7 (Application layer).
They allow or block traffic based on an individual (or group) security policy.
- disabling or otherwise bypassing a personal firewall is a common and basic objective in most advanced malware today.
### Operating System Firewalls
- Windows Firewall is an example of a personal firewall, default on Windows desktop or mobile operating system.
- Netfilter, or iptables, is the most popular open source, command line interface-based Linux firewall.

### Host-Based Intrusion Prevention Systems (HIPS)
- signature-based or anomaly-based, making it susceptible to the same issues as other signature- and anomaly-based endpoint protection approaches.
- HIPS software often causes significant performance degradation on endpoints.

## Mobile Device Management (MDM)
| OS | term | Defnintion |
| - |- |- |
| Apple OS | Jailbreaking | process of removing software restrictions imposed by Apple in order to install unauthorized applications or operating systems on Apple devices. |
| Andoird OS | Rooting | process of removing software restrictions imposed by Android device vendors in order to install unauthorized applications or operating systems |

MDM centralized management:
- Data Loss Prevention (DLP): Restrict what type of data can be stored on or transmitted from the device
- Policy Enforcement: Enforce security policies, such as those involving passcodes, encryption, lock-down security settings, jailbreaking, or rooting
- Malware Protection: Detect and prevent breaches from mobile malware
- Software Distribution: Remotely install software, including patches and updates, over a cellular or Wi-Fi network
- Remote Erase/Wipe: Securely and remotely delete the complete contents of a lost or stolen device
- Geofencing and Location Services: Restrict specific functionality in the device based on its physical location

### Server Management







