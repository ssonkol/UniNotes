# Multiple-Stage Columnar Transposition Cipher
Tag: #review 

---
## Definitions

**Transposition Cipher**
>Perform some sort of permutation on the plaintext letters. Works on blocks of letters of the plaintext.

---

## Notes
#### Columnar Transposition Cipher

This is generally done by;
- Writing a message in a rectangle, row by row, and read message off, column by column, but permute the order of the columns.
- The order of the columns thus is the key to the algorithm.

For example, with key 4312567 (and with padding to fill the grid)
![[Pasted image 20221015161431.png]][1]

To encrypt, start with column labelled 1, write down all letters in that column, proceed with column labelled 2, etc.

- A pure transposition cipher is easily recognized and attacked: ciphertext has same letter frequencies as original plaintext.

#### Multiple-stage columnar transposition cipher

- A transposition cipher (columnar or not) can be made significantly more secure by **performing more than one stage of transposition**.
- Result: more complex permutation that is not easily reconstructed. 

Re-encrypting a foregoing message:
![[Pasted image 20221015161638.png]][1]

Using the same algorithm
![[Pasted image 20221015161709.png]][1]

To visualise this double transposition, designate 28 letters in original plaintext by their position

![[Pasted image 20221015161758.png]][1]

First transposition is still in quite a regular structure (+7 in blocks of 4!):
![[Pasted image 20221015161829.png]][1]

Second: less structured permutation (cryptanalysis more difficult):
![[Pasted image 20221015161850.png]][1]

With multiple stages of encryption, it can produce an algorithm that is significantly more difficult to cryptanalyze.


## Questions

---
## Footnote

Backlink: [[Transposition Ciphers]]

Sources:
1.
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12
