# Mono-Alphabetic Substitution Ciphers
Tag: #review 

---
## Definitions

---
## Notes
#### General Idea
Generalise Caesar cipher by allowing an arbitrary substitution

**Permutation** of a finite set $S$ of elements: an ordered sequence of all elements of $S$, each element appearing exactly once.
- In general: $n!$ permutations of a set of n elements

Example:
> 6 permutations of $S = {a, b, c}: abc, bac, acb, bca ,cab, cba$

If the "cipher" line of a Caesar cipher can be any permutation of the 26 alphabetic characters, then there are 26! possible keys.

This is referred to as a **mono-alphabetic substitution cipher**, because a single cipher alphabet is used per message.


#### Mathematical definition

Let $K$ be the set of all permutations on the alphabet A. Define for each $e ∈ K$ an encryption transformation $E_e$ on strings $m = m_{1}m_2 · · · m_n ∈ M$ as

$E_{e}(m) = e(m_1)e(m_2)· · · e(m_n) = c_{1}c_2 · · · c_n = c$

To decrypt $c$, compute the inverse permutation $d=(c_{n)}= m$

**Remember $E_e$ is a mono-alphabetic substitution cipher!!**




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