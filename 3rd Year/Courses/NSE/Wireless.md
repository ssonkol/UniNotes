# Wireless
---
### Wireless & Mobile Networks

#### Wireless Networks with Infrastructure
For infrastructure, they need an access point (AP), a router for wireless LAN/WIFI and a base station for telecommunications.

Mobile Ad hoc networks (MANETs)

MANET - An autonomous system of mobile nodes which are free to move about arbitrarily.

The devices cooperate for building up a network, nodes enter and leave the network.

Applications:
- Military use
- Emergency operation
- Wireless sensor networks

Efficiency is severely restricted 
- Nodes with very different capabilities
- Limitations in power consumption
	- Lack of centralised PKI 
	- Lightweight cryptography

#### Heterogeneous Networks
This is a hybrid solution.
It can reduce deployment costs.
- Cellular aided mobile ad hoc networks
	- Ad hoc networks within classical cellular networks
	- Security and routing can be left for the cellular network.

![[Pasted image 20230508123358.png]]

### Wireless Security


**Risk Factors**:
- Higher security risk of wireless networks compared to wired networks.
- Key factors: Channel, mobility, resources, accessibility

Channel:
- Wireless networking typically involves broadcast communication, which is far more susceptible to eavesdropping and jamming than wired network
- Wireless networks are also more vulnerable to activate attacks that exploit vulnerabilities in communications protocols

Mobility:
- Wireless devices are far more portable and mobile than wired devices

Resources:
- Some wireless devices, such as smartphones and tablets, have sophisticated operating systems but limited memory and processing resources with which to counter threats, including DoS and malwares.

Accessibility:
- Some wireless devices, such as sensors and robots, may be left unattended in remote and/ or hostile locations
- This greatly increases their vulnerability to physical attacks

The components provide points of attacks -
- End point - mobile phone, tablet, sensors, laptops
- Access point - WI-FI hotspots, cellular tower, wireless access point
- Wireless media - Carries the radio waves for transfer

#### Wireless Network Threats
Accidental association:
- Company wireless LANs in close proximity may create overlapping transmission ranges
- A user intending to connect to one LAN may unintentionally log on to a wireless access point from a neighbouring network

Malicious Association:
- In this situation, a wireless device is configured to appear to be a legitimate access point, enabling the operator to steal passwords from legitimate users and then penetrate a wired network through a legitimate wireless access point

Ad hoc networks:
- These are peer-to-peer networks between wireless computers with no access between them
- Such networks can pose a security threat due to a lack of a central point of control

Identity Theft (MAC Spoofing):
- This occurs when an attacker is able to eavesdrop on network traffic and identify the MAC address of a computer with network privileges

Man-in-the-middle attacks:
- This attack involves persuading a user and an access point to believe that they are talking to each other, when in fact the communication is going through an intermediate attacking device
- Wireless networks are particularly vulnerable to such attacks

Denial of Service (DoS):
- This attack occurs when an attacker continually bombards a wireless access point or some other accessible wireless port with various protocol messages designed to consume system resources
- The wireless environment lends itself to this type of attack because it is so easy for the attacker to direct multiple wireless messages at the target

Network injection:
- This attack targets wireless access points that are exposed to nonfiltered network traffic, such as routing protocol messages

#### Securing Wireless Transmissions

The principal threats to wireless transmissions are eavesdropping, altering or inserting messages, and disruption.

To deal with eavesdropping, two types of countermeasures are appropriate:
- Signal-hiding techniques
	- Turn off SSID broadcasting by wireless access points
	- Assign cryptic names to SSIDs
	- Reduce signal strength to the lowest level that still provides requisite coverage
	- Locate wireless access points in the interior of the building, away from windows and exterior walls
- Encryption
	- Is effective against eavesdropping to the extent that the encryption keys are secured

To deal with message alteration:
- Encryption and authentication

#### Securing Wireless access points
The main threat involving wireless access points is unauthorised access to the network

The principal approach for preventing such access is the IEEE 802.1X standard for port-based network access control
- The standard provides an authentication mechanism for devices wishing to attach to a LAN or wireless network
- The use of 802.1X can prevent rogue access points and other unauthorized devices from becoming insecure backdoors

**How to Secure**:
- Use encryption
- Use antivirus, antispyware software and a firewall
- Turn off identifier broadcasting
- Change the identifier on your router from the default
- Change your router's pre-set password for administration
- Allow only specific computers to access your wireless network

### Mobile Device Security
Mobile devices have become an essential element for organisations as part of the overall network infrastructure

Prior to the widespread use of smartphones, network security was based upon clearly defined perimeters that separated trusted internal networks from the untrusted internet.

Due to massive changes, an organisation's networks must now accommodate:
- Growing use of new devices
- Cloud-based applications
- De-perimeterisation
- External business requirements

**Security Concerns for mobile devices**
- Lack of physical security controls
- Use of untrusted mobile devices
- Use of untrusted networks
- Use of untrusted content
- Use of applications created by unknown parties
- Interaction with other systems
- Use of location services


