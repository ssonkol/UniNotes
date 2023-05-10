# Traffic Analysis
---
## Notes

### Data Acquisition
This is the process of understanding the meaning of captured traffic after sniffing

sniffing tools include:
- Tcpdump
- Wireshark
- Snort
- Bro

#### Libpcap

Libpcap is an API for capturing live network traffic
It actually captures frames which include all data from the data link layer to the application layer, due to encapsulation

- Network sniffers/analysers capture network traffic and save them in a pcap file
- They are then able to open these pcap files created by other tools

#### BPF - Berkley Packet Filter

- A kernel agent that discards unwanted packets as early as possible
- Two components:
	- Network tap
	- Packet filter
- BPF feeds the packet to each participating process' filter.
	- This user-defined filter decides whether a packet is to be accepted and how many bytes of each packet should be saved
- For each filter that accepts the packet, BPF copies the requested amount of data to the builder associated with that filter


![[Pasted image 20230126132805.png]]


##### How sniffers use libpcap
![[Pasted image 20230126134633.png]]

#### Tcpdump

This is a powerful packet analyser running in cmd 
- We use the command tcpdump -list-interfaces to see which interfaces are available for capture

![[Pasted image 20230126134812.png]]

#### Wireshark
This is a packet analyser with a GUI

### Traffic Analysis

The 3 different types of traffic analysis include:
- Protocol Analysis - Analyse individual protocol inside a packet
- Packet Analysis - Analyse protocols of different layers inside a set of packets
- Flow Analysis - Analyse a flow composed of multiple packets

#### Protocol Analysis
We use protocol analysis to:
- Understand the semantics of the information being transferred
- Interpret the information

#### Packet Analysis
We do packet analysis to:
- Inspect the protocols within a set of packets transmitted
- Identify packets of interest using packet analysis techniques

- If you're a network professional
	- We can use it to monitor the health of a network
- If you're a security professional
	- We can use it for passive network vulnerability assessment
- If you're an attacker
	- We can use it as a passive attack tool
	- Or to steal information such as passwords


##### Frames
Frames are a processing data unit within the link layer.

An internet layer packet is a payload of frames![[Pasted image 20230126140521.png]]
#### Packet Analysis Techniques

- Pattern Matching
	- Used to identify packets of interest by matching specific values in the packet capture
- Parsing protocol fields
	- Extract the contents of a particular protocol field
	- E.g. Wireshark shows the contents of each field in an IP packet
- Packet filtering
	- Separate packets based on the values of fields in protocol metadata
	- Showing ICMP packets only



### Flow Analysis

Flow analysis is the practice of examining related groups of packets

We need flow analysis to:
- Identify patterns
- Isolate suspicious activity and discard irrelevant data
- Analyse higher-layer protocols 
- Extract data

#### Flow Analysis Techniques

- List conversations and flows
	- List all conversations and/or flows within a packet capture or only specific flows based on their characteristics
- Export a flow
	- Isolate a flow or multiple flows, and store the flow(s) of interest to a disk for further analysis
- File and data carving
	- Extract files or other data of interest from the reassembled flow


---
Backlink: [[TCP&IP]]
