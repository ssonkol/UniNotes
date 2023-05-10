# TCP_IP Architecture
---

## Notes


### TCP/IP Protocol Architecture
The architecture is broken down into:
1. Application - This provides access to the environment for users and distributed information services
	1. Email, File transfer, remote access, HTTP, DNS
2. Transport - This transfers data between end points. It may provide error control, flow control, congestion control
	1. TCP, UDP
3. Internet
	1. Shield layers from details of physical network configuration, providing routing and forwarding
4. Network Access - This is the logical interface to network hardware, with medium access control.
	1. Ethernet, WIFI, IoT
5. Physical - Transmission of bit streams
	1. Twisted pair, optical fibre, satellite, radio

![[Pasted image 20230125202134.png]]

### Sending to Network (Encapsulation)
![[Pasted image 20230125202315.png]]

### Receiving from Network (Decapsulation)
![[Pasted image 20230125202329.png]]

### Routing and Sending to Network again
![[Pasted image 20230125202420.png]]

### Receiving the destination (Decapsulation)
![[Pasted image 20230125202456.png]]


---
Backlink: [[TCP&IP]]
