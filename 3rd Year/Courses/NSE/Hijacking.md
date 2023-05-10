# Hijacking
---
## Notes

This is the idea of taking over what belongs to someone else, especially during run-time.

We can use Hijacking to:
- Disrupt or jam communications
- Insert False or Malicious data

Whilst this may be similar to spoofing, the difference is that jacking takes over an existing connection whereas spoofing initiates a new connection to cheat.

##### Off-path vs On-path adversaries

On-Path adversary is a type of adversary in the context of computer networking, who has the ability to monitor or manipulate data packets that pass through the network path it is on.

- On-Path adversaries are more powerful as they have the ability to corrupt transmitted data
- They can also use the connection state, however it is difficult to scale up


An off-path adversary, on the other hand, is one who is not on the same network path as the communication being monitored or manipulated, but still has the ability to gain access to the information being transmitted.
- It is very difficult to insert false data with an off-path 

### TCP Hijacking

TCP hijacking is a type of cyber attack that allows an attacker to take control of an established TCP connection by intercepting and modifying the packets transmitted between the communicating parties. This can be achieved by several techniques, including IP spoofing, ARP spoofing, and session fixation.

1.  The client (C) and the server (S) initiate a TCP connection.
    
2.  The attacker (A) intercepts the communication between C and S by placing themselves between them on the network.
    
3.  A analyses the sequence and acknowledgment numbers being used in the TCP communication between C and S.
    
4.  A sends a spoofed packet to S with a false source IP address, pretending to be C, and with a specially crafted sequence and acknowledgment number.
    
5.  S accepts the spoofed packet and sends its own response, which A intercepts and modifies.
    
6.  A now has control of the TCP connection between C and S, and can intercept and modify any packets transmitted between them. For example, A can inject malicious payloads into the communication, or simply eavesdrop on the communication to steal sensitive information.

It's important to note that TCP hijacking can be prevented through the use of secure protocols such as SSL/TLS and the implementation of strong network security measures such as firewalls, intrusion detection systems, and anti-spoofing measures.

#### In-depth
The attacker needs to construct a valid TCP segment acceptable by the client/server
The attacker must get these fields correct:
- Source IP address + port number (easy)
- Destination IP address + port number (easy)
- Sequence Number (not very difficult if the attacker is on-path)

1. Sniff packets
2. Predict Sequence number (client -> server / server -> client)
3. Inject data spoofing as client

##### Predict TCP sequence number on-path

When the attacker is intercepting a message between the Client and the server.
When the data is being poisoned. the attacker may manage to put the sequence number as x+1 (which is the sequence number that the server is expecting) then poisoned data can be added behind/next to the data that has already arrived.

- It is also okay if the attacker adds an x+d when the injected data is placed in the receiver's buffer if delta is within the boundary of the receivers TCP buffer

- We can do this to spoof as a client or as a server.

##### What can the Attacker do if they are off-path
- Blindly spoof as the client, and send an SYN packet to the server as if it was from the client
- The attacker must get the sequence number correct

1. Attacker sends IP and SYN with the sequence x
2. The server returns the sequence number y with the acknowledge number x+1
3. The SYN packet arrives at the real client and not the attacker
	1. When the client receives this, they may send RST to the server to terminate the connection
4. To prevent this the attacker quickly sends back an acknowledgement number y+1 and a sequence number x+1 with the data 
	1. The attacker doesn't know y so they must guess it


##### How they guess the number
The attacker exploits a vulnerability that there is a mismatch between the specification and implementation.

"When new connections are created, an initial sequence number (ISN) generator is employed which selects a new 32 bit ISN. The generator is bound to a 32 bit clock whose low order bit is incremented roughly every 4 microseconds"
- Thus the ISN cycles approximately every 4.55 hours

However the Unix TCP/IP stack does not adhere to this.
- The sequence number stacks increases by 128,000 every seconds and 64000 for every new TCP connection.
- Therefore it is relatively easy to predict and can be much more readily exploited than one which follows the RFC standard

1. Attacker uses ICMP flooding on client, making them unable to respond to any messages received
2. The attacker sends a genuine SYN package with the IP of the attacker and the sequence number x
3. The server sends back an acknowledgement number x+1 and sequence number y
	1. This number y will be what the attacker uses to predict the value y' the server will send in communication with the client
4. The attacker sends a RST (reset) package to end the connection
5. The attacker now sends a spoofed package with the clients IP and the sequence number x'
6. The server responds to the client with a sequence number y+N and acknowledgement number x'+1
	1. The packet arrives and is ignored as it is currently under a flooding attack which the attacker can use
7. The attacker now sends a spoofed acknowledgment number Y+N+1 and sequence number x'+1 with the poisoned data
8. Spoofed connection is established and the session is now hijacked

##### Example

1. Swamp the Client C with ICMP flooding, taking it out of the picture (because the attacker wants to spoof as C)
2. Create a real connection to port 80 on the web Server, and record the sequence number returned by the web Server.
3. Close the connection with the Server.
4. Create a raw IP socket, change its protocol to that of TCP, and change its source IP to that of the Client (by writing in the kernel)
5. Send a SYN packet (supposedly from the Client) to port 80 on the web server. 
6. The server then sends an SYN+ACK to the Client C, which is silently ignored because C is under ICMP flooding attack
7. Send an ACK packet to the server with the acknowledgement number equal to the sequence number previously recorded plus N+1

- After connection is established and hijacked
	- Send data to the Server, taking care to increment the sequence number each time by the amount of data sent. The Server thought the data comes from the Client.


### BGP Route Hijacking attack

#### Border Gateway Protocol
Border Gateway Protocol (BGP) is a protocol used for routing traffic on the Internet. It helps to determine the best path for data to travel from one network to another.

BGP is used by Internet Service Providers (ISPs) to exchange information about the reachability and status of IP addresses and networks. This information is used to build a routing table, which is a database of information that tells routers which path to take to reach a specific network.

In simple terms, BGP is like a map for the Internet, helping data to find its way from one place to another. By exchanging information about network reachability and status, BGP helps to ensure that data is routed efficiently and reliably across the Internet.

#### Autonomous system
This is the Unit of router policy, either a single network or a group of networks that is controlled by  a common network administrator on behalf of a single administrative entity (such as a university, a business enterprise or a business division)

##### Intra-AS routing
This is routing within the AS.
This is for destinations that are within the same AS;
- RIP, OSPF
- Routing Tables

##### Inter-AS routing and CIDR prefix
Also known as inter-domain routing, this is where all AS' run the same inter-AS routing protocol (BGP).

In BGP, packets aren't routed to a specific destination IP address, but to Classless Inter-Domain Routing (CIDR) prefixes, with each prefix representing a subnet or a collection of subnets.

CIDR is classless as any number of bits can be used for the network part of a packet.

###### CIDR prefix
 The CIDR prefix is the number of 1 bits in the subnet marks
 For example:![[Pasted image 20230209124501.png]]
 - 172.16.122.204, the network part is 16 bits, and host part is also 16 bits 
 - The subnet mask is composed of 16 ones followed by 16 zeros, 255.255.0.0
 - Hence the CIDR prefix = 16
 - The subnet can be expressed as 172.16.0.0/16 in CIDR prefix notation
 
The CIDR prefix is used in the routing table for BGP
Each entry is in the form of (x, I):
- x is a CIDR prefix
- I is an interface number for one of the router's interface

##### BGP functionalities
It can:
- Obtain network prefix reachability information from neighbouring AS'
	- BGP allows each subnet to advertise its existence to the rest of the internet
	- BGP makes sure that all the routers in the internet know about that subnet
- Determine the best routes to the network prefixes based on
	- Policy
	- Prefix reachability information
- AS' perform longest prefix matching to select which neighbours to route through
	- For example:
		- When the address 192.168.20.19 needs to be looked up in a router having two entries in its routing table![[Pasted image 20230209125325.png]]
		- Both entries contain the looked up address, the longest prefix of the candidate routes 192.168.20.16/28, making the route more specific, therefore it is chosen


#### BGP Route Advertisement 
###### Propagation
If AS22394 wants to advertise to AS7018 then it first send out its (ID, CIDR prefix)
![[Pasted image 20230209130004.png]]

1. AS22394: (22394, 66.174.161.0/24)
2. Because AS6167 is in-between them it must then relay this by adding on its ID to the front of the message : (6167, 22394, 66.174.161.0/24)
3. AS3356 adds on its ID: (3356, 6167, 22394, 66.174.161.0/24) 
4. AS7018 adds on its ID : (7018, 3356, 6167, 22394, 66.174.161.0/24)

- Each AS advertises 66.174.161.0/24 and gives the sequence of other ASs that lead to the advertised subnet

###### How is BGP route advertisement carried out?
- Routers exchange routing information over TCP connections using port 179
- eBGP, external BGP (TCP) connection spans two ASs
- iBGP, internal BGP (TCP) connection between routers in the same AS
![[Pasted image 20230209130052.png]]

#### BGP prefix Hijacking 
- When an AS announces a route to network prefixes that it doesn't actually control
- False information is added to routing tables in BGP routers across the internet

![[Pasted image 20230209130253.png]]

1. The attacker lies about a subset of the prefix rather than the whole prefix belonging to another AS
2. The false route is chosen because BGP prefers longest prefix matching

#### How to Create a Routing Blackhole
AS' advertises routes it cannot actually offer
- This results in packets going into a network blackhole


---
Backlink: [[Hijacking & Poisoning]]
