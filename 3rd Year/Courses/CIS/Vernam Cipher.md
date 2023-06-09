# Vernam Cipher
Tag: #review 

---
## Definitions


---
## Notes
This is a proposed system where the keyword is as long as plaintext and has no statistical relationship to it.

It works on bits rather than letters using XOR ($\oplus$):
![[Pasted image 20221015151329.png]] [3]

So that
![[Pasted image 20221015151452.png]][3]

Remember _XOR gate_ is a digital logic gate that gives a true (1 or HIGH) output when the number of true inputs is odd.

###### General Idea

$P \oplus K = C$
$C \oplus K = P$

![[Pasted image 20221015152723.png]][3]

- $p_{i}$/$c_{i}$/$k_{i}=i^{th}$ binary digit of plaintext/ciphertext/key
- Ciphertext generated by bitwise XOR of plaintext and key
- Decryption: simply same bitwise operation (by properties of XOR)
- Essence of this cipher: means of construction of the key

## Questions
![[Pasted image 20221015162051.png]]

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