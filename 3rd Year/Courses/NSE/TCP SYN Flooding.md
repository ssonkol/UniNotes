# TCP SYN Flooding
---
## Notes
Transmission Control Protocol (TCP) is a transport layer protocol for many applications, such as HTTP for web, SMTP for email and ftp for file transfer.
- It is one of the main protocols in the Internet protocol suite
- TCP provides reliable end-to-end connection-oriented service to applications, which defines a connection of ordered sequence of segments, over unordered IP network.
- Reliability is provided by segment sequencing, re-transmission and loss detection
- It also provides flow control and congestion control through the sliding window algorithm and loss detection of segments

### TCP connection
A TCP connection is identified by source IP address + port number, and destination IP address + port number. The port number then links to applications running on hosts.

A link is established through three-way handshake

#### TCP Three-way handshake
Fields of the TCP header used in three-way handshake
- Port numbers (16 bits each)
- SYN flag (1 bit)
- ACK flag (1 bit)
- Sequence number (32 bits)
- Acknowledgement number (32 bits)
![[Pasted image 20230203192423.png]]
##### Connection Setup
![[Pasted image 20230203192446.png]]

### TCP SYN Flooding
- An SYN flood attack works by the TCP client not responding to server with the expected ACK packet
- The malicious client can either not send the expected ACK, or more effectively spoof the source IP address in the SYN, causing the server to send the SYN-ACK to a falsified IP address – which will not send an ACK because it knows that it never sent a SYN.
- The server will wait for the missing ACK for a bit. However, the resources bound on the server may eventually exceed the resources available and the server cannot accept any legitimate clients
- This in turn causes Denial of service

#### Spoofing Process
1. Attacker, who is botmaster here, instructs the bots to send high volume of SYN packets to targeted server, often with spoofed IP addresses
2. The server then responds to each one of the SYN packets and leaves an open port ready to receive the response
3. While the server waits for the final ACK packet - which never arrives - the attacker continues to send more SYN packets
	1. The arrival of these new packets causes the server to temporarily maintain a new open port connection for a certain length of time and once all the available resources have been utilised, the server is unable to function normally

---
Backlink: [[Spoofing, Flooding & Sniffing]]
