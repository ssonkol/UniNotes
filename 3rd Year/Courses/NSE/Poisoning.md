# Poisoning
---
## Notes

### DNS
Known as Domain Name system, this is a distributed databased implemented in a hierarchy of DNS servers. An application-layer protocol that allows hosts to query the distributed database.

DNS is essentially a directory service that translates hostnames to IP addresses![[Pasted image 20230209131849.png]]We need to cache DNS queries so that second and sequent lookups are cheap and easy

- DNS has a hierarchical tree like structure ![[Pasted image 20230209131700.png]]
#### DNS Query

##### Iterative 
![[Pasted image 20230209131945.png]]
![[Pasted image 20230209132106.png]]
###### With Caching
1. Request host sends out request for IP
2. Local DNS checks cache, if information is there, it sends it back otherwise it sends a request to root DNS server
	1. Sends request to Top Level DNS server
	2. Sends request to Authoritative DNS server
3. Authoritative DNS server sends it back to Local DNS
4. Local DNS responds to request host and stores mapping in cache
##### Recursive
![[Pasted image 20230209132002.png]]
- Unfortunately this method does not scale hence it is not used in practice

### DNS Cache Poisoning attack
1. Usual process happens
2. Whilst the Local server is sending out the query, the attacker sends a poisoned IP to the Local DNS so it has a wrong mapping
3. Local DNS remembers this and stores it in cache
4. Now whenever a request is made to the Local DNS server about the site, they are sent the poisoned IP information
5. Them the requesting hosts are sent to the attackers chosen IP address

#### Query QID Attack
- Every DNS query has a QID
- The DNS uses connectionless UDP
- If the attacker responds to the query with the right QID, then it winds over the real nameserver's response
![[Pasted image 20230209133038.png]]


1. Use dig, a DNS lookup utility to collect information about the QID

#### RRSet Attack

- DNS response contains different Resource Record Sets, or RRSets
- An, additional section, where the name server can give additional information that may be useful for future lookups 

![[Pasted image 20230209133208.png]]

- In an iterative query, the .com nameserver says you can ask ns.example.com for the IP address of example.com. To help next request, an additional record might give IP for ns.example.com.
- Darth abuses this feature and adds an additional record that says the IP address of victim.com is 88.88.88.88
- FIX: Bailiwick checking (when asking for www.google.com, do not allow www.victim.com to be accepted as an additional record)

---
Backlink: [[Hijacking & Poisoning]]
