# DHCP Starvation & DHCP Spoofing
---

## Notes

### DHCP
Dynamic Host Configuration Protocol is a protocol that automatically provides clients with IP addresses and other related configuration (e.g. default gateway)

Protocol run: DORA between client and DHCP server ![[Pasted image 20230203181419.png]]
- Discovery: Client broadcast message to discover the server
- Offer: Server unicast message offering IP
- Request : Client accepting the IP offered
- Acknowledge: Server acknowledges the IP and sends other related configuration

#### Genuine vs Spoofed

##### Genuine Request Message
DHCP request message contains the source MAC address of the network device requiring an IP address.

##### Spoofed DHCP request message
In a DHCP starvation attack, an attacker broadcasts a large number of DHCP_REQUEST messages with spoofed source MAC addresses

If the legitimate DHCP sever in the network starts responding to all these bogus DHCP_REQUEST messages, available IP addresses in the DHCP server scope will be depleted within a very short span of time

##### DHCP Rogue Server

Once the available number of IP addresses in the DHCP server is depleted (through the spoofed request message), network attackers could set up a bogus DHCP server and respond to new DHCP DISCOVERY messages from the network's DHCP clients.

The rogue server starts handing out IP addresses and other TCP/IP configuration settings including default gateway and DNS server IP addresses, which can now point to an IP address controlled by the attacker.

This also facilitates a man-in-the-middle attack and sniffing attacks.

### Smurfing

A smurfing attack is when a ping is used to cause DoS

Steps:
1. Smurf malware is used to generate a fake echo request, containing a spoofed source IP, which is actually the target server address
2. The request is sent to the intermediate IP broadcast network
3. The request is transmitted to all of the network hosts on the network
4.  Each host sends a ping response to the spoofed source
5. With enough ping responses, the target server is brought down
6. Creating denial of service (DoS)

Amplification: This is when a small amount of traffic is converted into large amounts of traffic, in order to attack the target

### NTP Amplification DDoS Attack

NTP (Network Time Protocol) - Allows computers to synchronise their clocks

-  This is a UDP based protocol using port 123
- Used to keep consistent timekeeping among all clock-dependent devices within a network
- The time of a local system using NTP can be synchronised to other reference sources and used as a reference source to synchronise other clocks
- NTP uses hierarchical, semi-layered system of time sources

#### NTP Clock Strata

Each level of the heirarchy is called a Stratum and is assigned to a number of starting with 0 for the reference clock at the top

A server synchronised to a stratum n server runs at stratum n+1![[Pasted image 20230203183713.png]]
#### How does it work?
1. Client sends the server an NTP message, which is timestamped when it leaves the client (T1 = 9am)
2. The NTP message arrives at the server and is timestamped too (T2 = 10:00:01AM)
3. When the NTP message leaves the server, the server timestamps it (T3 = 10:00:02AM)
4. The NTP message arrives back at the client with the local time timestamped( T4 = 09:00:03AM)
5. The client calculates the roundtrip delay
	1. D1 = T4-T1 = 3 seconds = Total roundtrip delay
	2. D2 = T3-T2 = 1 second = Processing time at server end
	3. Roundtrip delay of NTP message on network = D1-D2 = 2 seconds
6. The client Calculates the time difference between the NTP client and the NTP server
	1. 01 = T2-T1 =  1hr 1 sec
	2. 02 = T3-T4 = 59 min 59 sec]Offset = (01+02)/2 = 1 hour
7. Based on this, the NTP client can synchronise its own clock to that of the server

#### NTP amplification attack
- We can rely on the use of publicly accessible NTP servers to overwhelm a victim system with UDP traffic
- The NTP service supports a monitoring service that allows administrators to query the server for traffic counts on connected clients. This information is provided by the 'monlist' cmd - which returns a list of recent hosts that have connected to the service

##### Attack strategy
Use amplification between NTP request and NTP response
- Spoof the IP address to be the victim in an NTP request message
- Send the NTP request message to vulnerable NTP servers, which we ask the server to run monlist cmd and respond
- The monlist cmd causes a list of the last 600 IP addresses which connected to the NTP server to be sent to the victim

##### Attack Process
1. Attacker uses botnet to prepare NTP request packets with spoofed addresses to NTP servers, which have their monlist cmd enabled. The spoofed IP address is the victim's IP address
2. The botnet sends the NTP request to NTP servers using its monlist cmd, resulting in a large response
3. The server responds to the spoofed address with the resulting data, normally of much larger size than the original NTP request (since monlist cmd returns 600 hosts' IP addresses)
4. The victim receives the response and the surrounding network infrastructure becomes overwhelmed with the amplification of traffic, resulting in DoS attack.

##### Amplification Factor
NTP request = 234 bytes
Monlist returns 600 IP addresses that need to be sent in about 100 packets as a response 
- Note that Wireshark shows only 10 packets each of 482 bytes long
NTP response total = 100 * 482 = 48200 bytes
Amplification factor = 48200 / 234 = 206 (approx.)

---
Backlink: [[Spoofing, Flooding & Sniffing]]
