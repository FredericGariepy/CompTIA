# Chapter 4
# :book: [Questions](https://lognpacific.com/free-certification-practice-tests/free-security-sy0-701-practice-questions/chapter-4-securing-your-network/)
# :bookmark: [Network LESSONS IPsec](https://networklessons.com/cisco/ccie-routing-switching/ipsec-internet-protocol-security)
# :globe_with_meridians: [IEEE_802.1X](https://en.wikipedia.org/wiki/IEEE_802.1X)

___

### 802.11 `b` , `g`, `a`, `ac` , `n` , `ax` , `be`
> 802.11 is a set of standards developed by the IEEE for wireless local area networks (WLANs).
> 
> It defines protocols for implementing wireless communication, including various enhancements for speed, range, and security.

- 802.11b: 2.4 GHz
- 802.11g: 2.4 GHz
- 802.11a: 5 GHz
- 802.11ac: 5 GHz
- 802.11n: 2.4 GHz and 5 GHz
- 802.11ax (Wi-Fi 6): 2.4 GHz and 5 GHz
- 802.11be (Wi-Fi 7): 2.4 GHz, 5 GHz, and 6 GHz

___

NAC (Network Access Control) __agent__ \
is software that enforces security policies on devices trying to access a network.

It checks compliance with security standards (e.g., antivirus, OS updates) before granting access. 

___

Some NAC vendors refer to __dissolvable agents__ _as_ an _"agentless capability"_, \
even though this is somewhat of a misnomer.

- __A dissolvable agent__ : \
1. is downloaded
2. and runs on the client when the client logs on remotely,
3. provides information and status back to the NAC system,
4. then removes itself.

___

__TKIP__ (Temporal Key Integrity Protocol) and \
__CCMP__ (Counter Mode with Cipher Block Chaining Message Authentication Code Protocol) \
are encryption protocols used in Wi-Fi security.

- TKIP: Used in WPA; provides per-packet keying and was designed to replace WEP.
- CCMP: Used in WPA2; based on AES and offers stronger security and performance.

WPA with TKIP is vulnerable to many attacks, while the others are considered stronger or more secure.

___

Wtf is a __'bluebugging’ attack__? \
bluebugging allows the attacker:
- to gain full access to the phone
- also to install a backdoor without the user’s knowledge.

This backdoor provides the attacker the ability to use the phone’s call function, \
enabling them to _listen in on the device’s immediate surroundings or conversations_.

Furthermore, it allows the attacker to _enable call forwarding, send messages, and more._ 

___

### L2TP
__L2TP does not provide any encryption.__ \
Because of this, it cannot be used by itself for VPN traffic.

Instead, data must be encrypted with another protocol, such as IPsec, before being passed to L2TP for transport over the VPN.

## :bookmark: read [L2TPv3 (Layer 2 Tunnel Protocol Version 3)](https://networklessons.com/cisco/ccie-routing-switching-written/l2tpv3-layer-2-tunnel-protocol-version-3) 

___

### Tunnel mode in IPsec
Tunnel mode in IPsec, unlike Transport mode, encrypts both the payload and the packet headers.

This means that the IP addresses used within an internal network are encrypted and hidden from anyone who might intercept the traffic.

Attackers could see the source and destination IP addresses, but they would not be able to see any internal IP address information. \
This is specifically beneficial when data is being transmitted over non-secured networks or public networks such as the internet, where data interception is a risk. 

## :bookmark: Read [IPsec](https://networklessons.com/cisco/ccie-routing-switching/ipsec-internet-protocol-security)

___

Always-on VPN automatically initiates a VPN connection whenever the user’s device connects to the Internet. \
This can be useful for home users or for mobile devices that connect to various Internet connections throughout the day.

___

### RADIUS (Remote Authentication Dial-In User Service) 

Default port for a RADIUS server is 1812.
> This is usually implemented in the context of WPA2’s Enterprise mode,
>  meant to provide authentication for users.

RADIUS (Remote Authentication Dial-In User Service) server in WPA2 is used for:
- centralized authentication,
-  authorization,
-   and accounting of users trying to access a wireless network.

It validates user credentials and controls access based on policies.

___

### PEAP vs. EAP
PEAP (Protected Extensible Authentication Protocol) is a specific implementation of EAP (Extensible Authentication Protocol). 

- EAP: A framework for various authentication methods in networks.
- PEAP: Encapsulates EAP within a secure TLS tunnel, providing an extra layer of security by protecting the inner EAP messages.

___

### EAP-TLS
[802.1X EAP-TLS Authentication Flow Explained ](https://www.securew2.com/blog/802-1x-eap-tls-authentication-flow-explained)


EAP-TLS is different from PEAP and EAP-TTLS in the fact that:
- __EAP-TLS requires certificates on both the 802.1X server as well as the clients__. \
This provides additional security for the communications.

___

The weaknesses of the Password Authentication Protocol (PAP) ---> No Encryption:

___


What is a main benefit of using IPsec’s Tunnel mode over Transport mode?

--> The IP addresses that are used within the internal network are encrypted.

Explanation: This is a benefit of using Tunnel mode because it enhances security by encrypting all information within the network, including the IP addresses. \
This makes the internal IP address information hidden to any potential attackers.

___

### Network-based Intrusion Detection System (NIDS)
- It can __decode encoded traffic__
- It can assess threats on individual systems and workstations
- It can monitor encrypted and non-encrypted network traffic

___

### L2TP (Layer 2 Tunneling Protocol)
L2TP is a VPN protocol that creates a secure tunnel for data transmission over the internet. \
It often works with IPsec for encryption, providing a secure connection for remote access and site-to-site VPNs.

___

### Secure Socket Tunneling Protocol (SSTP)
- __SSTP encrypts VPN traffic using TLS over the port 443__.

It is also a useful alternative when the VPN tunnel must go through a device using NAT, and IPsec is not feasible.

___

##### What are the two primary detection methods used for attack detection in an IDS (Intrusion detection system)? 
- Signature-based and anomaly-based

___

#### What is Bluejacking in the context of Bluetooth device attacks?

<img src="https://cdn.discordapp.com/attachments/1285673198062665728/1289417671812841492/SPOILER_Bluejacking.jpg?ex=66f8bf49&is=66f76dc9&hm=5d8e60276f1acc4ed5477172a9d6fcf66d43c0fc3d99aa2bfb857a401b17b170&" width=420px />

___

| EAP Method | Certificates Required       | Authentication Methods           |
|----------------|--------------------------------|-------------------------------------|
| PEAP       | Server certificate only        | Usernames and passwords             |
| EAP-TTLS   | Server certificate only        | Flexible (e.g., passwords)          |
| EAP-FAST   | No client certificate required  | PAC for authentication               |
| EAP-TLS    | Both client and server required | Client and server certificates       |


- EAP-FAST: No client certificate required; PAC for authentication.
- PEAP: Server certificate only; usernames and passwords.
- EAP-TTLS: Server certificate only; flexible (e.g., passwords).
- EAP-TLS: Both client and server required; client and server certificates.

___


#### WEP Secuity FLAW
It uses a small initialization vector (IV) and reuses keys

____

#### Evil Twin in network security?
An evil twin is a rogue access point that uses the same (or similar) SSID as a legitimate access point to trick users into connecting with it. \
This is done with the malicious intent to steal sensitive data or capture login credentials.

___

PEAP encapsulates and encrypts the EAP conversation in a TLS tunnel to enhance security, providing an extra layer of protection.

___

WPA2 (IEEE 802.11i) uses strong cryptographic protocols such as Advanced Encryption Standard (AES) and Counter-mode/CBC-MAC Protocol (CCMP).

## :bookmark: read [IEEE 802.1X](https://en.wikipedia.org/wiki/IEEE_802.1X)

IEEE 802.1X is an IEEE Standard for port-based network access control (PNAC). \
It is part of the IEEE 802.1 group of networking protocols. \
It provides an authentication mechanism to devices wishing to attach to a LAN or WLAN.

- The standard directly addresses an attack technique called Hardware Addition where an attacker posing as a guest, customer,...

