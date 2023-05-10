Tag: #review 

---
# Block Cipher

## Notes

A block cipher is an encryption scheme that breaks up the plaintext message into strings(blocks) of a fixed length n and encrypts one block at a time

### Method
- It takes in input one block of n bits of plaintext and a key of k bits, producing in output one block of ciphertext of n bits
- For decryption it takes in input a block of n bits of ciphertext and a key of k bits, producing in output a plaintext block of n bits.

![[Pasted image 20221006194543.png]][1]

#### Examples:

For $n=2$: 
- cyphertext  01 could come from plaintext 10 or 11![[Pasted image 20221020200905.png]][5]

##### Ideal Block Cipher

This can be used to define any reversible mapping plaintext-ciphertext

A 4-bit input produces one of 16 possible input states, which is mapped by the [[Substitution Ciphers]] into a unique one of 16 possible output states, each of which is represented by 4 ciphertext bits.

Encryption/Decryption mappings can be defined by a tabulation.

![[Pasted image 20221020201211.png]]

###### Problems
- Small block size ($n=4$): equivalent to a classical substitution cipher and thus easily attackable
- Large block size: Not practical implementation and performance

### Modes of Operation

This is a technique used for enhancing the effect of a cryptographic algorithm or adapting the algorithm for an application, such as applying a block cipher to a sequence of data blocks or a data stream.

![[Pasted image 20221108174314.png]][6]

#### Electronic Codebook (ECB)
This is the simplest mode

The plaintext is broken into N independent blocks ($P_1,...,P_N$)
- Each plaintext block $P_i$ is encrypted individually, independently of other blocks
- Requires last block to be padded to a full b bits if it is a partial block
- Each $P_i$ is a value that is substituted, like a codebook, hence name

Each ciphertext block is decrypted also individually, with same K: $P_{i}= D(K, C_i)$
![[Pasted image 20221108174651.png]][6]

##### Limitations and Ideal Use

- For lengthy messages, ECB mode may not be secure:
	- If the same b-bit block of plaintext appears more than once in the message, it always produces the same ciphertext
	- If the message is highly structured, it may be possible for a cryptanalyst to exploit these regularities.
- Hence it is not recommended for messages longer than a block
- It's ideal for a short amount of data, such as an encryption key

#### Cipher-block Chaining (CBC)

To overcome security deficiencies of ECB: same plaintext block if repeated, should produce different ciphertext blocks.

##### Steps
1. Cipher input is XOR of current plaintext block with preceding ciphertext block.
2. ![[Pasted image 20221108175425.png]][6]
3. Requires last block to be padded to a full b bit if it is a partial block

![[Pasted image 20221108175505.png]][6]

###### Correctness
![[Pasted image 20221108183356.png]][6]

Initialisation of Vector IV:
- A data block that is the same size as the cipher block
- IV must be known to both the sender and the receiver but be unpredictable by a third party and be protected against unauthorised changes
	- This could be done by sending IV using ECB encryption

##### Properties & Use

- Repeating patterns of b bits are not exposed:
	- Input to the encryption function for each plaintext block bears no fixed relationship to the plaintext block
- Properties (can be proved rigorously):
	- Identical plaintext blocks mapped to different ciphertext
	- Chaining dependencies: $C_i$ depends on all preceding plaintext
	- Self-synchronising: If an error occurs in $C_i$ but not in $C_{i+1}$ then $C_{i+2}$ is correctly decrypted
- **CBC is appropriate for encrypting messages of length greater than b bits **
- Can be used for confidentiality and for authentication

#### Block Cipher to Stream Cipher
![[Pasted image 20221108184020.png]][6]

It's possible to convert a block cipher into a stream cipher using of the modes CFB and OFB (and CTR)

A stream cipher;
- Eliminates the need to pad a message to be an integral number of blocks
- It also can operate in real time: if character stream is being transmitted, each character can be encrypted and transmitted immediately.

The desirable property of a stream cipher is that the ciphertext is the same length as plaintext.

#### Cipher Feedback (CFB)
Units of plaintext are chained together so that the ciphertext of any plaintext unit is a function of all the preceding plaintext.

Rather than blocks of b bits, plaintext is divided into segments of s bits
![[Pasted image 20221108184337.png]][6]

##### Encryption & Decryption
![[Pasted image 20221108184841.png]][6]

Although CFB can be viewed as a stream cipher, it doesn't conform to the typical construction of a stream cipher:
- A typical stream cipher takes as input some initial value and a key and generates a stream of bits, which is then XORed with plaintext bits.
- CFB is a stream of bits that is XORed with plaintext also depends on plaintext
###### Encryption

Input: b-bit shift register initially set to some initialisation vector.
- Let MSB$_s$(X) be the most significant s bits of X.
- First unit of ciphertext ![[Pasted image 20221108184504.png]][6] is XOR of
	- first segment of plaintext $P_1$
	- leftmost (most significant) s bits of output of encryption function
- Contents of shift register are shifted left by s bits, and $C_1$ is placed in rightmost (lest significant) s bits of shift register
- Process continues until all plaintext units have been encrypted
![[Pasted image 20221108184652.png]][6]

###### Decryption

Decryption uses same scheme, except that received ciphertext unit is XORed with output of encryption function to produce plaintext unit:![[Pasted image 20221108184807.png]][6]







#### Output Feedback (OFB)

OFB has a similar structure to CFB except for 2 differences:
- Output of encryption function is fed back into the shift register in OFB
	- Whereas CFB ciphertext unit is fed back to the shift register
- OFB operates on full blocks, not an s-bit subset

![[Pasted image 20221108185705.png]][6]

**Nonce**
> This is a time-varying value that has at most a negligible chance of repeating 

![[Pasted image 20221108185803.png]][6]

##### Encryption & Decryption

Nonce $I_{1} = IV$ unique to each execution of encryption operation:
- Sequence of $O_i$ depends only on key and IV an not on plaintext
- For given K and IV, stream $O_i$ used to XOR with stream $P_i$ is fixed
- If 2 different messages had an identical block of plaintext in identical position, an attacker could determine that portion of $O_i$ stream

![[Pasted image 20221108185847.png]]

OFB has a structure of a typical stream cipher (but one block at a time)
- Generates a stream of bits as a function of an initial value and a key
- The stream of bits is XORed with plaintext bits

- The generated stream that is XORed with plaintext is itself independent of plaintext
- OFB can alternatively be used keeping the shift register of CFB

###### Encryption
1. Let block size be b
2. If last plaintext block $P_N$ contains u < b bits, the most significant u bits of last output block $O_N$ are used for XOR
3. Remaining b - u bits of the last output block are discarded


#### Feedback Characteristic of modes of operation

All NIST-approved block cipher modes of operation (except ECB) involve feedback
- Think of encryption as taking input from a input register whose length equals encryption block length and with output stored in an output register
- Input register updated one block at a time by feedback mechanism
- After each update, encryption algorithm is executed, producing a result in output register
- Meanwhile, a block of plaintext is accessed

OFB and CTR outputs are independent of both plain and ciphertext
- Therefore, they are natural candidates for stream ciphers that encrypt plaintext by XOR one full block at a time.






---
## Footnotes
Links: [[Ciphers]], [[Feistel Cipher]]

Sources:
1. 
	- Name: [CIS-lec03.1: Substitution ciphers — Caesar cipher and mono-alphabetic substitution ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354989)
	- Author: Luca Vigano
	- Date: 15/10/22
2. 
	- Name: [CIS-lec03.2: Substitution ciphers — Homophonic substitution ciphers, Playfair cipher, Polyalphabetic substitution ciphers (Vigenère cipher) (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354991)
	- Author: Luca Vigano
	- Date: 15/10/22
3. 
	- Name: [CIS-lec03.3: Substitution ciphers --- Vernam cipher, One-time pad (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354993)
	- Author: Luca Vigano
	- Date: 15/10/12
4. 
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12
5. 
	- Name: [CIS-lec04.2: Composite (product) ciphers and the Feistel Cipher (part 1/2)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355005)
	- Author: Luca Vigano
	- Date: 20/10/22
6. 
	- Name: [CIS-lec06.1: Block cipher modes of operation](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355026)
	- Author: Luca Vigano
	- Date: 08/11/22 