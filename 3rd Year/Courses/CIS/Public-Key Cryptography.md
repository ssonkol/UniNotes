# Public-Key Cryptography
Tag: #review 

---
## Definitions

---
## Notes

### Keys
#### Hierarchy of keys
- Session Key
	- Used to encrypt data between users for 1 session then discarded
- Master Key
	- Used to encrypt session keys
	- Shared by user(s) and key distribution center (KDC)

![[Pasted image 20221108191850.png]][1]

#### Key distribution issues

- Hierarchies of KDCs required for large networks, but requires mutual trust between agents involved
- Session key lifetimes should be limited for greater security
- Use of automatic key distribution on behalf of users, but then must trust system 
- Use of decentralized key distribution
- Controlling key usage


### Public-Key Cryptography

1. Let {E$_e$ | e ∈ K} and {D$_d$ | d ∈ K} form an encryption scheme
2. Consider transformation pairs (E$_e$ , D$_d$ ) where knowing E$_e$ it is infeasible, given c ∈ C, to find an m ∈ M such that E$_e$ (m) = c
3. This implies it is infeasible to determine d from e. Hence, E$_e$ constitutes a trap-door one-way function with trapdoor d (as explained in more detail later)
4. Called public key as e can be public information:

##### Encryption/Authentication
![[Pasted image 20221108192412.png]][1]

##### Conventional (Symmetric) Encryption vs Public-Key (asymmetric) Encryption

**Conventional Encryption**

Needed to work
1. The same algorithm with the same key is used for encryption and decryption
2. The sender and receiver must share the algorithm and the key.

Needed for Security
1. The key must be kept secret
2. It must be impossible or at least impractical to decipher a message if the key is kept secret.
3. Knowledge of the algorithm plus samples of ciphertext must be insufficient to determine the key


**Public-Key Encryption**

Needed to Work:
1. One algorithm is used for encryption and a related algorithm for decryption with a pair of keys, one for encryption and one for decryption
2. The sender and receiver must each have one of the matched pair of keys (not the same one)

Needed for Security:
1. One of the two keys must be kept secret
2. It must be impossible or at least impractical to decipher a message if one of the keys is kept secret
3. Knowledge of the algorithm plus one of the keys plus samples of ciphertext must be insufficient to determine the other key

##### Secrecy & Authentication
![[Pasted image 20221108193254.png]][1]

###### Secrecy 
X is a secret intended for B
Only B, who possesses PR$_b$, can decrypt Y = E(PU$_B$, X)![[Pasted image 20221108193035.png]][1]

###### Authentication
Only A, who possesses PR$_a$, can have generated Y = E(PU$_A$, X)
Note that everybody can decrypt Y (and read X) as PU$_a$ is public![[Pasted image 20221108193204.png]][1]

#### Applications of Public-key Cryptosystems

Encryption/Decryption
- Sender encrypts a message with recipient's public key

Key exchange
- Two sides cooperate to exchange a session key
- Different approaches are possible, involving private key(s) of on or both parties

Digital Signature
- Sender "signs" a message with its private key
- Signing is achieved by a cryptographic algorithm applied to a message or to a small block of data that is a function of a message

#### Requirements for Public-Key cryptography

1. It is computationally easy for any principal B to generate a pair (public key PU$_b$, private key PR$_b$)
2. It is computationally easy for sender A, knowing PU$_b$ and M, to generate C = E(PU$_b$, M)
3. It is computationally easy for receiver B to decrypt C using PR$_b$ to recover M: M = D(PR$_b$, C) = D(PR$_b$, E(PU$_b$, M))
4. It is computationally infeasible for an adversary knowing PU$_b$ to determine PR$_b$, knowing PR$_b$ and C to recover M
5. (Useful, but not always necessary) The two keys can be applied in either order:
			M = D(PU$_b$, E(PR$_b$, M)) = D(PR$_b$, E(PU$_b$, M)).

![[Pasted image 20221108193824.png]][1]

### Summary
- Brute-force attacks are possible
	- Countermeasure: use large keys!
		- But trade-off is necessary as complexity of encryption/decryption may not scale linearly with the length of the key
		- In practice: public-key encryption is confined to key management and digital signature
- Computing private key from public key
	- No proof that this attack is infeasible! (Not even for RSA)
- Probable-message attack


---
## Footnote

Backlink: [[Cryptosystems]]

Sources:
1. 
	- Name: [Introduction to Public-key Cryptography](https://keats.kcl.ac.uk/pluginfile.php/8503969/mod_resource/content/2/CIS-lec06.2.pdf)
	- Author: Luca Vigano
	- Date: 08/11/22