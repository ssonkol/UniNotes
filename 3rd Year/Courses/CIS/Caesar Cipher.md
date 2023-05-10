# Caesar Cipher
Tag: #review 

---
## Definitions

---
## Notes

This cipher is implemented by cipher disks to encrypt a letter with the nth letter to the right

Example:

plain: a b c d e f g h i j k l m n o p q r s t u v w x y z
cipher: D E F G H I J K L M N O P Q R S T U V W X Y Z A B C

Mathematically, give each letter a number:
![[Pasted image 20221015131820.png]][1]

Then: $C = E(3,P) = (P + 3) \mod 26$

This is because in general:
for $K \in {1, ... , 25}:$
	$C = E(K,P) = (P + K) \mod 26$
	$P = D(K,C) = (C - K) \mod 26$

Use modulo 26 since from 0-25 there are 26 numbers.

##### Why is brute-force cryptanalysis possible?

There are 3 important characteristics enabling us to use a brute-fore method.
1. The encryption and decryption algorithms are known
2. There are only 25 keys to try
3. The language of the plaintext is known and easily recognizable

What generally makes brute-fore cryptanalysis impractical is the use of an algorithm that employs a large number.
If the language of the plaintext is unknown, then the output may not be recognisable, furthermore, there could also be two possible sensible plaintexts in two different languages


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