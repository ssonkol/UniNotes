# Playfair Cipher
Tag: #review 

---
## Definitions

**Substitution Cipher**
> This is a cipher in which the letters of plaintext  are replaced by other letters or by numbers or symbols.

---
## Notes
### Playfair Cipher
This cipher uses a 5x5 matrix of letters constructed using a keyword

This is best explained by example:
> 1. Pick keyword: Monarchy

> 2. Construct matrix: 
> - This is done by filling in letters of the keywords (minus duplicates) left to right & top to bottom
> - Any remaining letters in alphabetic order, where I and J count as one letter
> ![[Pasted image 20221015141438.png]][1]
> 
> 3. Plaintext is encrypted two letters at a time:
>   If a pair is a repeated letter, insert filler like ‘X’ (e.g., “BALLOON” ; “BA LX OX ON"). Add an ‘X’ also at the end, if needed (or any other character, like the ‘A’ in this example).
> 
> 4. If both letters fall in the same row, replace each with letter to right, wrapping back to start from end (e.g., “AR" is encrypted as “RM").
>  ![[Pasted image 20221015141656.png]][1]
> 5. If both letters fall in the same column, replace each with the letter below it, wrapping to top from bottom (e.g., “MU” is encrypted as “CM").
> ![[Pasted image 20221015141750.png]][1]
> 6. Otherwise each letter is replaced by the letter in the same row and in the column of the other letter of the pair (e.g., “HS" becomes “BP" and “EA" becomes “IM", or “JM", as the encipherer wishes).
> 
>To decrypt, use the inverse (opposite) of rules 2 and 3, and the 1st as-is (dropping any extra “X"s that do not make sense in the final message when finished) and the 4th as-is.

#### Pros & Cons of Playfair Cipher

##### Pro
- Security much improved over monoalphabetic: 26 × 26 = 676 digrams vs. 26 letters.
	- Would need a 676 entry frequency table to analyse, and correspondingly more ciphertext.

##### Cons

- Still leaves much of the structure of the plaintext language intact
- A
- 
- few hundred letters of ciphertext are generally sufficient




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