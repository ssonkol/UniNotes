# Honeypots
---

## Notes

Honeypots are traps set to detect, deflect, or in some manner counteract attempts at unauthorised use of information or network systems.

Honeypots are decoy systems that are designed to lure a potential attacker away from critical systems.

It can be viewed as an intrusion detection technique used to:
- Learn from unknown attacks
- Study intruders modus operandi
- Better identify, understand and protect against threats

Traffic landing in a honeypot is unsolicited.

It can be used for:
- Prevention
- Detection
- Information Gathering

#### Honeypot Value

- No production value
	- These systems are filled with fabricated information designed to appear valuable but a legitimate user of the system won't have access to
	- Any attempt to communicate with the system is most likely a probe, scan or attack
- Honeypot intrusion prevention
	- Divert an attacker from accessing critical systems
	- Collect information about the attackers activity
	- Encourage the attacker to stay on the system long enough for administrators to respond
	- Any attack against the honeypot is made to seem successful, administrators have time to mobilise and log and track the attacker without ever exposing productive systems

### Deployment

Typically located in the DMZ,  or outside the boundary router. A honey trap can also be installed on an internal network, virtual environment.

They are made to look as real as possible with in-depth monitoring that is relevant to the attacker.


### Classification

#### By purpose

Production Honeypots:
- These are meant to be used in production environments of companies.
- They are characterised by the ease of deployment and utilisation
- They are a trade-off between ease of operation and the quantity of collected information

Research Honeypots:
- These provide comprehensive information about attacks
- However they are more difficult to deploy

#### By Level of Interaction

Low Interaction Honeypots:
- Emulate a small set of services, application
- They cannot be exploited to get complete access to the honeypot
- They attacker is limited to the level of emulation
- These tend to be production honeypots

	Advantages:
	- Low risk
	- Easy to deploy/maintain
	Disadvantages:
	- Capture limited information

High interaction Honeypots:
- These use real operating systems and applications
- The attacker gains full access at the network/system
- They tend to be used in research honeypots

	Advantages:
	- Capture extensive information
	Disadvantages
	- High risk and time intensive to maintain

#### By Implementation

Physical Honeypot:
- A real machine on the network

Virtual Honeypot:
- Simulated or virtualised by a host machine that forwards the network traffic to the virtual honeypot
- Multiple virtual honeypots can be simulated on a single host
- Usually high-interaction honeypots

#### By direction of the interaction
- Server Honeypots
- Client Honeypots

### How Honeypots Work

#### 1.  Data Control

Honeypots control and contain the activities of an attacker by interacting with the attacker through network protocols

Bandwidth throttling - Intentionally slowing or speeding of an internet service by an Internet Service Provider (ISP)

#### 2. Data Capture

Honeypots monitor and log all of the activities of an attacker within the honeypot - this is kept at all levels (Network activity, Application activity, System activity.

It then stores all captured data in one central location.

#### 3. Data Analysis

The honeypots analyse the data being collected.

Human driven analysis:
- Rely on automated tools to process the data

Machine driven analysis:
- Assume that the network connection are either:
	- Malicious
	- Anomalous

### Case Study

RAT - Remote Administration Tool

This is a tool that gives a remote attacker total interactive access to a victims machine.
They can:
- Capture audio from microphone
- Capture video from webcam
- Log keyboard input
- Browse files on a machine

#### Methodology
![[Pasted image 20230302190939.png]]

1. Collection of DarkComet malware samples by regularly querying VirusTotal Intelligence
2. Extraction from the samples:
	- Password to decrypt network comms with the controller
	- Version of DarkComet
	- Campaign ID
	- Info about the controller : Domain Names, IP addresses, Ports
3. Scanning
	- Use tools to conduct internet wide scans for DarkComet controllers
4. Controller Monitoring
	- Continuously probe every known DarkComet controller to determine if the service is online or not
	- Use DNS resolution to track controllers that use dynamic DNS services to frequently change IP addresses
	- Controller is the part of the DarkComet malware that runs at the attacker's machine to control the other part of the malware running at the victims machine.
5. Operator Monitoring
	- Design and deploy honeypots on the VM, capture network traffic on pcap etc.![[Pasted image 20230302191054.png]]
6. Behaviour reconstruction
	- Over two experiments
		- 1165 samples
		- 2747 total sessions recorded
		- Reconstructed the network traffic
		- Analyse the operations that occurred
		- Capture screen (and timestamp)
		- Capture changes for Remote Desktop Protocol sessions
		- 785 sessions resulted in engagement with the operator
		- Several week long experiment

### Honeytokens

Honeytokens are honeypots that are not computer systems but:
- Unused email addresses
- Fake database entries
- etc.

Their value lies not in their use, but in their abuse
- Their use in inherently suspicious
- Necessarily malicious

#### Common Honeytokens

Bogus medical records
- Donal Trump created in database
	- Record has no true value since ther is no real patient with that name. Instead, the record is a honeytoken, an entity that has no authorised use.
	- If an employee is looking for interesting patient data, this record will definitely stand out. If the employee attempts to access this record, you will most likely have an employee violating patient privacy.
	- 


---
Backlink: [[NSE Outline]]
