# One-Time Pad
Tag: #review 

---
## Definitions

---
## Notes
###### General Idea
This is an improvement on the [[Vernam Cipher]], where you
- Use a truly random key that is
	- As long as the message, so that the key need not be repeated
	- Used to encrypt and decrypt a single message, and then discarded


- Each new message $P$ requires a new key of same length as P
- Produces random output wit no statistical relation to plaintext
- **Unbreakable**: C **contains no information whatsoever about $P$**
Only cryptosystem that exhibits so-called perfect secrecy

![[Pasted image 20221015154105.png]][3]

Example:
>Exhaustive search of all possible keys yields many legible plaintexts, with no way of knowing which was the intended one, e.g.
>![[Pasted image 20221015154144.png]][3]
>Now suppose a cryptanalyst managed to find these two keys.
>- Two plausible plaintexts are produced.
>- Which is the correct decryption (i.e., which is the correct key)?
>
>If the actual key were produced in a truly random fashion, then cryptanalyst cannot say that one key is more likely than the other.
>
>Given any P of equal length to C, there is K that produces that P.

#### Pros & Cons of One-Time Pad

###### Pros
- Only cryptosystem that exhibits so-called perfect secrecy
	- Each new message $P$ requires a new key of same length as P
	- Produces random output wit no statistical relation to plaintext
	- **Unbreakable**: C **contains no information whatsoever about $P$**

###### Cons
- Practical Difficulties
	- Making large quantities of random keys
	- Key distribution and protection, where for every message to be sent, a key of equal length is needed by both sender and receiver

Hence

- Limited utility
- Useful primarily for low-bandwidth channels requiring very high security


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