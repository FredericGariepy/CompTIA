| Term / Acronym | Expansion | Def. |
|-|-|-|
|ARO|Annual Rate of Occurrence|The estimated frequency of data breaches per year.|
|SLE|Single Loss Expectancy| The estimated cost of a single data breach (including data loss, legal fees, and reputation damage.|
|ALE|Annual Loss Expectancy | ARO * SLE = frequency * cost|
|MOA|Memorandum of Understanding or Agreement|[See: NIST def.](https://csrc.nist.gov/glossary/term/memorandum_of_understanding_or_agreement)|
|SPF|Sender Policy Framework|email authentication protocol designed to prevent email spoofing|
|ASLR|Address Space Layout Randomization|memory-protection process randomizing the location where system executables are loaded into memory|
|MDM|Mobile Device Management|administration of mobile devices, usually implemented by use of a third-party product with management features for particular vendors of mobile devices|
|ACLs|Access Control Lists|Rules that specify which users or system processes are granted access to resources, as well as what operations are allowed on given resources |
|SFTP|Secure File Transfer Protocol |SFTP operates over the SSH protoco|
|UBA|User Behavior Analytics|[What is user behavior analytics (UBA)?](https://www.ibm.com/topics/user-behavior-analytics)|
|PEP|policy enforcement point|[ A system entity that requests and subsequently enforces authorization decisions.](https://csrc.nist.gov/glossary/term/policy_enforcement_point)|
|SAML|Security Assertions Markup Language | |
| | | |
| | | |


### Agentless monitoring
It monitors systems and devices using standard protocols like SNMP, WMI, NetFlow, sFlow, or packet sniffing without requiring agents to be installed on the target systems.

This type of monitoring minimizes the impact on system performance and reduces maintenance overhead, as it does not require the installation and upkeep of agents on individual systems. Agentless monitoring provides sufficient oversight for a smaller environment without the complexity and resource demands associated with agent-based solutions.

- [Agentless monitoring in Windows](https://learn.microsoft.com/en-us/system-center/scom/manage-agentless-monitoring?view=sc-om-2025)
- [Agentless monitoring in PRTG](https://www.paessler.com/remote-monitoring) *PRTG supports Agent & Agent-less*


### Data tokenization
Data tokenization is a process that replaces sensitive data with a token, which is a unique, non-sensitive string of characters.
[How Does Payment Tokenization Work?](https://m2pfintech.com/blog/how-does-payment-tokenization-work/)

### Platform diversity
In the context of **an enterprise with a homogeneous network environment, the most effective strategy** to improve resilience against specific threats targeting their current platform **is to diversify the platforms used across different departments**. \
Platform diversity involves using a variety of operating systems, software, and hardware, which reduces the risk of widespread impact from vulnerabilities or attacks that specifically target a single platform. 

### [What Is Sender Policy Framework (SPF)?](https://www.proofpoint.com/us/threat-reference/spf)
In email cybersecurity, SPF enables the receiving mail server to check whether incoming email comes from a domain authorized by that domain’s administrators.

### Address Space Layout Randomization (ASLR).
Address space layout randomization (ASLR) is a technique that is used to increase the difficulty of performing a buffer overflow attack that requires the attacker to know the location of an executable in memory.
- [Six Facts about Address Space Layout Randomization on Windows](https://cloud.google.com/blog/topics/threat-intelligence/six-facts-about-address-space-layout-randomization-on-windows/)


### [What Is A Transparent Proxy?](https://www.fortinet.com/resources/cyberglossary/transparent-proxy)
Proxy servers essentially act as a middleman between you and the internet.
- **Transparent Proxies** are useful for monitoring, filtering, and caching without requiring user interaction, often used by organizations for network management. 
- **Non-Transparent Proxies** are used for privacy(The proxy hides your real IP addres), security, and bypassing content restrictions, where the user is aware and in control of the proxy configuration.

Proxy uses:

- Firefox: Menu>Settings>Network Settings>Settings>Manual proxy configuration
- Tor Network
- Curl 
```bash
curl -x http://proxy_ip:proxy_port http://example.com
```

- Python Requests / Web Scraping
```python
# SOCKS4: Older version, supports only TCP traffic (works for web browsing, emails, etc.).
# SOCKS5: Newer version, supports both TCP and UDP traffic, allows for more features like authentication and better security options.

import requests

proxies = {
    "http": "socks5://proxy_ip:proxy_port",
    "https": "socks5://proxy_ip:proxy_port"
    "http": "http://proxy_ip:proxy_port",
    "https": "https://proxy_ip:proxy_port",
}

response = requests.get("http://example.com", proxies=proxies)
print(response.text)
```




















