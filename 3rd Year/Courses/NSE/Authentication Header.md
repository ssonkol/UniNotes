# Authentication Header
---
## Notes

### Authentication Header (AH) ![[Pasted image 20230312122734.png]]
This is an extra header between layers 3 & 4 (IP and TCP) that provides destination enough information to identify SA

AH guarantees integrity only.

- The sequence number is initialised to 1 and incremented by sender for each packet.
- The receiver stored incoming packets in a sliding window (default size 64) to order and sort out duplicates

### Anti-replay service
A replay attack is one which an attacker obtains a copy of an authenticated packet and later transmits it to the intended destination.

The receipt of duplicate, authenticated IP packets may disrupt service in some way or may have some other undesired consequence.

#### Example
Assume a new security association is established

Sender:
1. Set sequence number counter to 0
2. Each time a packet is sent, increase the counter by 1, and place the value in the sequence number field
3. If the counter reaches 2^32-1, terminate this SA, and negotiate a new SA with a new key

Receiver:
![[Pasted image 20230312123757.png]]
1. If the received packet sequence number fails within the window and is new, the MAC is checked for integrity. If the packet is authenticated, the corresponding slot is marked.
2. If the received packet sequence number is to the right of the window (=N+1) and is new, the MAC is checked. If the packet is authenticated, the corresponding slot is marked and the window advances by 1 slot (move to the right)
3. If the received packet sequence number is to the left of the window or if the authentication fails, the packet is discarded; this is an auditable event

### AH modes
- Original Datagram![[Pasted image 20230312124035.png]]


- Transport Mode:
	- AH inserted after IP header, before IP payload
	- MAC (Message Authentication Code) is taken of entire packet
	- Provides end-to-end protection between IPsec-enabled systems![[Pasted image 20230312124046.png]]

- Tunnel Mode:
	- Entire original packet authenticated, new outer IP header
	- Inner headers carries ultimate source/destination address
	- New outer header is also protected and may contain different IP addresses, e.g. firewalls or security gateways![[Pasted image 20230312124059.png]]







---
Backlink : [[IP Security]]
