# Encapsulation Security Payload
---
## Notes
![[Pasted image 20230312124122.png]]

The header specifies encryption and optional authentication. It can be used to provide confidentiality, data origin authentication, connectionless integrity, an anti-replay service, and (limited) traffic flow confidentiality

Its set of services provided depends on the options selected at the time of establishing the SA and on the location of the implementation in a network topology.

### ESP mode
There are two ways in which the IPsec ESP service can be used:
- Transport mode
	- Provides end-to-end encryption between hosts supporting IPsec
	- Uses a transport mode SA
- Tunnel mode
	- Can be used to set up a VPN
	- Uses a tunnel mode SA
	- Corporate networks use ESP tunnel to build VPN

### ESP transport mode
- Encrypts only the data portion of each packet, but leaves the header untouched

If using IPv4:
- ESP header is inserted into IP packet immediately prior to the transport-layer header
- ESP trailer is after IP packet
- If authentication is selected, ESP Authentication Data field is added after ESP trailer
- Entire transport-level segment plus ESP trailer are encrypted
- Authentication covers all of cyphertext plus ESP header

If using IPv6:
- This is viewed as end-to-end payload (i.e. it is not examined or processed by intermediate routers)
- The ESP header appears after IPv6 base header and hop-by-hop, routing, and fragment extension headers
- Destination options extension header could appear before or after ESP header, depending on semantics desired.
- Encryption covers entire transport-level segment plus ESP trailer plus destination options extension headers if it occurs after ESP header
- Authentication covers all of cyphertext plus ESP header

#### Summary
1. At the source, the block of data consisting of ESP trailer plus entire transport-layer segment is encrypted and plaintext of this block is replaced with its cyphertext to form an IP packet for transmission. Authentication is added if this option is selected.
2. Packet is then routed to destination. Each intermediate router needs to examine the process IP header plus any plaintext IP extension headers but doesn't need to examine cyphertext
3. Destination node examines and processes IP header plus any plaintext extension headers. Then, on basis of SPI in ESP header, the destination node decrypts remainder of the packet to recover plaintext transport-layer segment.


- The transport mode operation provides confidentiality for any application that uses it, thus avoiding the need to implement confidentiality in every individual application.
- One drawback to this mode is that it is possible to do traffic analysis on the transmitted packets.

### ESP tunnel mode

Tunnel mode ESP is used to encrypt an entire IP packet
- ESP header is prefixed to a packet
- The packet plus ESP header is encrypted.

#### ESP tunnel mode against traffic analysis
It's not possible to simply transmit encrypted IP packet prefixed by an ESP header because the IP header contains destination addresses and possibly source routing directives and hop-by-hop option information.
- Intermediate routers would be unable to process such a packet

ESP therefore encapsulates the entire block (ESP header plus cyphertext plus Authentication Data, if present) with a new IP header that contains sufficient information for routing but not for traffic analysis

#### ESP tunnel mode benefits
- Tunnel mode ESP is useful in configuration that includes a firewall or other sort of security gateway that protects a trusted network from external networks
- Encryption occurs only between an external host and security gateway or between two security gateways
- This relieves hosts on internal network of processing burden of encryption and simplifies key distribution task by reducing the number of needed keys
- Furthermore, it prevents traffic analysis based on ultimate destination

![[Pasted image 20230312130043.png]]

---
Backlink : [[IP Security]]
