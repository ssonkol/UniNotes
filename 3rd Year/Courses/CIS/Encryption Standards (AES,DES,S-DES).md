# Encryption Standards (AES,DES,S-DES)
Tags: #review #cryptography 

---
## Notes

### Data Encryption Standard

#### Overall Scheme
DES has a block size of 64 bits
- Plaintext and ciphertext space
	- $M = C = (0,1)^{64}$
- Input:
	- Plaintext: 64 bits
	- Key: 56 bits
	*Note: 64 bit key as input but only 56 are used*
- Output: 64 bits


DES keys are all bit-strings of length 64 with the following property:
- If a 64-bit DES key is divided into 8 bytes, then the sum of the 8 bits of each byte is odd

This means that 7 of the 8 bits determine the value of the 8th bit, and that transmission errors of one bit can be stopped.

Therefore the key space is![[Pasted image 20221027145908.png]][1]


Plaintext is processed in 3 phases:
1. Initial permutation (IP) rearranges bits to produce permuted input
2. 16 rounds of both permutation and substitution functions
	- Output of $16^{th}$ round: 
		- 64 bits, function of input plaintext and key
	- Left and right halves of output swapped to produce pre-output
3. Pre-output is passed through IP$^{-1}$ to finally produce the 64-bit ciphertext
![[Pasted image 20221027151329.png]]

*Note: IP and IP$^{-1}$* have no real cryptographic significance (it's included to facilitate loading blocks in and out of mid-1970s 8-bit based hardware).

The use of the 56-bit key is as follows:
- Initially, the key is passed through permutation functions
- For each of the 16 rounds, a subkey K$_i$ is produced by combination of a left circular shift and a permutation
	- Permutation function is the same for each round
	- A different subkey is produced because of repeated shifts of key bits
![[Pasted image 20221027151855.png]][1]


**IP and IP$^{-1}$ defined by tables**:
- Input to a table consists of 64 bits numbered from 1-64
- 64 entries in permutation table contain a permutation of numbers from 1-64
- Each entry in permutation table indicates position of a numbered input bit in output which also consists of 64 bits
- Even bits to LH half, odd bits to RH half

**Example**:
Consider 64-bit input M (left) and permutation IP(M) (right)![[Pasted image 20221027152411.png]][1]

IP$^{-1}$(IP(M)) restores original ordering of bits.

#### Details of Single Round![[Pasted image 20221027152452.png]][1]

- L and R halves of each 64-bit intermediate value treated as separate 32-bit quantities.
- As in any classic Feistel cipher, overall processing at each round is:![[Pasted image 20221027152528.png]][1]
- Round key K$_i$ is 48 bits
- R$_{i-1}$ is 32 bits
	- Is expanded to 48 bits by using Expansion Permutation (E) table, which defines a permutation plus an expansion that involves duplication of 16 bits of R$_{i−1}$. 
	- Resulting 48 bits are XORed with K$_i$
![[Pasted image 20221027152730.png]][1]

- 48-bit result of XOR passes through a substitution function (S-box) that produces a 32-bit output, which is permuted by using a table (Permutation Function P)![[Pasted image 20221027152850.png]][1]

The role of S-boxes in F is illustrated in the below figure![[Pasted image 20221027152930.png]][1]

- Substitution consists of a set of 8 S-boxes, each of which accepts 6 bits as input and produces 4 bits as output.

These transformers are defined as below:
- First and last bits of the input to box Si form a 2-bit binary number to select 1 of 4 substitutions defined by four rows in the table for S$_i$
- Middle 4 bits select one of the 16 columns
- Decimal value in the cell selected by the row and column is then converted to its 4-bit representation to produce output.
	- Example: in S$_1$, for input 011001, the row is 01 (row 1) and the column is 1100 (column 12)
	- The value in row 1, column 12 is 9, so the output is 1001
	- Each row of an S-box defines a general reversible substitution.
![[Pasted image 20221027153148.png]][1]

**Key Generation**:
![[Pasted image 20221027153227.png]][1]

- 64-bit key used as input (bits 1..64)
- Every eighth bit is ignored, as indicated by lack of shading in table (a)
- Key first subjected to a permutation governed by table (b) **Permuted Choice One**
- Resulting 56-bit key then treated as two 28-bit quantities C$_0$ and D$_{0}$
- At each round, C$_{i−1}$ and D$_{i−1}$ separately subjected to a **circular left shift** (rotation) of 1 or 2 bits, as governed by table (d)
- These shifted values serve as input to
	- Next round, and
	- **Permuted Choice Two** (table (c)), which produces a 48-bit output that serves as input to function $F(R_{i−1}, K_i )$
![[Pasted image 20221027153505.png]][1]

#### DES Decryption
As with any Feistel cipher, decryption uses the same algorithm as encryption, except that the application of the subkeys is reversed.

### An example of DES
Consider P = 0123456789ABCDEF, whose binary expansion is![[Pasted image 20221027153748.png]][2]

The application of IP yields![[Pasted image 20221027153817.png]][1]
Given we have the IP![[Pasted image 20221027153844.png]][2]

So we obtain![[Pasted image 20221027154314.png]][2]


- We use key 133457799BBCDFF1, whose binary expansion is![[Pasted image 20221027154343.png]][2]
- We compute the first round key. To ignore every 8th bit (as in table (a))![[Pasted image 20221027154428.png]][2]
- We carry out a permutation governed by Permuted Choice One (table (b))![[Pasted image 20221027154441.png]][2]
- Resulting 56-bit key then treated as two 28-bit quantities C$_0$ (denoted in green) and D$_0$ (denoted in yellow)


- C0 = 1111000011001100101010101111
	D0 = 0101010101100110011110001111

- At each round, Ci−1 and Di−1 separately subjected to a circular left shift (rotation) of 1 or 2 bits, as governed by table (d)

- For instance, C1 and D1 are obtained by a left shift 1:
	C1 = 1110000110011001010101011111
	D1 = 1010101011001100111100011110

- These shifted values serve as input to
	- next round, and
	- Permuted Choice Two (table (c)), which produces a 48-bit output that serves as input to function F(Ri−1, Ki )

- From C1 and D1, by table (c), we obtain
	K1 = 000110110000001011101111111111000111000001110010
![[Pasted image 20221027154752.png]][2]
- Using
		R$_0$ = 11110000101010101111000010101010
		K$_1$ = 00011011000000101110111111111100 0111000001110010 
- And the expansion permutation E we obtain 
		E(R$_0$) ⊕ K$_1$ = 011000010001011110111010100 001100110010100100111 
		![[Pasted image 20221027155144.png]][2]
- which, given in input to S-box and permutation P, yields 
		F(R$_0$, K$_1$) = 00100011010010101010100110111011 
- Finally, an XOR with 
		L$_0$ = 11001100000000001100110011111111 
- yields 
		R$_1$ = 11101111010010100110010101000100 

- The other rounds are computed analogously.





#### Security of DES
Since its invention, security of DES has been studied very intensively. Special techniques such as differential cryptanalysis and linear cryptanalysis have been invented to attack DES, but the most successful attack has been an exhaustive search of the key space.
- With special hardware or large networks of workstations, it is now possible to decrypt DES ciphertexts in a few days or even a few hours.
	- 7 hours with 1 million dollar computer in 1993.
	- Soon DES will be breakable on a single PC

##### Increasing DES Security: Double DES

**Idea**: Perform two DES encryptions![[Pasted image 20221027155516.png]][2]

**Attack**: Meet in the Middle
- For C = E(K$_2$, E(K$_1$, P)) let X = E(K$_1$, P) = D(K$_2$, C)
- Given known P and C encrypt P for all 2$^{56}$  possible K$_1$
- Store in table, sorted by X
- Decrypt C with all 2$^{56}$  possible K$_2$ and look for a match
- Each hit is a candidate solution. Validate with additional plain/cipher-text pair
- A known plaintext attack against double DES (112 bit keys) will succeed with effort on the order of 2$^{56}$ operations. 

##### Increasing DES Security: Triple DES
Use 3 stages of encryption instead of 2, with 2 keys K$_1$, K$_2$:![[Pasted image 20221027160003.png]][2]

- **Compatibility** is maintained with standard DES (K$_2$ = K$_1$).
- No known practical attack ⇒ brute-force search with 2$^{112}$ operations. Triple DES with 3 different keys K$_1$, K$_2$, K$_3$ exists as well:
	- Effective key length of 168 bits.
	- Adopted by some Internet applications (e.g., PGP and S/MIME)

### Advanced Encryption Standard
This is a symmetric block cipher intended to replace DES for commercial applications
- 1997: NIST initiated selection process for the successor of DES. One of the submissions was the Rijndael cipher (named after its inventors Rijmen and Daemen)
- 2001: this encryption scheme standardized as the Advanced Encryption Standard
- AES special case of Rijndael, which admits more different block lengths and ciphertext spaces

AES uses a 128-bit block size and a key size of 128, 192, or 256 bits

AES does not use a Feistel structure.
	- Instead, each full round consists of 4 separate functions: byte substitution, permutation, arithmetic operations over a finite field, and XOR with a key.

#### AES Encryption
- Plaintext block size of 128 bits, or 16 bytes
- Key length can be 16, 24, or 32 bytes (128, 192, or 256 bits)
- Algorithm referred to as AES-128, AES-192, or AES-256, depending on key length
- Cipher consists of N rounds, depending on key length:
	- 10 rounds for a 16-byte key
	- 12 rounds for a 24-byte key
	- 14 rounds for a 32-byte key
![[Pasted image 20221027160859.png]][3]

### Simplified DES
S-DES is a simplified version of the DES (Data Encryption Standard) algorithm.

It closely resembles the real thing, with smaller parameters, to facilitate operation by hand for pedagogical purposes. It is not intended as a real encryption tool, rather as a teaching tool.


![[Pasted image 20221027163846.png]]

- S-DES works with an 8-bit plaintext (and thus an 8-bit ciphertext) and a 10-bit key
- S-DES involves several fixed operations involving particular permutations or other kinds of operators
- It starts by using the following 8-bit initial permutation IP:![[Pasted image 20221027163921.png]][4]
- and ends with the inverse permutation IP$^{−1}$ :![[Pasted image 20221027163936.png]][4]

S-DES also uses
- The expansion permutation E/P, whereby 2 separate permutations are applied to a 4-bit number:![[Pasted image 20221027164035.png]][4]

- The 4-bit permutation P4:![[Pasted image 20221027164049.png]][4]
- The two S-boxes:![[Pasted image 20221027164127.png]][4]
- The swap operation SW:![[Pasted image 20221027164152.png]][4]


![[Pasted image 20221027164258.png]][4]

#### S-DES Key Generation

Given the 10-bit key K = (k$_0$ k$_1$ . . . k$_{9}$), where k$_i$ ∈ {0, 1}, the subkeys are generated as follows
- There are two given permutations![[Pasted image 20221027164449.png]][4] 
	and a shifting sequence (1, 2).
- First apply P10 (which is used only once) to the key and get P10(K) = (k$_2$ k$_4$ k$_1$ k$_6$ k$_3$ k$_9$ k$_0$ k$_8$ k$_7$ k$_5$) = (s$_0$ s$_1$ s$_2$ s$_3$ s$_4$ s$_5$ s$_6$ s$_7$ s$_8$ s$_9$), where s$_0$ = k$_2$, s$_1$ = k$_4$, …, s$_9$ = k$_5$
- Break this string (s$_0$ s$_1$ s$_2$ s$_3$ s$_4$ s$_5$ s$_6$ s$_7$ s$_8$ s$_9$) into two substrings consisting of the first 5 and the last 5 bits and shift each substring to the left by 1, since 1 is the first number in the shifting sequence (1, 2)
- Apply ![[Pasted image 20221027164815.png]][4] to pick out and permute 8 of the 10 bits, and obtain key 1:
	- P8(Shift$_1$ (P10(K))) =![[Pasted image 20221027164910.png]] [4]

*Note: the examples continue - laziness ensues so I've just decided to continue copy and pasting the examples*

#### S-DES Sub-Key Generation
![[Pasted image 20221027165116.png]]![[Pasted image 20221027165127.png]][4]

#### Encryption Example
![[Pasted image 20221027165208.png]]![[Pasted image 20221027165223.png]]![[Pasted image 20221027165251.png]]![[Pasted image 20221027165349.png]][4]


#### Decryption Example
![[Pasted image 20221027165423.png]]
![[Pasted image 20221027165436.png]]
![[Pasted image 20221027165452.png]]
![[Pasted image 20221027165508.png]]

## Questions:

---
## Footnotes
Backlinks: [[Cryptosystems]]

Sources:
1. 
	- Name: [CIS-lec05.1: DES: the Data Encryption Standard](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355014)
	- Author: Luca Vigano
	- Date: 27/10/22
2. 
	- Name: [CIS-lec05.2: An example of DES, and Security of DES and Triple DES](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355016)
	- Author: Luca Vigano
	- Date: 27/10/22
3. 
	- Name: [CIS-lec05.3: AES: Advanced Encryption Standard](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355018)
	- Author: Luca Vigano
	- Date: 27/10/22
4. 
	- Name: [CIS-lec05.4 (reading material): Simplified DES (S-DES)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355020)
	- Author: Luca Vigano
	- Date: 27/10/22