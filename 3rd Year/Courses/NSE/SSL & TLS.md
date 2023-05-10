# SSL & TLS
---
## Notes

The SSL protocol provides communications privacy over the internet. The protocol allows client/server applications to communicate in a way that prevents eavesdropping, tampering, or message forgery ---- RFC 2246

Goals:
- Secrecy, Integrity, (optionally mutual) authentication
	- Works by setting up a one (or two) way authentic channel for secret communication using public-key certificates


The SSL/TLS consists of various sub-protocols which run on top of the TCP
- TLS Handshake: initialised (or reinitialises existing) connections. Establish channel with desired channel properties
- TLS Record: protocol for sending application data. Describes way in which application data is compressed, authenticated with a MAC, and resulting payload is encrypted.
- Other protocols: for renegotiating ciphers and error recovery

![[Pasted image 20230316134642.png]]


### TLS Connection and TLS Session

**TLS Connection**
- A transport that provides a suitable type of service
- For TLS such connections are peer-to-peer relationships
- Connections are transient
- Every connection is associated with one session

**TLS Session**
- A TLS Session is an association between the client and server with an associated state that specifies encryption methods, client and server MAC secrets, encryption keys etc.
- Created by handshake protocol
- Define a set of cryptographic security parameters which can be shared among multiple connections
- Are used to avoid the expensive negotiation of new security parameters for each connection

A TLS connection is basically a secure stream within a session

### TLS Record Protocol
The TLS Record Protocol provides two services for connections:
- **Confidentiality** - The handshake Protocol defines a shared secret key that is used for conventional encryption of TLS payloads
- **Message Integrity** - The Handshake Protocol also defines a shared secret key that is used to form a message authentication code (MAC)
![[Pasted image 20230316135326.png]]

### TLS Handshake Protocol

1. Establish security Capabilities
2. Exchange server certificate
3. Client key exchange. Optional authentication of client using client certificate
4. Finish establishing session

![[Pasted image 20230316135459.png]]


#### Server certificate
![[Pasted image 20230316140045.png]]

Certificate: X.509v3, signed by a trusted 3rd party. Here details other than the name and public key are omitted.

- Actual protocol allows additional key-exchange message needed if negotiating e.g. DH key
- In full protocol, server may also request certificate from client too. Rarely used in practice as it requires clients have personal public key certificates

#### Client Exchange
![[Pasted image 20230316140030.png]]
- PMS is a pre-master secret used to compute a master secret M, which is in turn used to generate various keys.
- M = PRF(PMS, Na, Nb), where PRD is a pseudo-random function, e.g., constructed from a MAC
- The first and third messages authenticate the client. Client sends certificate and hash, computed using all previous messages exchanged

#### An Interpretation
![[Pasted image 20230316140422.png]]
If A shares one-sided key with trusted CA and has a communication channel with B then 1 promotes this to an authentic channel
- In 2, a non authenticated agent A sends keying material to B. Effect of encryption/MAC-ing with this can be understood as follows:
	- When A subsequently sends: we have sender invariant channel
	- When B subsequently responds: channel is receiver invariant
	- Both yield essentially a secure channel with a pseudonym

Secure channel with a pseudonym cannot be promoted to a secure channel, where sender's identity is authenticated. Hence SSL is often followed by additional client authentication.

### TLS for Web Servers

#### User Interface Vulnerabilities

**Example 1: Bad users of SSL in internet**

PKIs (Public Key Infrastructures) are supposed to provide authentication, but they don’t even do that. One company F-Secure sells software from its web site at www.datafellows.com. If you click to buy software, you are redirected to the website www.netsales.net, which makes an SSL connection with you. The SSL certificate was issued to “NetSales, Inc., Software Review LLC” in Kansas. F-Secure is headquartered in Helsinki and San Jose. By any PKI rules, no one should do business with this site. The certificate received is not from the same company that sells the software. This is exactly what a man-in-the-middle attack looks like, and exactly what PKI is supposed to prevent.

**Example 2 : Phishing** 


- Social Engineering + Technological Trickery
	- From account@LaSSale.com
	- Wed Jun 8 20:49:11 2005
	- We are glad to inform you, that our bank has a new security system. The new updated technology will ensure the security of your payments through our bank. As we are doing this for your own safety, we suggest you to test your account validation, this test will maintain the safety of your account. All you have to do is to complete our online secured form. Thank You.
- Users directed to spoofed sites via email-SPAM, DNS hijacking, etc, and tricked into revealing personal data such as credit card number + CVV (credit-card verification value, designed to ensure card possession)


Phishing solutions
- Industry trend is towards multifactor authentication of client. But phishing is a server-side authentication problem! 
- A possible solution: multiple communication channels
	- SSL/TLS combined with 5G telecommunications
	- Server sends user a TAM (temporary authorisation number) by SMS, required for authentication
	- Succeeds as additional transaction key:
		- “transfer $50 to UBS account 23171: confirm with JX3A17” Here attack requires man-in-the-middle on both channels
	- Drawback: requires existing relationship with the server. I.e., client’s mobile phone number is registered with the server


#### Attacks on TLS: Heartbleed

- A catastrophic vulnerability disclosed in the OpenSSL cryptography library (widely used TLS implementation) in April 2014.
	- May be exploited regardless of whether the principal using a vulnerable OpenSSL instance for TLS is a server or a client.
	- Results from improper input validation (due to a missing bounds check) in the implementation of the TLS heartbeat extension (RFC 6520), which provides a way to keep alive secure communication links without the need to renegotiate the connection each time.
	- Vulnerability classified as a buffer over-read, a situation where more data can be read than should be allowed.
- At time of disclosure, some 17% (around half a million) of the Internet’s secure web servers certified by trusted authorities were believed to be vulnerable to the attack, allowing theft of the servers’ private keys and users’ session cookies and passwords.


---
Backlink:[[NSE Outline]]
