# Security Attacks
---

## Notes
Cryptographic protocols are message exchange among two or more entries and are designed to resist attacks and traffic analysis.

Possible types of attacks include:
- Cryptanalysis
- Message/field insertion, deletion and change
- Replay (of a previously valid ciphertext)
- Man-in-the-middle attack

Countermeasures for each type of attack:
- Cryptoanalysis
	- Longer keys
	- Throw away weak keys
- Message/Field insertions, deletion  & Change
	- Integrity check (hash, MAC, digital signature)
- Replay attack
	- Provide freshness in protocol run
	- Timestamp, sequence number, nounce
- Man-In-The-Middle Attack
	- Cryptographic protocols should be well designed and verified
	- Use formal methods to evaluate security properties of cryptographic protocols

### Digital Signature
Attach redundant bit to transmitted data to allow the recipient to verify the source sender and integrity of the data
- This can be used to provide authentication, integrity, and non-repudiation because the signature cannot be crated by any individual except the owner of the signing key (private key)

### Authentication Exchange

- Sender and receiver negotiate to ensure the identity of each other
- General means of authentication include
	- Password
	- Fingerprint
	- Smartphone
	- 2-factor or multifactor authentication

### When to choose a means for Authentication 

- If peer entities and the means of communication are both trusted
	- Use password
- If peer entities are trusted but not the means of communication
	- Use combination of password and cryptographic protocols
- If neither peer entities nor the means of communication is trusted
	- Use the above pus non-repudiation service

### Security Mechanisms
- Access Control: Enforce a policy of limiting access to a resource to only those users who are authorised
- Traffic Padding: Insertion of bits into gaps in a data stream to frustrate traffic analysis
- Notarisation: Trusted third party to assure certain property of data exchange
- Security Audit Trail: Data collected and potentially used to facilitate a security audit
- Security recovery: Deals with requests from security mechanisms, such as event handling and management function, and takes recovery actions

### Jamming
- Takes up the transmission channel regardless of the rules specified by network protocols and affects availability for legitimate packets


It is an effective link layer attack when media is broadcast based

### Sniffing
Eavesdrop on unencrypted data in the packets
- Capture passwords and authentication tokens if they are sent in the clear
- Capture packets for later playback in replay, man-in-the-middle attack and packet injection attacks
- Packet sniffer can have a benign purpose: useful for network debugging and diagnostics

### Spoofing
This is the act of masquerading or impersonating somebody you are not.

Types of spoofing includes:
- Email spoofing
- Text Message Spoofing
- Call ID Spoofing
- URL spoofing
- DNS Spoofing
- IP Address Spoofing


---
Backlink: [[Introduction - NSE]]