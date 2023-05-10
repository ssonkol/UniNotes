# Composite Ciphers
Tags: #review 

---
## Definitions


## Notes
Ciphers are based on just substitutions or transpositions are not secure
Ciphers can be combined, however...
- Two substitutions are really only one more complex substitutions
- Two transpositions are really only one more complex transposition
- But a substitution followed by a transposition makes a new harder cipher

Hence why **Product Ciphers** also known as **Composite Ciphers** chain substitution-transposition combinations.

This is a Cipher with a $k$-bit key and $n$-bit blocks, allowing a total of $2^k$ possible transformations rather than $2^n!$


### Rotor Machines

Composite Ciphers are difficult to do by hand, which is why cipher machines came in handy (more so were invented)

These are the most common complex ciphers in use before modern ciphers, and were widely used in WW2:
- Enigma
- Hagelin
- Purple

These machines implemented a very complex, varying substitution cipher.
By using a series of cylinders, each giving one substitution, which rotated and changed after each letter was encrypted.
![[Pasted image 20221020195320.png]][1]

A good use of Composite Ciphers include the [[Feistel Cipher]].


---
## Footnotes

Backlink: [[Ciphers]]

Sources:
1. 
	- Name: [CIS-lec04.2: Composite (product) ciphers and the Feistel Cipher (part 1/2)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355005)
	- Author: Luca Vigano
	- Date: 20/10/22

