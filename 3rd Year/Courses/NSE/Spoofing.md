# Spoofing
---
## Notes

This is the act of pretending to be somebody you are not.

### Layer Identities
#### Internet Layer
At the internet layer, a computer node is identified by its IP address (IPv4/IPv6)
- IPv4 ![[Pasted image 20230202183748.png]]
- IPv6![[Pasted image 20230202183803.png]]
#### Link Layer Identity
At the link layer, a computer node is identified by the MAC address on their NIC (usually designed by device manufacturers)

### Translating between IP & MAC

Since an IP packet needs to be delivered in link layer frames, on local area networks, we need to know both the IP and MAC addresses of a computer node.

This is where we use ARP and RARP to translate between MAC address and IP address.![[Pasted image 20230202184120.png]]
#### ARP (Address Resolution Protocol)

1. System A is looking for the physical address of a certain IP
2. It sends out this request to the local area network.
3. The node which meets the IP address (System B) responds to the call and provides its physical address (MAC)

##### Request Message - Generation
![[Pasted image 20230202190435.png]]

##### Receive Message Generation
![[Pasted image 20230202190517.png]]

##### Reply Message Generation
![[Pasted image 20230202190551.png]]


##### ARP Translation Table
To avoid sending ARP packages every time, a host caches the IP and MAC in its ARIP table with an age to it. These contents are erased if no activity occurs within a given period.


#### RARP (Reverse Address Resolution Protocol)

1. System A sends out a RARP request to all nodes in the LAN providing its MAC address telling all that it wants to find out its IP
2. The RARP sever returns back its IP address


### ARP Cache Poisoning by Spoofing

By constructing spoofed ARP replies and actively joining the ARP protocol run, an attacking system could convince a target computer to send frames destined for computer B to the attacker instead.

This is known as ARP Cache Poisoning.

Steps:
Assume there are two nodes - A & B
A has the IP and MAC of Node B and Node B has the IP and MAC address of Node A
Assume there is a node attacker
1. Attacker learns IP address of Node A & B
2. Construct a spoofed ARP package combining IP address of node B and its own MAC
3. Send this to node A
4. Node A updates its details on Node B, replacing the MAC with the Attacker's MAC
5. Now, packets for Node B sent by Node A will now be sent to the attacker

#### How to make it harder

- Cache entries expire quickly
- Some systems may send out a unicast ARP to confirm update caches
However the attacker can re-send an ARP spoof packet (once every 40s is usually enough to do the trick)

We can beat this again by:
- Creating a static ARP table on a device
	- Load it into RAM every time the OS is loaded
	- This way no ARP request is sent out


#### Man-In-The-Middle Attack with ARP
Do the initial steps for ARP spoofing, now do it to the other system.

This way you can have both parties send information to you. 
You can choose to actively listen by just passing data on, or you can send poisoned replies to either party.


### MAC flooding
This is where a switch is fed many Ethernet frames, each containing different spoofed source MAC addresses.
This in turn will consume the limited memory in the switch, especially old, lower-end switches.

If the CAM table fills up and the switch cannot hold any more entries, some might divert to a fail open state. This forces significant quantities of incoming frames to be flooded out on all ports of the switch/hub. Allowing the attacker to the sniff traffic that might not otherwise be visible.

![[Pasted image 20230202210024.png]]



---
Backlink: [[Spoofing, Flooding & Sniffing]]