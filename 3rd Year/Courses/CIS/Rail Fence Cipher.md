# Rail Fence Cipher
Tag: #review 

---
## Definitions

**Transposition Cipher**
>Perform some sort of permutation on the plaintext letters. Works on blocks of letters of the plaintext.

---

## Notes

Plaintext is written down as a sequence of diagonals and then read off as a sequence of rows. (Beware: variants exist under the same name)

**Encryption Example**:
> The message:
> 	MEET ME AFTER THE TOGA PARTY

> Will rail fence of depth 2, we write
> 	![[Pasted image 20221015160041.png]][1]
>  So that the ciphertext is
> 	 ![[Pasted image 20221015160114.png]][1]

The idea goes back to the Greek Scytale 
![[Pasted image 20221015160145.png]][1]

Decryption is done by reconstructing the diagonal grid used to encrypt the message
- Start by making a grid with as many rows as the key is, and as many columns as the length of the ciphertext.
- Place the first letter in the top left square, and dashes diagonally downwards where the letters will be.
- When we get back to the top row, we place the next letter in the ciphertext.
- Continue like this across the row, and start the next row when you reach the end.


**Decryption Example**:
- If we receive the ciphertext “TEKOOHRACIRMNREATANFTETYTGHH” encrypted with a key of 4, we have a table with 4 rows because the key is 4, and 28 columns as the ciphertext has length 28.
- We start by placing the “T” in the first square, and then dash the diagonal down spaces until we get back to the top row, and place the “E” here. Continuing to fill the top row we get:
![[Pasted image 20221015160358.png]][1]

- Continuing this row-by-row, we get the successive stages shown below:
![[Pasted image 20221015160424.png]]![[Pasted image 20221015160511.png]][1]


## Questions


---
## Footnote

Backlink: [[Transposition Ciphers]]

Sources:
1.
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12
