# Internet Key Exchange(IKE)
---
## Notes
IKE is a protocol suite for establishing and maintaining SAs (Security Association - a one-way relationship between a sender and receiver defining security services)

Typical key establishment protocol - one phase, in which parties use master keys to establish shared key material.
- Master keys - Pre-shared secret symmetric keys, public encryption key (used only for encryption/decryption), or public signature key (restricted to signing and signature verification)

IKE proceeds in two such phases:
- Phase 1 - Two parties negotiate an SA - agreeing on keying material and mechanisms to use in phase 2
- Phase 2 - The SA of phase 1 is used to create "child SAs" to encrypt and authenticate further communications

IKE established not just keys but security association such as
- The protocol format used 
- The cryptographic and hashing algorithm used
- The keys

IKE is very flexible
- It supports authentication based on a variety of pre-shared secrets (master keys)
- But also very complex
	- Many options, alternative subprotocols

### Perfect Forward Secrecy (PFS)
This is a property of key-agreement protocols ensuring that a session key derived from aa set of long-term keys cannot be compromised if one of the long-term keys is compromised in the future.
- The key used to protect transmission of data must not be used to derive any additional keys
- If the key used to protect transmission of data is derived from some other keying material, then that material must not be used to derive any more keys
	- In this way, compromise for a single key permits access only to data protected by that single key

- The trick to achieving PFS is to generate temporary session keys, not derivable from information stored at the node after the session concludes, then forget it after the session concludes
- Furthermore, periodic generation of new keys and keying material complicates cryptanalysis

### IKE Phase 1
Establish a secure channel so that phase 2 negotiations can occur privately.

- Negotiate a "ISAKMP" SA using Diffie-Hellman exchange with 
	- Cookies : to protect against DoS attacks
	- Identifier: to name partners
	- Authenticators: data computed by a MAC, h(key, data)

Typically, exchange of authenticated IDs occurs after DH exchange, so that DH key material can be used to encrypt the messages in the authentication phase
- Offer 2 modes (main mode and aggressive mode)

##### Example 
![[Pasted image 20230316132349.png]]

#### Modes & Variants
Main Mode:
- 6 messages exchanged between Initiator(I) and responder (R)
- Offers identify protection and considerable flexibility in terms of parameters and configurations that can be negotiated 
![[Pasted image 20230316131802.png]]

![[Pasted image 20230316131846.png]]


1. ISA_I (ISAKMP SA data from I) includes a series of proposals and a list of algorithms for each proposal
2. ISA_R (ISAKMP SA from R) consists of the proposals that were accepted and the algorithm chosen for each
3. Messages 3  & 4 contain the half-keys and nonces of I and R
4. Messages 5 & 6 are encrypted with the algorithm negotiated by the ISAKMP SA of 1 & 2
	- Key K is determined from Diffie Hellman k
	- ID_I and ID_R each identify a user or host (e.g. an IP address, fully-qualified domain name, certificate, or email address)
	- AUTH_I and AUTH_R is authenticated data, depending on the variant used, e.g., MAC or signature

Aggressive Mode:
- Faster without protection
- 3 messages exchanged between I and R
- This exchange occurs without identify protection, except when public-key encryption is used for authentication

Each mode has 4 variants, based on authentication method
- Pre-shared key, digital signatures, and 3 public-key variants
- The derivation of keying material and message contents depend on the authentication scheme used

### IKE Phase 2 
Establish new SAs that can be used to protect "real" communication (i.e. the IPsec SA) since phase 2 is protected by the SA established in phase 1.

New group Mode:
- Negotiate new parameters of the SAs (e.g. change cryptographic group)
- This mode does not establish new SAs (and it doesn't replace or pre-empt quick mode)


#### Quick Mode Simplified
- If PFS is required, quick mode supports a new DH exchange (optional message parts)
- Since multiple quick mode negotiations may take place simultaneously between two participants, and since each uses the cookie pair of phase 1, each is assigned a unique identifier
- Encryption uses the data of phase 1. The new key for use with the newly established SA is ![[Pasted image 20230316132848.png]] Where protocol and SPI are the protocol and SPI fields of the ISAKMP proposal payload, and k is a key produced by the DH exchange for perfect forward secrecy.

![[Pasted image 20230316132955.png]]




---
Backlink : [[IP Security]]
