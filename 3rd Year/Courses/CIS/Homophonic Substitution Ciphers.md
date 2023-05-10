# Homophonic Substitution Ciphers
Tag: #review 

---
## Definitions

---
## Notes

Since Mono-Alphabetic ciphers are easy to break; we can instead provide multiple substitutes (i.e. homophones) for a single letter to make frequency analysis more difficult.

##### Steps:
1. To each $a \in A$ associate a set $H(s)$ of strings of $t$ symbols, where $H(a), a \in A$ are pairwise joint
2. Replace each $a$ with a randomly chosen string from $H(a)$
3. To decrypt a string $c$ of $t$ symbols, one must determine an $a \in A$ such that $c \in H(a)$
4. The key for the cipher is the sets $H(a)$

Example:
>$A = {x, y}, H(x) = {00, 10}$, and $H(y) = {{01, 11}}$. The plaintext $xy$ encrypts to one of $0001, 0011, 1001, 1011$.
>
>Cost: data expansion and more work for decryption.

#### Cons of Homophonic Substitution Ciphers
- Cryptanalysis is still relatively straightforward
	- Each element of plaintext affects only one element of ciphertext,
	- Multiple-letter patterns still survive in the ciphertext


There are only two principal methods used in substitution ciphers to lessen the extent to which the structure of plaintext survives in ciphertext:
1. Encrypt multiple letters of plaintext
2. Use multiple cipher alphabets


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