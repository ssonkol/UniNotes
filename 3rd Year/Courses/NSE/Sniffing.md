---
quickshare-date: 2023-05-10 18:42:55
quickshare-url: "https://noteshare.space/note/clhhznyng411201pjpaq3urmq#8pxriuBecUy58NdL9LQEPKXXUnJs+H6tEm5zfjxm8is"
---
# Sniffing
---
## Notes

This is the idea of listening to network conversations that are not intended for you.
- The Network interface card (NIC) can be set to promiscuous mode to get all packets from the network.
- Packet sniffers intercept and log network traffic that they can see via the NIC

### Physical Interception

The physical layer consists of:
- Wires
- Air transmission
- Fiber
- Hub
- Switch
- Router

Now sniffing information in transit in the physical layer depends on:
- Whether we are in a network or not
- The attack is passive or active

### Passive interception (Promiscuous Mode)

An NIC has two working modes:
- Non-promiscuous mode - This mode drops unintended traffic
- Promiscuous mode - This mode gets all packets from a network

This works for Hubs and WIFI networks but doesn't work for networks using switches as a switch has a separated broadcasting domain.

### Active Interception 
#### Port Mirroring

- Also known as SPAN (Switch Port Analyser), port mirroring works by the switch sending a copy of network packets seen on one port to the SPAN ports.
- The SPAN port mirrors all traffic through the switch.



Good intentions include:
- Network Diagnostics
- Intrusion Detection

Malicious Behaviour includes:
- Attacker plugs into port to see all traffic

#### Network Tapping

This is where a hardware device is inserted at a specific point in a network where data can be accessed for testing or troubleshooting purposes

This would be a layer 1 device![[Pasted image 20230125212404.png]]
##### Pin Connection
- Pins 3 and 6 of Tap A are connected to pins 1 and 2 of Host A and Host B
- Pins 3 and 6 of Tap B are connected to pins 3 and 6 of Host A and Host B

This causes brief disruption as the cable needs to be separated.
![[Pasted image 20230125212601.png]]

##### Traffic Flow
![[Pasted image 20230125212737.png]]


#### Bypass TAPs

This is put inline on the critical links
- Every packet being sent from the network will get to the monitoring tool
- It can also work in the Bypass mode to bypass the monitor appliance and keep the critical link running

![[Pasted image 20230125213241.png]]

#### Vampire Taps
- This is where you pierce the shielding copper wires in order to provide access to the signal within
- This may bring down the link

### Rogue Access Point
This is a wireless access point that has been installed on a network without explicit authorisation from a local network admin

Types:
- Hardware:  A wireless router
- Software: A computer/laptop with a virtual one

They are usually open and try to mimic a known WIFI network ID (e.g. Eduroam)
Victims connect unaware that they're connecting to the rogue AP![[Pasted image 20230125213627.png]]




---
Backlink: [[TCP&IP]]