# IP Security Policy
---
## Notes
The security policy is applied to each IP packet that transits from a source to a destination

the policy is determined primarily by the interaction of two databases:
- The security association database (SAD)
- The security policy database (SPD)
![[Pasted image 20230312113359.png]]

### SAD

A security association (SA) is a one-way relationship between sender and receiver defining security services

SA specifies things like:
- Authentication Algorithm (AH)
- Encryption Algorithm (ESP)
- Keys
- Key lifetimes
- Lifetime of security association
- Protocol mode (tunnel or transport)

SA is uniquely identified by three parameters - 
- Security Parameters Index (SPI) - A bit string assigned to this SA and having local significance only. SPI is carried in AH and ESP headers to enable the receiving system to select SA under which a received packet will be processed
- IP destination address - Address of destination endpoint of SA
- Security Protocol Identifier - A field from the outer IP header that indicates whether the SA is an AH or ESP SA

### SPD
This provides a means by which IP traffic is related to specific SAs

In its simplest form, an SPD contains entries, each of which defines a subset of IP traffic and points to an SA for that traffic.

In more complex environments, there may be multiple entries that potentially relate to a single SA or multiple SAs associated with a single SPD entry
- Each SPD entry is defined by a set of IP and upper layer protocol field values called selectors
- These are used to filter outgoing traffic in order to map it into a particular SA

### IP Traffic Processing
IPsec is executed on a packet-by-packet basis

When IPsec is implemented:
- Each outbound IP packet is processed by the IPsec logic before transmission
- Each outbound packet is processed by the IPsec logic after reception and before passing the packet contents on to the next higher layer (TCP or UDP)
![[Pasted image 20230312121851.png]]

#### Outbound
- IPsec searches SPD for a match to this packet
- If no match is found, the packet is discarded and an error message is generated
- If a match is found, further processing is determined by the first matching entry in the SPD, which can be:
	-  DISCARD - The packet will be discarded
	-  BYPASS - There is no further IPsec processing
	-  PROTECT - The SAD is searched for a matching entry
- If no entry is found in the SAD, IKE  is invoked to create an SA with the appropriate keys and an entry is made in the SAD
- If an entry is found in the SAD, that entry determines processing for this packet
	- Either encryption, authentication or both can be performed, and either transport or tunnel mode can be used
	- The packet is then forwarded to the network for transmission.

**Packet Type Check**
- IPsec determines whether this is an unsecured IP packet or one that has ESP or AH headers/trailers, by examining the IP protocol field (IPv4) or Next Header field (IPv6)


- If the packet is secured, IPsec searches the SAD for a match to this packet
- If no match is found in the SAD, then the packet is discarded
- Otherwise IPsec applies appropriate ESP or AH processing, and then IP header is processed and removed and the packet payload is delivered to the next higher layer, such as TCP


---
Backlink : [[IP Security]]