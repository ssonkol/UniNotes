# Polyalphabetic Substitution Ciphers
Tag: #review 

---
## Definitions

---
## Notes
#### General Idea

- Use different mono-alphabetic substitutions as one proceeds through the plaintext message.

This means there are two general features common to all such ciphers:
1. A set of related monoalphabetic substitution rules are used
2. A key determines which particular rule is chosen for a given transformation

#### Vigenère Cipher

##### Idea

Assume
- A sequence of plaintext letters $P = p_0, p_1, p_2, . . . , p_{n−1}$,
- A key consisting of the sequence of letters $K = k_0, k_1, k_2, . . . , k_{m−1}$

Typically $m < n$

Sequence of ciphertext letters $C = C_0, C_1, C_2, . . . , C_{n−1}$ :
![[Pasted image 20221015145756.png]] [2]

- First letter of the key is added to first letter of plaintext, mod 26, second letters are added, and so on through the first $m$ letters of plaintext. 
- For next $m$ letters of the plaintext, the key letters are repeated.
- Process continues until all of plaintext sequence is encrypted

Decryption: $p_i = (C_{i} − k_{i} \mod m) \mod 26$

Example:

> If the keyword is "deceptive", the message "we are discovered save yourself" is encrypted as,
> ![[Pasted image 20221015150431.png]][2]
> Expressed numerically:
> ![[Pasted image 20221015150457.png]][2]


##### Pros & Cons of Vigenère Cipher

###### Pros
- Multiple ciphertext letters for each plaintext letter, one for each unique letter of the keyword
	- Hence, letter frequency information is obscured
###### Con
- Not all knowledge of the plaintext structure is lost
- It is better than Playfair, but considerable frequency information remains

##### Saint-Cyr Slide

This is a slide used to encrypt and decrypt polyalphabetic ciphers by hand.

- A slide with repeated alphabet
- Line up plaintext "A" with key letter, e.g "C"
- Then read off any mapping for key letter
![[Pasted image 20221015151022.png]][2]





## Questions


---
## Footnote

Backlink: [[Substitution Ciphers]]

Sources:
1. 
	- Name: [CIS-lec03.1: Substitution ciphers — Caesar cipher and mono-alphabetic substitution ciphers (slides)File](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354989)
	- Author: Luca Vigano
	- Date: 15/10/22
2. 
	- Name: [CIS-lec03.2: Substitution ciphers — Homophonic substitution ciphers, Playfair cipher, Polyalphabetic substitution ciphers (Vigenère cipher) (slides)File](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354991)
	- Author: Luca Vigano
	- Date: 15/10/22
3. 
	- Name: [CIS-lec03.3: Substitution ciphers --- Vernam cipher, One-time pad (slides)File](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354993)
	- Author: Luca Vigano
	- Date: 15/10/12
4. 
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12