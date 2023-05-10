# Cryptanalysis & Brute Force Attacks
Tags: #review #cryptography 

---
## Notes
### Cryptographic Schema
Below is a general model for a network security

![[Pasted image 20221006174423.png]][1]
If data is to be shared between the sender (principal 1) to the recipient (principal 2) across an internet service
- Two principals must cooperate for the exchange to take place
- A logical **information channel** is established by defining a route from source to destination and by the principals used of communication protocols (e.g. TCP/IP)

### Techniques for providing security
All the techniques for providing security have two components
1. A **security-related transformation** on information to be sent
	1. Encryption of the message, which scrambles the message so that it is unreadable by an advisory.
	2. Addition of a code based on the contents of the message, which can be used to verify the identity of the sender
2. Some **secret information** shared by the two principals
	1. An encryption key used in conjunction with transformation to "scramble" message before transmission and unscramble it on reception.

A trusted third-party may be needed to achieve secure transmission
- They may be responsible for distributing the secret information to the two principals while keeping it from any opponent
- They may be needed to arbitrate disputes between two principals concerning authenticity of a message transmission.

#### The 4 Basic Tasks
The general model shows that there are 4 basic tasks:
1. Design an algorithm for performing the security-related transformation
2. Generate the secret information to be used with the algorithm
3. Develop methods for the distribution and sharing of secret information
4. Specify a protocol to be used by the two principals that makes use of the security algorithm and the secret information to achieve a particular security service

#### General Cryptographic Schema

Below is a diagram of your general cryptographic schema
![[Pasted image 20221006182013.png]] [1]

You have two types of algorithms:
- [[Symmetric Encryption]]
- [[Asymmetric Encryption]]

*Remember!!*
*==Security depends only on secrecy of the key, not the algorithm!!==*


### Cryptographic Systems

Cryptographic systems can be characterised along 3 independent dimensions:
1. The type of operations used to transform plaintext into ciphertext
	1. All encryption algorithms are based on two general principles:
		1. **Substitution**: Each element in plaintext is mapped into another element
		2. **Transposition**: Elements in plaintext are rearranged
		All of these operations must ne reversible
2. The number of keys used
	1. [[Symmetric Encryption]], single-key, secret key or conventional encryption where both sender and receiver use the same key
	2. [[Asymmetric Encryption]], two-key or public-key encryption where the sender and receiver use different keys
3. The way in which plaintext is processed
	1. [[Block Cipher]] processes input one block of elements at a time, producing an output block for each input block
	2. [[Stream Cipher]] processes input elements continuously, producing in output one element at a time, as it goes along
	3. [[Code Cipher]] process input elements one block of text at a time into a code


### Cryptanalysis & Brute-Force Attacks

#### Cryptanalysis
- Attacks rely on nature of the algorithm plus some knowledge of general characteristics of the plaintext or even some sample plaintext-ciphertext pairs
- Exploits the characteristics of the algorithm to attempt to deduce a specific plaintext or to deduce the key being used

#### Brute-Force Attack
- Attacker tries every possible key on a piece of ciphertext until an intelligible translation into plaintext is obtained
- On average, half of all possible keys must be tried to achieve success
- Its cost heavily depends on key size an on average, half of all possible keys must be tried to achieve success

### Cryptanalytic Attacks
- Always assume attackers know the algorithms used!
- Contrast with security by obscurity
	- Note that security by obscurity has been proven extremely dangerous

#### Model of Attack
![[Pasted image 20221006200932.png]][1]

**Input**: Whatever adversary necessarily knows from the beginning, e.g. public key, distribution of plaintexts

**Oracle**: Models information adversary can obtain during an attack.
	Different kinds of information characterize different types of attacks

**Output**: Whatever the adversary wants to compute e.g. secret key, partial information of plaintext

#### Types of Attack
![[Pasted image 20221006201330.png]][1]

#### How to build a definition of security
![[Pasted image 20221006201433.png]][1]

1. Specify an oracle (type of attack)
2. Define what the adversary needs to do to win the game
3. The system is secure under the definition, if any efficient adversary wind the game with only negligible probability.
#### Classification of Security
![[Pasted image 20221006201705.png]][1]

##### Unconditional Security
This is where the System (algorithm) is secure even if the attacker has unbounded computing power since the ciphertext provides insufficient information to uniquely determine the corresponding plaintext

- Security measured using information theory
- With exception of one-time pad, there's no unconditionally secure encryption algorithm.
	- Hence strive for an algorithm that meets one or both of:
	1. Cost of breaking cipher exceeds value of encrypted information
	2. Time required to break cipher exceeds useful lifetime of information

##### Conditional Security

This is where a system can be broken in principle, but this requires more computing power than a realistic attacker would have.
- Security measured using complex theory.


## Questions:

![[Pasted image 20221006202206.png]][1]

---
## Footnotes
Backlinks: [[Cryptosystems]]

Sources:

1. 
	- Name: CIS-lec02.4: Cryptanalysis and Brute-Force Attack(Slides)
	- Author: Luca Vigano
	- Date: 06/10/22