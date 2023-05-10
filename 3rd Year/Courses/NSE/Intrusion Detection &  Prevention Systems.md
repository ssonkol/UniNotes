# Intrusion Detection &  Prevention Systems
---
## Notes

An Intrusion detection system is used to detect and report intrusion attempts to the network. Think of this as the security camera after the gate. It alerts any intrusion attempts to the security administrator.

IDS sits behind the firewall. Since firewalls block intruders from the outside, IDS capture intruders who are insiders.

##### Types of Intruders
- Masquerade
	- This is an individual who is not authorised to use the computer and manages to penetrate the system's access controls to exploit a legitimate user's account
- Misfeasor
	- This is a legitimate user who has access to data, programs or resources for which such access is not authorised, or who is authorised for such access but misuses their privileges
- Clandestine User
	- This is an individual who seizes supervisory control of the system and uses this control to evade auditing and access controls or to suppress audit collection


### Intrusion Prevention System
This is an IDS with an automated response:
- Shut down attacker connections
- Try to back-trace the attacker
- Counter attack

This is because an intrusion prevention system will eventually fail, which is why the second line of defence is intrusion detection.

An effective IDS can also act as a deterrent. Furthermore, acting as a collection of information about intrusion techniques that can be used to strengthen the intrusion prevention facility,

### How to detect an intruder
We get this from the behaviours an intruder may show, and the behaviours an authorised user may show.

#### Reputation Detection
Detect the hosts communication with someone of bad reputation. This is based on public or private blacklists.
- Malware domain list
- Spamhaus Block lists
- PhishTank


#### Anomaly Based Detection
This is a detection system where a normal system behaviour is defined first. This is then checked against the later if an anomaly in behaviour is detected.

When normal system is defined, it involves the collection of data relating to the behaviour of legit users over a period of time.

- Statistical checks are made to observed behaviour to determine is that behaviour is legit or not.
- This is based on threshold detection (define thresholds independent of  the user, for the frequency and occurrence of various events) or profile based detection (a profile of the activity each user is developed and used to detect changes in the behaviour of individual accounts.

##### Types of Statistical Tests
- Mean & Standard Deviation
	- Taken over a period of time and easy to calculate
	- Can be applied to a variety of counters, timers, and resource measures
	- Inadequate for intrusion detection if used alone
- Multivariate Calculation
	- Determines a correlation between two or more variables (processor time, resource usage, login frequency)
	- Intruder behaviour may be characterised with greater confidence by considering such a correlation
- Markov Process
	- Estimates transition probabilities among various states
	- Efficient in describing protocol run
- Time series model
	- Observes and calculates values based on sequence of events over time
	- This can be used to detect a series of actions that happen to rapidly or too slowly

###### Advantages & Disadvantages

Advantages:
- Detects previously-unknown attacks
- Doesn't need updating

Disadvantages:
- Difficult to configure/train
- Assumes that anomalous means malicious
- Generates many false alarms
- Resource intensive

#### Misuse based detection
This is when abnormal system behaviour is defined first.

This involves an attempt to define a set of rules or attack patterns that can be used to decide that a given behaviour is that of an intruder

- Often referred to a signature detection
- Relies on models of malicious behaviour
- Identify matching entries in the even stream

##### Advantages & Disadvantages

Advantages:
- Generates few false alarms
- Provides an explanation for alerts
- It's fast
- It's more resilient to evasion

Disadvantages:
- It detects only known attacks
- It needs continuous updating
- It's vulnerable to over-stimulation attacks


##### Indicator of Compromise (IoC)

These are pieces of forensic data (system log entries/files) that identify potentially malicious activity on a system or network.

These can eb host-based or network based metadata elements, but can also be complex shell code.

Host based:
- Registry key
- Process Name
- User account
- Directory Path
- File name
- File hash
- Text string in file

Network-based:
- IP addresses
- Port
- Protocol
- Domain name
- URL
- Downloaded file name or hash
- Text string in payload


### Other IDS classifications

- Timelines
	- Real-time 
	- Non real-time
- Response type
	- Passive
	- Active
- State Dependency
	- Stateful analysis
	- Stateless analysis
- System Type
	- Software
	- Hardware
- Topology
	- Host IDS
	- Network IDS
	- Distributed IDS - monitor the whole network with multiple probes


#### Host IDS

This looks for traffic on the local host
Usually the NIC is in non-promiscuous mode but also may consider:
- Logs
- System calls
- Host activities

This IDS is tuned for local services only

#### Network IDS

This eavesdrops all hosts in a network segment
- NIC is in non-promiscuous mode
- It's places at strategic locations
	- Choke points like firewalls
	- Dematerialised zones
	- Internal networks

##### Deployment

Traditional Deployment:
- Connect the IDS to a trunk port and see all network traffic
- Can detect attacks but there are no countermeasures
![[Pasted image 20230302165910.png]]

Inline Deployment:
- The IDS is deployed inline and analyses live traffic. This is the De facto in intrusion prevention systems.
- This allows the prevention of attacks

![[Pasted image 20230302165924.png]]


#### Distributed IDS
- Multiple sensors collect events and send events to a centralised manager
- Sensors can be NIDS and/or HIDS
- Manager correlates collected events
- Use a dedicated network or VPN for Probe-Manager traffic

These have evolved towards what is commercially known as: 
Security Information and Event Management (SIEM)


The host module operates as a background process on a monitored system. Collecting data on security events and sends these to the central manager.

TH e central manager receives reports from host agents and LAN monitor, processes and correlates this to report to detect intrusion.

### How IDS works
- Input Information
	- Application specific information: correct data flow
	- Host specific information: local logs, syscalls, file system changes
	- Network specific information: packets, etc.
- Intrusion detection policies
	- Known bad: blacklist with known attacks or attackers
		- Reputation based detection
		- Signature based/ rule based/ misuse based detection
	- Known good: alert anything out of usual
		- Anomaly based detection
- Response intrusions
	- Passive Response
	- Active Response


#### Data Collection

Collected Data:
- Alert data : IDS alerts
- Log data: complete host logs
- Statistical data: network stats
- Session data: 5-tuple flows
- Packet string data: HTTP headers
- Full packer capture: PCAP files

Tools:
- Packet capture: tcpdump, wireshark
- Session data: netflow, IPFIX
- Session string: URLsnarf
- Logs: syslog

We can measure performance by doing a true, false against predicted true, false like punnet square/grid.


---
Backlink: [[NSE Outline]]