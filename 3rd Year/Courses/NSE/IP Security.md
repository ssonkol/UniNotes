# IP Security
---
## Outline
- [[IP Security Policy]]
- [[Authentication Header]]
- [[Encapsulation Security Payload]]
- [[Internet Key Exchange(IKE)]]

## Notes
This is a capability that can be added to either current version of the internet Protocol (IPv4/IPv6) by means of additional headers.

By implementing security at the IP level, an organisation can ensure secure networking not only for application that have security mechanisms (e.g. secure email, Kerberos, Security Socket Layers (SSL)). But also for security-ignorant applications.

Essentially packet filtering based on a policy database - like a firewall between two ends.

IPsec includes three functional areas:
- **Authentication** - Assuring that the packet was transmitted by the party identified as the source in the packet header, and that packet has not been altered in transit
- **Confidentiality** - Enables communicating nodes to encrypt messages to prevent eavesdropping by third parties
- **Key Management** - Concerned with the secure exchange of keys

It can be installed on:
- Operating Systems
- Security Gateways - Firewalls or routers

### Applications of IPsec
- Secure branch office connectivity over the internet
- Secure remote access over the internet
- Establishing extranet and intranet connectivity with partners
- Enhancing e-commerce security

The main feature of IPsec is that it enables it to support these varied applications is that t can encrypt and/or authenticate all traffic at the IP level - thus all distributed applications can be secured.

### Benefits of IPsec
- IPsec provides strong security that can be applied to all traffic crossing the perimeter
- IPsec in a firewall is resistant to bypass if all traffic from outside must use IPsec and the firewall is the only entrance from the internet into the organisation
- IPsec is below transport layer (TCP, UDP) and so is transparent to applications
- IPsec can be transparent to end users
- IPsec can provide security for all individual users if needed


### IPsec standard
IPsec is an IETF standard, complex specification covering protocols for a variety of purposes:
- Authentication Header (AH) - Protects the integrity and the authenticity of IP datagrams (but not their confidentiality!!)
- Encapsulating Security Payload (ESP) - Protects confidentiality and optionally also integrity
- Internet Key Exchange Protocol (IKE) - Provided key management


---
Backlink: [[NSE Outline]]
